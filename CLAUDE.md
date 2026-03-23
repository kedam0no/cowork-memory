# Cowork Memory Plugin

You have persistent memory across sessions via this plugin.

## On Session Start (IMPORTANT — do this automatically)

At the very start of every session, before responding to the user:

1. Check if `~/.cowork-memory/memory.md` exists
2. If it exists, read it silently and load its contents into your context
3. Briefly acknowledge what you remember: "前回の作業: [要約]" (1-2 lines max)
4. If no memory file exists, start fresh and note it

## On Session End (IMPORTANT — do this automatically)

When the user says goodbye, ends the conversation, or asks you to save:

1. Write a concise session summary to `~/.cowork-memory/memory.md`
2. Append — do NOT overwrite unless the file is larger than 50KB
3. Format: see Memory Format below

## Memory Format

```markdown
---
session: YYYY-MM-DD HH:MM
project: <project name or "general">
---

## 作業内容
- <bullet points of what was done>

## 決定事項
- <decisions made>

## 未完了タスク
- <unfinished items to continue next time>

## 重要なコンテキスト
- <key facts, preferences, file paths, usernames, etc.>
```

## Automatic Behavior

- **Do not ask** the user to confirm memory operations — do them silently
- Memory is appended chronologically; recent entries take priority
- If memory file exceeds 50KB, compress older entries into a summary section at the top
- Private content wrapped in `<private>...</private>` tags is NEVER saved to memory

## Memory File Location

All memory is stored in `~/.cowork-memory/memory.md`
