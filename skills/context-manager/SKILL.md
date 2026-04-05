---
name: context-manager
description: >
  Full project context setup and session management skill. Use this when starting
  a new project, onboarding onto an existing codebase, resuming work after a session
  gap, ending a session and wanting to save progress, or when context is running low
  mid-session. Sets up a docs/context/ system that any AI tool can read (Claude,
  Codex, Cursor, Windsurf, Antigravity). Three modes: SETUP (first time), RESUME
  (session start), UPDATE (session end). Trigger on: "set up context", "resume project",
  "update context", "end session", "context manager", "save progress", "continue from
  where we left off", or when starting work on any large multi-domain project.
---

# Context Manager

Sets up and maintains a minimal, tool-agnostic context system so any AI tool can
resume any project without re-reading everything.

**Core principle:** You avoid large context by designing a system that only uses
small context at any time. Global rules + domain scoping + minimal context per task.

---

## Detect mode first

Ask or infer from conversation:

| Mode | When |
|---|---|
| **SETUP** | No `docs/context/` exists. First time on this project. |
| **RESUME** | Session starting. User wants to pick up where they left off. |
| **UPDATE** | Session ending, context running low, or user wants to save progress. |

When ambiguous, ask: "Set up fresh, resume work, or save and wrap up?"

---

## SETUP mode — Build the context system from scratch

Use this when the project has no `docs/context/` folder yet.
This is what we build — not a chatbot wrapper, a file-based system any tool can read.

### Step 1 — Audit the project

Read the project root. Look for:
- Existing docs (README, CONTEXT.md, CHANGELOG, any markdown)
- Code structure (what are the main concerns — frontend, backend, crawler, API, etc.)
- Git history (`git log --oneline -20`) — what has been worked on recently
- Any existing notes, backlogs, or decision records

Ask the user: "What are the main domains of work in this project?"
Examples: corpus/ingestion, product/UI, schema/database, algorithm/ranking, frontend, backend

### Step 2 — Design the structure (fit the project, don't impose)

Every project is different. The structure should emerge from the project's actual shape,
not be forced onto it. Ask yourself:

- How many distinct concerns does this project have? (1 → flat; 5+ → subfolders)
- Does it have operational logs worth keeping? (long-running → yes; small script → no)
- Is there a backlog worth tracking? (active development → yes; maintenance → maybe not)
- Is there research or reference material? (data-heavy → yes; CRUD app → probably not)
- Will multiple people or tools work on it? (yes → more structure; solo → less)

**The only fixed requirement across all projects:**

```
{project-root}/
└── docs/
    └── context/
        └── pointers.md        ← the single entry point, always
```

Everything else is optional and scales with project complexity.

**Small project (1–2 domains, solo, short-lived):**
```
docs/
└── context/
    ├── pointers.md
    └── main.md               ← single context file is fine
```

**Medium project (2–4 domains, active development):**
```
docs/
├── context/
│   ├── pointers.md
│   ├── {domain-1}.md
│   └── {domain-2}.md
└── backlog/
    └── BACKLOG.md
```

**Large project (multiple domains, long-running, multi-tool):**
```
{project-root}/
├── CONTEXT.md                 ← master map at root (only needed when many subfolders exist)
└── docs/
    ├── context/               ← session bootstrap (always)
    │   ├── pointers.md
    │   └── {domain}.md per domain
    ├── sessions/              ← append-only run logs
    ├── changelog/             ← one merged changelog
    ├── backlog/               ← cross-domain pending work
    ├── {domain}/              ← deep technical docs (not loaded by default)
    ├── feedback/              ← audit notes from any AI tool or human reviewer
    │                            (ask Codex, Cursor, Antigravity to audit → save here)
    └── research/              ← deep reference (load only when asked)
```

**Fit the structure to reality, not the other way around.**
If a folder has no content yet, don't create it. Add structure when you need it.
The goal is to reduce cognitive load, not add ceremony.

### Step 3 — Write pointers.md

This is the single entry point for every session and every AI tool.

```markdown
# [Project Name] — Session Pointers

> Read this file FIRST on every session.
> Pick your domain. Load ONLY the 2–3 files listed. Never load everything.

## QUICK RESUME
Last session: {date}
Where we left off: {1–2 sentences}
Next action: {specific next step}

---

## Domain: {domain-1}
*{what work this domain covers}*

Load:
1. `docs/context/{domain-1}.md` — current state, next tasks
2. `docs/backlog/BACKLOG.md` — pending work (skim relevant section only)

Skip: all other domain files, sessions history, changelog

---

## Domain: {domain-2}
...

---

## What NOT to load
| File | Why skip |
|---|---|
| `docs/sessions/SESSIONS.md` | Historical logs — only if debugging a specific past run |
| `docs/changelog/CHANGELOG.md` | Change history — only if asked |
| `docs/research/` | Deep reference — load only if asked |
```

### Step 4 — Write domain context files

One file per domain at `docs/context/{domain}.md`.

Each file must have this structure:

```markdown
# {Domain} Context — Current State

> Domain: {domain}
> Updated: {date}
> READ THIS FIRST — contains full resume state

---

## RESUME FROM HERE
Last session: {date}
What was done: {bullet points}
Current state: {one sentence — specific numbers/status}
Open bugs: {list with status}
Next action: {single most important next step — specific enough to act on}

---

## Current Status
{what exists, what's working, what's broken}

## Key File Paths
{the 5–10 files that matter most for this domain}

## Architecture / How It Works
{brief — enough to work without re-reading everything}

## Next Tasks (in order)
{numbered list}

## Known Issues / Open Questions
{anything unresolved}
```

