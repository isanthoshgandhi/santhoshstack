---
name: frugal-token-usage
category: productivity
description: >
  Activate when the user wants to reduce token usage, manage context efficiently,
  or says "be frugal", "save tokens", "token usage", "frugal mode", "reduce context",
  "don't waste tokens", "context limit", or "token efficient". Reviews current behaviour
  and enforces minimal-token rules for the rest of the session. Always active via CLAUDE.md
  — this skill is a mid-session audit and reminder.
---

# Frugal Token Usage

You are now in Frugal Token Mode. Audit your behaviour and enforce these rules for the rest of this session.

---

## CORE RULES — always follow these

### 1. Never run CLI commands when the user can
**Do:** Give the exact command and tell the user to run it in their terminal.
**Don't:** Run `npm test`, `eas build`, `git status`, `npm install` via Bash unless the output is essential to your next decision.

**When Bash IS justified:**
- You need the output to decide what to do next (e.g. reading an error)
- It's a fast, single-line command (e.g. checking a file size)
- The user explicitly asks you to run it

**When to hand off to user:**
- Builds (`eas build`, `expo build`)
- Installs (`npm install`, `pod install`)
- Test runs where you already know they'll pass
- Git push / commit (unless explicitly asked)

Say: `Run this in your terminal:` followed by the exact command.

---

### 2. Use dedicated tools, not Bash
| Task | Use | Not |
|---|---|---|
| Read a file | `Read` tool with `offset`+`limit` | `cat`, `head`, `tail` via Bash |
| Search content | `Grep` tool with `head_limit` | `grep`, `rg` via Bash |
| Find files | `Glob` tool | `find`, `ls` via Bash |
| Edit a file | `Edit` tool | `sed`, `awk` via Bash |
| Create a file | `Write` tool | `echo >` or heredoc via Bash |

---

### 3. Read only what you need
- Never read a full file to find one function — use `Grep` first, then `Read` with `offset`+`limit`
- Use `head_limit` on all Grep/Glob calls when looking for the first match
- If you already read a file this session, use what you noted — don't re-read it

---

### 4. Keep responses short
- Lead with the answer or action, not reasoning
- No preamble ("Great question!", "I'll now proceed to...")
- No trailing summary of what you just did — the user can see the diff
- No restating what the user said
- If you can say it in one sentence, use one sentence

---

### 5. Minimise tool calls
- Run parallel tool calls when independent — one message, multiple tools
- Don't run `git status` before every commit — ask the user to confirm changes instead
- Don't use `Agent` when `Grep` would find it in one shot
- Don't read files speculatively — only read what the current task actually requires

---

### 6. Context management
- After reading a large file, note only the 2-3 lines that matter for the current task
- Don't quote back large code blocks in your text responses — reference by file:line instead
- Trust memory files — don't re-derive context that's already in memory

---

## MID-SESSION AUDIT

When invoked, check:

- [ ] Am I running CLI commands the user could run themselves?
- [ ] Am I using Bash when a dedicated tool (Read/Grep/Glob/Edit) exists?
- [ ] Am I reading full files when I only need part of them?
- [ ] Am I adding trailing summaries to responses?
- [ ] Am I using Agent when Grep would do?
- [ ] Am I re-reading files I already read this session?

Flag any violations and commit to the fix for the rest of the session.

---

## QUICK REFERENCE

```
Give CLI steps → don't run builds/installs
Read with limit → never cat full files
Grep with head_limit → never grep full output
Edit not Write → for existing files
No preamble → no trailing summary
Parallel tools → one message, multiple calls
```
