---
name: context-manager
description: >
  Full project context setup and session management skill. Use this when starting
  a new project, onboarding onto an existing codebase, resuming work after a session
  gap, ending a session and wanting to save progress, or when context is running low
  mid-session. Sets up a docs/context/ system that any AI tool can read (Claude,
  Codex, Cursor, Windsurf). Three modes: SETUP (first time), RESUME (session start),
  UPDATE (session end). Trigger on: "set up context", "resume project", "update context",
  "end session", "context manager", "save progress", "continue from where we left off",
  or when starting work on any large multi-domain project.
---

# Context Manager

Sets up and maintains a minimal, tool-agnostic context system so any AI tool can
resume any project without re-reading everything.

**Core principle:** Global rules + domain scoping + two files per domain.

**Two files per domain (non-negotiable):**
- `{domain}.md` — operational. Resume state, current status, next task, open bugs. Changes every session.
- `{domain}-ref.md` — reference. What exists, where it lives, how it works, why it's built this way. Changes only when architecture or decisions change.

**Three-layer architecture:**
```
Layer 3 — Knowledge     cross-project, distilled, long-lived  (~/.claude/knowledge/)
Layer 2 — Project       cross-session, time-aware             (docs/sessions/, docs/backlog/)
Layer 1 — Session       per-session context                   (docs/context/)
```

```
Layer 1 + 2 → {project-root}/docs/
Layer 3      → ~/.claude/knowledge/   (change to any persistent path — use it consistently)
```

---

## Step 1 — Detect mode

| Mode | When |
|---|---|
| **SETUP** | No `docs/context/` exists. First time on this project. |
| **RESUME** | Session starting. User wants to pick up where they left off. |
| **UPDATE** | Session ending, context running low, or saving progress. |

When ambiguous, ask: "Set up fresh, resume work, or save and wrap up?"

## Step 2 — Load mode file

After detecting mode, use Glob to find the mode file, then Read it and follow its instructions:

| Mode | File to load |
|---|---|
| SETUP | `**/context-manager/SETUP.md` |
| RESUME | `**/context-manager/RESUME.md` |
| UPDATE | `**/context-manager/UPDATE.md` |

Do not load all three. Load only the one that matches the detected mode.

---

## Context slicing rules (non-negotiable)

1. Never load full history
2. Load both domain files every session: `{domain}.md` + `{domain}-ref.md` (knowledge store = +1 on Cold resume only)
3. Prefer structured data over prose
4. Drop redundancy — if it's in the code, don't duplicate in context
5. Compress before adding — update existing files, don't append forever
6. pointers.md is the only file that routes — never bypass it
7. Session timing is mandatory — every entry must have start, end, duration
8. Distill before the log grows unreadable — trigger at 20 entries or 30 days
9. Knowledge store is read-only during RESUME — only written during UPDATE distillation
10. Always load the domain file — gap determines whether to also load sessions/knowledge store, not whether to load the domain file
11. {domain}-ref.md is a snapshot, not an accumulation — when a decision is superseded or a file path changes, replace it. Never append without pruning stale entries.
