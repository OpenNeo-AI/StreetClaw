---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 304402202dbe88d06d0e9077d63b7ee8807e12a51c1b15956a8afe8628e2d3eca856397602200bed2f022d90fe84ff4281f2280d2119eb2104692b8ccc2c663f0e451e870e40
    ReservedCode2: 3045022100b6348a7ca2a79851b8cc96e75bdc6faaa4ecade6f9c07f386361519f251005cb02204d17f60ce7ca3e6262e08bff89ec9a8999800f500e802cbb531c74118f0a5631
description: 日志记录子技能 - 记录文档创建结果到日志文件，支持 Markdown 和 JSON 格式。
name: feishu-logger
---

# 日志记录子技能

## 职责
收集所有步骤的结果，记录到日志文件（Markdown 和 JSON 格式）。

## 输入
- `blocks.json` - 解析结果
- `doc_info.json` - 文档信息
- `add_result.json` - 块添加结果
- `permission_result.json` - 权限操作结果
- `verify_result.json` - 验证结果

## 输出
- `CREATED_DOCS.md` - Markdown 格式日志
- `created_docs.json` - JSON 格式日志

## 工作流程

### 第一步：加载所有结果文件
从工作流目录加载所有 JSON 结果文件。

### 第二步：汇总信息
提取关键信息：文档 ID、URL、权限状态、验证状态等。

### 第三步：更新日志文件
追加记录到 `CREATED_DOCS.md` 和 `created_docs.json`。

### 第四步：打印摘要
在控制台打印创建摘要。

## 数据格式

### CREATED_DOCS.md 格式
```markdown
## 文档标题

- **时间**: 2026-01-22 10:30:00
- **文档ID**: `U2wNd2rMkot6fzxr67ScN7hJn7c`
- **URL**: [https://feishu.cn/docx/U2wNd2rMkot6fzxr67ScN7hJn7c](...)
- **collaborator_added**: True
- **owner_transferred**: True
- **user_has_full_control**: True
- **document_verified**: True
- **tables_created**: 10
- **blocks_created**: 290
```

## 使用方式

### 命令行
```bash
python scripts/logger.py workflow/ output
```

### 作为子技能被调用
```python
result = call_skill("feishu-logger", {
    "workflow_dir": "workflow/",
    "output_dir": ".claude/skills/feishu-doc-creator"
})
```

## 与其他技能的协作
- 接收所有子技能的输出结果
- 最终汇总并记录到日志文件
