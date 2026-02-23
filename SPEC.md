# Quill — Spec

## Problem

Existing AI plugins for Obsidian break the writing flow. You prompt in a separate panel, wait, then manually copy the result back into your note. On top of that, the AI has no knowledge of your vault — no linked notes, no metadata, no context beyond what you explicitly paste in.

## Solution

An Obsidian plugin that brings AI inline:

- **Command palette first** — trigger any AI action without leaving the editor
- **Vault-aware context** — every request automatically includes the current note, linked notes, frontmatter, and a custom system prompt
- **OpenRouter** — access to hundreds of models via a single API key; more providers later

## Core flows

| Trigger | Action | Result |
|---------|--------|--------|
| Select text → command | Transform (rephrase, shorten, expand, translate, improve style) | Selection replaced |
| Cursor in note → command | Generate (continue, summarize, suggest headings) | Inserted at cursor |
| Command → type question | Ask anything about the current note | Inserted as a block |

Streaming is required — output appears as it's generated. Escape cancels.

## Context sent to AI

```
[user system prompt]
[note metadata: frontmatter, tags, path]
[current note]
[linked notes — headings + first ~200 words each]
[user request]
```

Users can configure context depth (disable linked notes, set token limits).

## Out of scope for v1

- Chat sidebar or conversation history
- Full-vault indexing / RAG
- Automatic triggers