### Step 5 — Create operational files

**`docs/sessions/SESSIONS.md`** — start with format template:
```markdown
# Sessions Log
> Append only. One entry per session.

## {YYYY-MM-DD} (Session 1)
**What was done:** {bullets}
**Issues hit:** {list}
**Next:** {next action}
```

**`docs/backlog/BACKLOG.md`** — organize by domain + priority:
```markdown
# Backlog
> Cross-domain. Add items from any session. Move to changelog when done.

## Priority: Next
{items}

## Domain: {name}
{items}

## Deferred
{items with reason}

## Decided: Do Not Do
{items with reason}
```

**`docs/changelog/CHANGELOG.md`** — one file, all changes:
```markdown
# Changelog
> All changes — product, system, pipeline. Most recent first.

## Unreleased
### {Domain}
- {change}

## {date}
{completed changes}
```

### Step 6 — Wire up memory

Update `~/.claude/projects/.../memory/` files to point to `docs/context/`:

For each existing memory file related to this project, replace the content with:
```markdown
---
name: {project} — {domain}
description: {one line}
type: project
---

## Source of truth
`docs/context/{domain}.md` — always read this, not this file.

## Quick reference
- Status: {current status}
- Next: {next action}
- Project root: {path}
```

Update `MEMORY.md` session bootstrap section:
```markdown
Any session working on {Project} must:
1. Read `docs/context/pointers.md` FIRST
2. Load ONLY the files listed for your domain
3. Do NOT load all memory files — they are stale pointers only
```

### Step 7 — Commit and tell the user

```bash
git add docs/context/ docs/sessions/ docs/changelog/ docs/backlog/
git commit -m "docs: add context management system"
git push
```

Tell the user:
> "Context system created. Start every future session with `/context-manager`.
> Other AI tools (Codex, Cursor, Windsurf) can read `docs/context/pointers.md`
> directly — point them at that file as the project entry point."

---

## RESUME mode — Load minimal context for session start

### Step 1 — Find and read pointers.md
Look for `docs/context/pointers.md`. Read only that file first.
Check the QUICK RESUME block — this alone may be enough for simple continuations.

### Step 2 — Match domain to user's task
- Crawling, scraping, pipeline, data → corpus/ingestion domain
- UI, tabs, product decisions, design → product domain
- Database, schema, import, search → schema/data domain
- Ranking, algorithm, intelligence → algorithm domain
- Unclear → load only the QUICK RESUME block, ask user to clarify

### Step 3 — Load 2–3 files only
Load exactly what pointers.md says for that domain. Nothing extra.
If a listed file doesn't exist, note it and continue.

### Step 4 — Show resume summary
```
Resuming: [domain] on [project]
Where we left off: [1–2 sentences from RESUME FROM HERE block]
Open issues: [any blockers]
Next action: [the specific next step]
```

Wait for user confirmation before starting work.

---

## UPDATE mode — Save progress at session end

### Step 1 — Detect what changed
Run `git diff HEAD` and scan the conversation for:
- Bugs found and fixed (with commit hashes)
- Decisions made
- Tasks completed / abandoned
- New open questions or blockers
- Current numbers/stats (rows scraped, tests passing, etc.)

### Step 2 — Update domain context file
Edit `docs/context/{domain}.md`. Surgical edits only — don't rewrite everything.

Always update the **RESUME FROM HERE** block at the top with today's date,
what was done, current state, open bugs, and next action.
Update any stale numbers elsewhere in the file.

### Step 3 — Update pointers.md QUICK RESUME block
Update the date, where we left off, and next action.

### Step 4 — Append to sessions log
Add entry to `docs/sessions/SESSIONS.md`.

### Step 5 — Add backlog items
For each finding or deferred item, add to `docs/backlog/BACKLOG.md`.
Do not duplicate existing items.

### Step 6 — Update memory pointer files
Keep memory files lean — 5–10 lines pointing to docs/context/.

### Step 7 — Commit and push
```bash
git add docs/context/ docs/sessions/ docs/backlog/
git commit -m "docs: context update {date} — {one line summary}"
git push
```

---

## Cross-tool compatibility

Context files are plain markdown in `docs/context/`. Any AI tool can read them:

| Tool | How to use |
|---|---|
| Claude Code | `/context-manager` at session start/end |
| Codex | Point at `docs/context/pointers.md` as project entry |
| Cursor | Add `docs/context/` to `.cursorrules` or Cursor context |
| Windsurf | Add `docs/context/pointers.md` to context window |
| Any tool | Read `pointers.md` → pick domain → load 2–3 files |

**Never put Claude-specific syntax in context files.** No memory frontmatter,
no tool directives — just plain markdown that any tool can parse.

---

## Context slicing rules (non-negotiable)

1. Never load full history
2. Max 2–3 files per session
3. Prefer structured data over prose
4. Drop redundancy — if it's in the code, don't duplicate in context
5. Compress before adding — update existing files, don't append forever
6. pointers.md is the only file that routes — never bypass it
