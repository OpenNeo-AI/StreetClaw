---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 304502202706ff566066732df39585e122be52ebc5de90a20174d13225277c813744a362022100c44948263c68a7dae84e993e4c1e3f226235fa536909df05d8da371cdcf75a6d
    ReservedCode2: 3045022100d6c4dfeb78e78c8b2a2917e85c4c6bce8ec219299e0d56681529559c9d206c3402205ec897736575f7505875100f40f84c5644d00a9ca77f19a5891422503dcee78f
description: Summarize URLs or files with the summarize CLI (web, PDFs, images, audio, YouTube).
homepage: https://summarize.sh
metadata:
    clawdbot:
        emoji: "\U0001F9FE"
        install:
            - bins:
                - summarize
              formula: steipete/tap/summarize
              id: brew
              kind: brew
              label: Install summarize (brew)
        requires:
            bins:
                - summarize
name: summarize
---

# Summarize

Fast CLI to summarize URLs, local files, and YouTube links.

## Quick start

```bash
summarize "https://example.com" --model google/gemini-3-flash-preview
summarize "/path/to/file.pdf" --model google/gemini-3-flash-preview
summarize "https://youtu.be/dQw4w9WgXcQ" --youtube auto
```

## Model + keys

Set the API key for your chosen provider:
- OpenAI: `OPENAI_API_KEY`
- Anthropic: `ANTHROPIC_API_KEY`
- xAI: `XAI_API_KEY`
- Google: `GEMINI_API_KEY` (aliases: `GOOGLE_GENERATIVE_AI_API_KEY`, `GOOGLE_API_KEY`)

Default model is `google/gemini-3-flash-preview` if none is set.

## Useful flags

- `--length short|medium|long|xl|xxl|<chars>`
- `--max-output-tokens <count>`
- `--extract-only` (URLs only)
- `--json` (machine readable)
- `--firecrawl auto|off|always` (fallback extraction)
- `--youtube auto` (Apify fallback if `APIFY_API_TOKEN` set)

## Config

Optional config file: `~/.summarize/config.json`

```json
{ "model": "openai/gpt-5.2" }
```

Optional services:
- `FIRECRAWL_API_KEY` for blocked sites
- `APIFY_API_TOKEN` for YouTube fallback
