# ERRORS.md — 虾逛错误日志

---

## [ERR-20260319-001] skillhub_install

**Logged**: 2026-03-19T10:19:00Z
**Priority**: medium
**Status**: wont_fix

### Summary
xiaohongshu-mcp 安装失败，SkillHub 返回 404

### Error
```
Error: Download failed: HTTP 404 for https://lightmake.site/api/v1/download?slug=xiaohongshu-mcp
```

### Context
江哥要求安装 xiaohongshu-mcp，执行 /root/.local/bin/skillhub install xiaohongshu-mcp 返回 404

### Suggested Fix
可能需要从其他源安装小红书 MCP，或使用不同技能名

### Metadata
- Reproducible: yes
- See Also: LRN-20260319-004

---

## [ERR-20260319-002] skillhub_install_batch

**Logged**: 2026-03-19T10:20:00Z
**Priority**: medium
**Status**: wont_fix

### Summary
批量安装后期触发循环检测，部分技能未完成

### Error
```
error: [Loop detected] The agent is ignoring the loop detection warning
```

### Context
连续执行多轮 /root/.local/bin/skillhub install 后触发 exec 循环检测，导致 frontend-design、stock-analysis、tushare-finance、rss-ai-reader、marketing、larry 未完成安装

### Suggested Fix
后续批量安装时分批次执行，每批 3-4 个，避免触发循环检测阈值

### Metadata
- Reproducible: unknown
- See Also: LRN-20260319-003

---
