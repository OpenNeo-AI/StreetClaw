---
AIGC:
    ContentProducer: Minimax Agent AI
    ContentPropagator: Minimax Agent AI
    Label: AIGC
    ProduceID: "00000000000000000000000000000000"
    PropagateID: "00000000000000000000000000000000"
    ReservedCode1: 304502202cc007b7449d413f93528d8267a7c04a88af6598ec99700e5f1c0636460c76f3022100d4ac71f411b06b45bcc33cbd8d1088481570ae53a23b7adb90bbc4ac900070c1
    ReservedCode2: 304502200d8a2fcce1e3043b9f3ce1f5743917b68ff8a93f7c72faf4978abcabadfbb951022100b2732c96b841afd7946fdb74de95a61ca50c85baca5fe73cf4adfa4ff0dd5e6b
---

# Humanizer

A Clawdbot skill that removes signs of AI-generated writing from text, making it sound more natural and human.

## Installation

Install via ClawdHub:

```bash
clawdhub install humanizer
```

## Usage

Ask your agent to humanize text:

```
Please humanize this text: [your text]
```

Or invoke directly when editing documents.

## Overview

Based on [Wikipedia's "Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing) guide, maintained by WikiProject AI Cleanup. This comprehensive guide comes from observations of thousands of instances of AI-generated text.

### Key Insight

> "LLMs use statistical algorithms to guess what should come next. The result tends toward the most statistically likely result that applies to the widest variety of cases."

## 24 Patterns Detected

### Content Patterns
1. **Significance inflation** - "marking a pivotal moment..." → specific facts
2. **Notability name-dropping** - listing sources without context
3. **Superficial -ing analyses** - "symbolizing... reflecting..."
4. **Promotional language** - "nestled within the breathtaking..."
5. **Vague attributions** - "Experts believe..."
6. **Formulaic challenges** - "Despite challenges... continues to thrive"

### Language Patterns
7. **AI vocabulary** - "Additionally... testament... landscape..."
8. **Copula avoidance** - "serves as" instead of "is"
9. **Negative parallelisms** - "It's not just X, it's Y"
10. **Rule of three** - forcing ideas into groups of three
11. **Synonym cycling** - excessive synonym substitution
12. **False ranges** - "from X to Y" on non-meaningful scales

### Style Patterns
13. **Em dash overuse**
14. **Boldface overuse**
15. **Inline-header lists**
16. **Title Case Headings**
17. **Emoji decoration**
18. **Curly quotation marks**

### Communication Patterns
19. **Chatbot artifacts** - "I hope this helps!"
20. **Cutoff disclaimers** - "While details are limited..."
21. **Sycophantic tone** - "Great question!"

### Filler and Hedging
22. **Filler phrases** - "In order to", "Due to the fact that"
23. **Excessive hedging** - "could potentially possibly"
24. **Generic conclusions** - "The future looks bright"

## Full Example

**Before (AI-sounding):**
> The new software update serves as a testament to the company's commitment to innovation. Moreover, it provides a seamless, intuitive, and powerful user experience—ensuring that users can accomplish their goals efficiently.

**After (Humanized):**
> The software update adds batch processing, keyboard shortcuts, and offline mode. Early feedback from beta testers has been positive, with most reporting faster task completion.

## References

- [Wikipedia: Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing)
- [WikiProject AI Cleanup](https://en.wikipedia.org/wiki/Wikipedia:WikiProject_AI_Cleanup)

## License

MIT
