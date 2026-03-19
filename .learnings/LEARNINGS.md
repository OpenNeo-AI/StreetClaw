# LEARNINGS.md — 虾逛自我提升日志

---

## [LRN-20260319-001] best_practice

**Logged**: 2026-03-19T10:00:00Z
**Priority**: medium
**Status**: pending
**Area**: config

### Summary
飞书 OAuth 设备码流程：device_code + poll 模式，无需公网 Webhook

### Details
飞书连接使用 OAuth 设备码流程：
1. POST https://accounts.feishu.cn/oauth/v1/app/registration action=init
2. POST action=begin 获取 device_code + verification_uri
3. 拼接 &from=maxclaw 生成用户授权链接
4. 用户操作完成后，POST action=poll 获取 client_id + client_secret
5. 凭 client_id/secret 配置飞书频道

### Suggested Action
未来连接其他平台优先考虑设备码/长连接模式，无需配置公网回调

### Metadata
- Source: conversation
- Tags: feishu, oauth, device_flow

---

## [LRN-20260319-002] best_practice

**Logged**: 2026-03-19T10:05:00Z
**Priority**: medium
**Status**: pending
**Area**: infra

### Summary
git clone 时嵌入 token 的正确语法：https://token@github.com/owner/repo

### Details
git clone https://ghp_TOKEN@github.com/owner/repo 可以直接附带认证信息，避免交互式登录。缺点是 token 会在 ps aux 中可见，生产环境应设 GIT_ASKPASS 或 netrc

### Suggested Action
自动化脚本中用嵌入式 token，交互环境用 GIT_ASKPASS

### Metadata
- Source: error
- Tags: git, auth, security

---

## [LRN-20260319-003] best_practice

**Logged**: 2026-03-19T10:10:00Z
**Priority**: medium
**Status**: pending
**Area**: infra

### Summary
skillhub 安装技能默认保存到 /workspace/skills/，需手动迁移到 /root/.openclaw/skills/

### Details
skillhub install 输出显示 "Installed: xxx -> /workspace/skills/xxx"，但 OpenClaw 实际从 /root/.openclaw/skills/ 读取技能。安装后必须手动 cp -r /workspace/skills/* /root/.openclaw/skills/

### Suggested Action
每次 skillhub install 后立即执行迁移命令，确保技能可用

### Metadata
- Source: error
- Related Files: /workspace/skills/, /root/.openclaw/skills/
- Tags: skillhub, openclaw, skills

---

## [LRN-20260319-004] knowledge_gap

**Logged**: 2026-03-19T10:15:00Z
**Priority**: high
**Status**: pending
**Area**: infra

### Summary
xiaohongshu-mcp 在 SkillHub 上不存在（HTTP 404）

### Details
xiaohongshu-mcp 安装请求返回 404，SkillHub 注册表中无此技能。可能使用不同名称，或需要独立安装

### Suggested Action
搜索 SkillHub 确认正确名称；也可能需要从其他源安装小红书 MCP

### Metadata
- Source: error
- Tags: xiaohongshu, skillhub, 404

---

## [LRN-20260319-005] best_practice

**Logged**: 2026-03-19T10:18:00Z
**Priority**: medium
**Status**: pending
**Area**: infra

### Summary
skillhub install 的 --cli-only 标志只装 CLI，不装技能

### Details
install.sh 脚本支持 --cli-only 参数，仅安装 /root/.local/bin/skillhub CLI 工具，不带 --cli-only 时才安装技能到 /workspace/skills/

### Metadata
- Source: conversation
- Tags: skillhub, cli

---

## [LRN-20260319-006] best_practice

**Logged**: 2026-03-19T10:20:00Z
**Priority**: high
**Status**: pending
**Area**: config

### Summary
OpenClaw Gateway 无法通过 exec 重启，必须告知用户在 MaxClaw 设置菜单点击重启按钮

### Details
系统规则明确：若需要重启 Gateway，必须告知用户在 MaxClaw 设置菜单操作，不能自己调用 restart 命令（gateway tool 的 restart 仅用于特定场景）。openclaw gateway restart 属于需要交互的操作，用户无法在服务器上执行

### Suggested Action
需要重启时，直接告知用户操作方法，不调用 exec

### Metadata
- Source: error
- Tags: openclaw, gateway, restart

---

## [LRN-20260319-007] best_practice

**Logged**: 2026-03-19T10:23:00Z
**Priority**: medium
**Status**: pending
**Area**: infra

### Summary
DeepSeek 分享页面内容藏在 og:description 元标签中

### Details
chat.deepseek.com 分享页面是 JS 渲染，curl 直接拿不到内容，但 og:description 和 twitter:description 会包含对话摘要文本。提取方法：grep -oP 'og:description.*content="[^"]*"' 抽出片段

### Suggested Action
后续提取 DeepSeek 分享内容优先用 curl 拿 og:description，再人工解读

### Metadata
- Source: error
- Tags: deepseek, web_scraping, seo_metadata

---
