# FEATURE_REQUESTS.md — 虾逛功能需求日志

---

## [FEAT-20260319-001] tavily_mcp_config

**Logged**: 2026-03-19T10:20:00Z
**Priority**: high
**Status**: pending

### Requested Capability
tavily-search MCP 服务器配置，需要将 tavily MCP URL 注册到 OpenClaw MCP 管理器

### User Context
江哥提供 Tavily MCP URL：https://mcp.tavily.com/mcp/?tavilyApiKey=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
Tavily 是 AI 搜索工具，可用于深度研究

### Complexity Estimate
medium

### Suggested Implementation
通过 mcporter config add 命令添加 HTTP MCP 服务器，需先确保 mcporter 守护进程运行

### Metadata
- Frequency: first_time
- Related Features: agent-browser, tavily-search

---

## [FEAT-20260319-002] xiaohongshu_mcp

**Logged**: 2026-03-19T10:19:00Z
**Priority**: high
**Status**: pending

### Requested Capability
小红书 MCP 能力 —— 搜索小红书内容、提取笔记数据

### User Context
江哥需要完整的小红书能力，对虾逛来说可以提取小红书上的穿搭笔记、种草内容辅助购物参考

### Complexity Estimate
medium

### Suggested Implementation
从 GitHub 单独安装 xiaohongshu-mcp（不在 SkillHub）或搜索替代技能

### Metadata
- Frequency: first_time
- Related Features: content-extractor

---

## [FEAT-20260319-003] batch_skill_install_script

**Logged**: 2026-03-19T10:21:00Z
**Priority**: low
**Status**: pending

### Requested Capability
一键批量安装技能脚本，自动执行 skillhub install + 迁移到 /root/.openclaw/skills/

### User Context
江哥经常需要一次性安装多个技能，每次手动安装+迁移繁琐

### Complexity Estimate
simple

### Suggested Implementation
写一个 Shell 脚本：for skill in $@; do /root/.local/bin/skillhub install $skill && cp -r /workspace/skills/$skill /root/.openclaw/skills/; done

### Metadata
- Frequency: recurring
- Related Features: skillhub

---
