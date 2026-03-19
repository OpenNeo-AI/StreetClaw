---
name: github-sync
description: GitHub 文件同步工具。当需要向 GitHub 仓库推送文件、提交代码、更新文件时使用此技能。支持获取 SHA、自动创建/更新文件、批量推送。使用环境变量 GH_TOKEN（GitHub Personal Access Token）进行认证，不需要硬编码凭证。
---

# GitHub Sync · 代码同步技能

## 环境变量

| 变量 | 说明 | 获取方式 |
|------|------|---------|
| `GH_TOKEN` | GitHub Personal Access Token | GitHub Settings → Developer settings → Personal access tokens |
| `GITHUB_USER` | GitHub 用户名 | GitHub 主页用户名 |

## 核心操作

### 推送单个文件到 GitHub

```python
import urllib.request, base64, json, os

TOKEN = os.environ["GH_TOKEN"]
REPO = "Owner/RepoName"  # 例如 "OpenNeo-AI/StreetClaw"
BRANCH = "main"

def push_file(fname, local_path, commit_message):
    encoded = urllib.request.quote(fname, safe="")
    
    # 1. 获取文件当前 SHA（如果存在）
    sha = None
    req = urllib.request.Request(
        f"https://api.github.com/repos/{REPO}/contents/{encoded}",
        headers={"Authorization": f"token {TOKEN}"}
    )
    try:
        resp = urllib.request.urlopen(req, timeout=8)
        sha = json.loads(resp.read()).get("sha")
    except urllib.error.HTTPError as e:
        if e.code != 404:
            raise

    # 2. 读取本地文件并 Base64 编码
    with open(local_path, "rb") as f:
        content_b64 = base64.b64encode(f.read()).decode()

    # 3. 推送文件
    payload = {
        "message": commit_message,
        "content": content_b64,
        "branch": BRANCH,
    }
    if sha:
        payload["sha"] = sha  # 更新需要 SHA

    req2 = urllib.request.Request(
        f"https://api.github.com/repos/{REPO}/contents/{encoded}",
        data=json.dumps(payload).encode(),
        headers={"Authorization": f"token {TOKEN}", "Content-Type": "application/json"},
        method="PUT"
    )
    resp2 = urllib.request.urlopen(req2, timeout=15)
    result = json.loads(resp2.read())
    return result.get("content", {}).get("sha", "")[:8]
```

### 批量推送多个文件

```python
def push_files(files, repo, branch="main"):
    """
    files: list of (remote_fname, local_path, commit_message)
    """
    results = []
    for fname, fpath, msg in files:
        try:
            sha = push_file(fname, fpath, msg, repo, branch)
            results.append((fname, True, sha))
        except Exception as e:
            results.append((fname, False, str(e)[:60]))
    return results
```

## 注意事项

- ⚠️ **不要硬编码 TOKEN** — 始终从 `os.environ["GH_TOKEN"]` 读取
- ⚠️ **文件名含中文需要 URL 编码** — 用 `urllib.request.quote(fname, safe="")`
- ⚠️ **更新文件必须提供 SHA** — 否则返回 400 错误
- ⚠️ **避免循环调用** — exec 工具频繁调用会触发 loop 检测，建议用 Python 脚本批量处理后一次性 exec
- ⚠️ **大文件（如海报图片）Base64 后可能超时** — 适当增加 timeout

## 常见错误处理

| 错误 | 原因 | 解决方案 |
|------|------|---------|
| HTTP 400 Bad Request | SHA 不正确或 payload 格式错误 | 先 GET 获取最新 SHA |
| HTTP 401 | Token 无效或权限不足 | 检查 GH_TOKEN 权限 |
| HTTP 404 | 文件不存在（新建时 SHA 为 None 正常）| 正常，继续创建 |
| HTTP 409 | 文件内容无变化 | 可以忽略，SHA 不变 |
| exec loop detected | 频繁调用 exec | 改用 Python 脚本一次性完成所有网络请求 |

## 快速验证 Token 是否有效

```python
import urllib.request, json, os
req = urllib.request.Request(
    "https://api.github.com/user",
    headers={"Authorization": f"token {os.environ['GH_TOKEN']}"}
)
resp = urllib.request.urlopen(req, timeout=8)
user = json.loads(resp.read())
print("Username:", user["login"])
```
