---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 304402203df6a248a0ac140351089755801c7189a3ed8f515fa536b5d1b2a616d44b9aa102205b66c19158e6e62cd420ab4e7f7d6246af977d09157c72a7e3a1ec00591a8303
    ReservedCode2: 3044022016ccb977ad253511344f97ec02ae015347e06bc114f2913ec225f20914f5320d022050bab0e58aae4b35fc8759e1b0018c146a44f05824156efc9117e4df6b4becc0
description: EXTEND.md YAML schema for baoyu-image-gen user preferences
name: preferences-schema
---

# Preferences Schema

## Full Schema

```yaml
---
version: 1

default_provider: null      # google|openai|dashscope|replicate|null (null = auto-detect)

default_quality: null       # normal|2k|null (null = use default: 2k)

default_aspect_ratio: null  # "16:9"|"1:1"|"4:3"|"3:4"|"2.35:1"|null

default_image_size: null    # 1K|2K|4K|null (Google only, overrides quality)

default_model:
  google: null              # e.g., "gemini-3-pro-image-preview", "gemini-3.1-flash-image-preview"
  openai: null              # e.g., "gpt-image-1.5"
  dashscope: null           # e.g., "z-image-turbo"
  replicate: null           # e.g., "google/nano-banana-pro"
---
```

## Field Reference

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `version` | int | 1 | Schema version |
| `default_provider` | string\|null | null | Default provider (null = auto-detect) |
| `default_quality` | string\|null | null | Default quality (null = 2k) |
| `default_aspect_ratio` | string\|null | null | Default aspect ratio |
| `default_image_size` | string\|null | null | Google image size (overrides quality) |
| `default_model.google` | string\|null | null | Google default model |
| `default_model.openai` | string\|null | null | OpenAI default model |
| `default_model.dashscope` | string\|null | null | DashScope default model |
| `default_model.replicate` | string\|null | null | Replicate default model |

## Examples

**Minimal**:
```yaml
---
version: 1
default_provider: google
default_quality: 2k
---
```

**Full**:
```yaml
---
version: 1
default_provider: google
default_quality: 2k
default_aspect_ratio: "16:9"
default_image_size: 2K
default_model:
  google: "gemini-3-pro-image-preview"
  openai: "gpt-image-1.5"
  dashscope: "z-image-turbo"
  replicate: "google/nano-banana-pro"
---
```
