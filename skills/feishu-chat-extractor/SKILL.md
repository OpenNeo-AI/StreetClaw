---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 3045022100b356a6789e261f63d5080dd0c5d7dd82323fa90ae96408843b01cca30d0c90f2022064aa12ff9af268082122255b3b0760302610d2c2e042377d732f5c2f552ff93e
    ReservedCode2: 304502202c00a687851af3fbe67ce8fc7e216918c80cd755bfbfeecb16bb5aa753c71981022100de27ea4965b49551b8e34e1ce4ba82ce1e1653dbf556cb0a4b75a9dfa0e8cb14
description: Extract and analyze historical chat messages from Feishu/Lark groups. Use when needing to retrieve, process, or analyze group chat history, especially for OpenClaw/Clawdbot discussions. Handles pagination, time range filtering, and content extraction.
name: feishu-chat-extractor
---

# Feishu Chat Extractor

Extract and analyze historical messages from Feishu group chats.

## When to Use This Skill

- Extract full chat history from a Feishu group
- Filter messages by time range
- Extract OpenClaw/Clawdbot-related discussions
- Analyze user feedback and issues
- Generate reports from chat data

## Quick Start

### 1. Get Chat ID

```python
# Use existing chat_id or get from group
CHAT_ID = "oc_b05242fd39d405d022fccab873d7df1b"  # Example
```

### 2. Extract Messages

```bash
# Run extraction script
python3 scripts/extract_chat.py --chat-id <CHAT_ID> --output chat_data.json
```

### 3. Analyze Content

```bash
# Extract OpenClaw-related messages
python3 scripts/analyze_content.py --input chat_data.json --keywords openclaw,clawdbot,cron,mcp
```

## Core Workflow

### Step 1: Plan (P)

1. Identify target group and time range
2. Determine extraction scope (all messages or filtered)
3. Define analysis criteria (keywords, topics)

### Step 2: Do (D)

1. Run extraction script with appropriate parameters
2. Handle pagination for large message volumes
3. Save raw data to workspace

### Step 3: Check (C)

1. Verify message count matches expected
2. Check time range coverage
3. Validate data completeness
4. Review sample messages for quality

### Step 4: Act (A)

1. Re-extract if data incomplete
2. Filter and categorize messages
3. Generate structured report
4. Update documentation

## Key Techniques

### Time Range Extraction (Critical)

**Problem**: Default pagination may miss messages due to retention policies.

**Solution**: Use `start_time` and `end_time` parameters:

```python
params = {
    "container_id": chat_id,
    "container_id_type": "chat",
    "start_time": 1700000000,  # Unix timestamp (seconds)
    "end_time": 1700100000,
    "page_size": 50
}
```

This ensures complete message retrieval across any time span.

### Pagination Handling

```python
all_messages = []
page_token = None

while True:
    params["page_token"] = page_token
    result = fetch_messages(params)
    all_messages.extend(result["items"])
    
    if not result["has_more"]:
        break
    page_token = result["page_token"]
```

### Content Filtering

Filter by message type:
- `text` - Text messages
- `post` - Rich text posts
- `image` - Images
- `vote` - Polls

## Scripts

### extract_chat.py

Main extraction script. See `scripts/extract_chat.py` for full implementation.

Key features:
- Automatic pagination
- Time range filtering
- Progress logging
- Error retry logic

### analyze_content.py

Content analysis script. See `scripts/analyze_content.py` for full implementation.

Key features:
- Keyword extraction
- Topic categorization
- Report generation

## API Reference

### Get Chat History

```
GET https://open.feishu.cn/open-apis/im/v1/messages
```

Parameters:
- `container_id` (required): Chat ID
- `container_id_type`: "chat"
- `start_time`: Start timestamp (seconds)
- `end_time`: End timestamp (seconds)
- `page_size`: 1-50 (default 50)
- `page_token`: For pagination

### Common Error Codes

- `232006`: Invalid chat_id
- `232011`: Not in group
- `232025`: Bot capability not enabled

## Best Practices

1. **Always use time ranges** for complete extraction
2. **Check has_more** and paginate properly
3. **Save intermediate results** to avoid re-extraction
4. **Validate data** before analysis
5. **Document extraction parameters** for reproducibility

## Output Format

```json
{
  "chat_id": "oc_xxx",
  "extraction_time": "2026-02-06T17:00:00Z",
  "total_messages": 953,
  "time_range": {
    "start": "2026-01-27",
    "end": "2026-02-06"
  },
  "messages": [
    {
      "message_id": "om_xxx",
      "create_time": 1769500000000,
      "msg_type": "text",
      "content": "...",
      "sender": "..."
    }
  ]
}
```