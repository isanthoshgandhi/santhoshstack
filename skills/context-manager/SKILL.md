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

**Core principle:** You avoid large context by designing a system that only uses
small context at any time. Global rules + domain scoping + minimal context per task.

**Three-layer architecture:**
```
Layer 3 — Knowledge     cross-project, distilled, long-lived  (~/.claude/knowledge/)
Layer 2 — Project       cross-session, time-aware             (docs/sessions/, docs/backlog/)
Layer 1 — Session       per-session context                   (docs/context/)
```

Each layer builds on the one below. Don't skip ahead.

**Storage roots:**
```
Layer 1 + 2 → {project-root}/docs/        ← inside each repo
Layer 3      → ~/.claude/knowledge/        ← outside repos, persistent across all projects
```

> `~` resolves to your home directory on all platforms (Mac/Linux: `/home/{user}`, Windows: `C:\Users\{user}`).
> You can change the Layer 3 path to any persistent location you prefer — just use it consistently.

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

### Step 1 — Audit the project

Read the project root. Look for:
- Existing docs (README, CONTEXT.md, CHANGELOG, any markdown)
- Code structure (main concerns — frontend, backend, crawler, API, etc.)
- Git history (`git log --oneline -20`) — what has been worked on recently
- Any existing notes, backlogs, or decision records

Ask the user: "What are the main domains of work in this project?"
Examples: corpus/ingestion, product/UI, schema/database, algorithm/ranking, frontend, backend

### Step 2 — Design the structure (fit the project, don't impose)

Every project is different. Ask yourself:

- How many distinct concerns? (1 → flat; 5+ → subfolders)
- Does it have operational logs worth keeping? (long-running → yes; small script → no)
- Is there a backlog worth tracking? (active development → yes; maintenance → maybe not)
- Will multiple tools work on it? (yes → more structure; solo → less)

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
    └── main.md
```

**Medium project (2–4 domains, active development):**
```
docs/
├── context/
│   ├── pointers.md
│   ├── {domain-1}.md
│   └── {domain-2}.md
├── sessions/
│   └── SESSIONS.md
└── backlog/
    └── BACKLOG.md
```

**Large project (multiple domains, long-running, multi-tool):**
```
{project-root}/
└── docs/
    ├── context/               ← session bootstrap (always)
    │   ├── pointers.md
    │   └── {domain}.md per domain
    ├── sessions/              ← append-only run logs with timing
    ├── changelog/             ← one merged changelog
    ├── backlog/               ← cross-domain pending work
    ├── {domain}/              ← deep technical docs (not loaded by default)
    └── research/              ← deep reference (load only when asked)
```

**Fit the structure to reality, not the other way around.**
If a folder has no content, don't create it. Add structure when you need it.

### Step 3 — Write pointers.md

Single entry point for every session and every AI tool.

```markdown
# [Project Name] — Session Pointers

> Read this file FIRST on every session.
> Pick your domain. Load ONLY the 2–3 files listed. Never load everything.

## QUICK RESUME
Last session: N/A — first session
Gap since last session: N/A
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
| `~/.claude/knowledge/` | Long-term store — only if gap > 60 days |
```

### Step 4 — Write domain context files

One file per domain at `docs/context/{domain}.md`.

```markdown
# {Domain} Context — Current State

> Domain: {domain}
> Updated: {YYYY-MM-DD HH:MM}
> Staleness threshold: 14 days
> READ THIS FIRST — contains full resume state

---

## RESUME FROM HERE
Last session: {YYYY-MM-DD HH:MM}
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

**`docs/sessions/SESSIONS.md`** — with timing:
```markdown
# Sessions Log
> Append only. One entry per session. Include timing always.

## {YYYY-MM-DD} Session {N}
**Start:** {HH:MM}
**End:** {HH:MM}
**Duration:** {Xh Ym}
**Gap since last session:** {X days / first session}
**Domain:** {domain}
**What was done:** {bullets}
**Issues hit:** {list}
**Decisions made:** {list}
**Next:** {next action}
```

**`docs/backlog/BACKLOG.md`:**
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

**`docs/changelog/CHANGELOG.md`:**
```markdown
# Changelog
> All changes. Most recent first.

## Unreleased
### {Domain}
- {change}

## {YYYY-MM-DD}
{completed changes}
```

### Step 6 — Bootstrap the knowledge store

Check if `~/.claude/knowledge/` exists. If not, create it now — this is Layer 3 and must exist before any project uses distillation or Cold resume. Do not skip this step.

> You can use any persistent path outside your repos. `~/.claude/knowledge/` is the default.
> If you prefer a dedicated workspace folder, use that consistently and update the paths
> in pointers.md and the RESUME/UPDATE steps below.

```
~/.claude/knowledge/
├── index.md                   ← global index of all projects + learnings
├── patterns.md                ← recurring patterns across projects
├── global-backlog.md          ← cross-project backlog
└── projects/
    └── {project-slug}/
        └── learnings.md       ← distilled from SESSIONS.md (created on first distillation)
```

**`~/.claude/knowledge/index.md`:**
```markdown
# Knowledge Index

> Cross-project learnings. Updated by context-manager on distillation.
> Never load in full — pick relevant project or pattern only.

## Projects
| Project | Slug | Last distilled | Root |
|---|---|---|---|
| {name} | {slug} | {date} | {path} |

## Top patterns (load patterns.md for full list)
- {pattern 1}
- {pattern 2}
```

**`~/.claude/knowledge/patterns.md`:**
```markdown
# Cross-Project Patterns

> Recurring issues, solutions, and decisions across all projects.
> Add during distillation. Weight by recency — recent entries matter more.

## Pattern: {name}
**Seen in:** {project list}
**Last seen:** {date}
**Context:** {what triggers this}
**Solution:** {what worked}
**Anti-pattern:** {what didn't work}
```

**`~/.claude/knowledge/global-backlog.md`:**
```markdown
# Global Backlog

> Cross-project items. Link to project backlog for details.

## Active
| Item | Project | Added | Priority |
|---|---|---|---|

## Deferred
| Item | Project | Reason |
|---|---|---|
```

### Step 7 — Wire up memory

Update `~/.claude/projects/.../memory/` files:

```markdown
## Source of truth
`docs/context/{domain}.md` — always read this, not this file.

## Quick reference
- Status: {current status}
- Next: {next action}
- Project root: {path}
- Knowledge store: `~/.claude/knowledge/projects/{slug}/learnings.md`
```

Update `MEMORY.md` session bootstrap:
```markdown
Any session working on {Project} must:
1. Read `docs/context/pointers.md` FIRST
2. Load ONLY the files listed for your domain
3. Do NOT load all memory files — they are stale pointers only
4. Gap > 60 days → also load `~/.claude/knowledge/projects/{slug}/learnings.md`
```

### Step 8 — Wire up cross-tool config

**Cursor** — create `.cursor/rules/context.md` at project root (legacy: `.cursorrules`):
```
Context entry point: docs/context/pointers.md
Load this file first. Pick your domain. Load only 2-3 files listed.
Never load docs/sessions/ or docs/research/ unless explicitly asked.
```
> Cursor moved from `.cursorrules` to `.cursor/rules/*.md` — check current Cursor docs for your version.

**Windsurf** — create `.windsurf/rules/context.md` at project root (legacy: `.windsurfcontext`):
```
entry: docs/context/pointers.md
```
> Windsurf moved from `.windsurfcontext` to `.windsurf/rules/` — check current Windsurf docs for your version.

**Codex / any other tool** — add to project README under a `## For AI Tools` section:
```markdown
## For AI Tools
Read `docs/context/pointers.md` first. Pick your domain. Load only what it lists.
```

### Step 9 — Commit

```bash
git add docs/context/ docs/sessions/ docs/changelog/ docs/backlog/ .cursorrules .windsurfcontext .cursor/ .windsurf/
git commit -m "docs: add context management system"
git push
```

Tell the user:
> "Context system created. Start every future session with `/context-manager`.
> Cross-tool config written. Knowledge store at `~/.claude/knowledge/`."

---

## RESUME mode — Load minimal context for session start

### Step 1 — Find pointers.md (with fallback)

Look for `docs/context/pointers.md`.

**If it doesn't exist:**
- Check for `CONTEXT.md` at project root — may be old format
- Check for any `.md` in `docs/context/` — load whatever exists
- If nothing found: tell the user "No context system found. Run SETUP mode first, or point me at your context files."
- Do NOT proceed blind

**If it exists:** read it.

### Step 2 — Calculate gap and set resume depth

From the `Last session` timestamp in QUICK RESUME, calculate gap to today.
If no time component (date only), treat as 00:00 for gap calculation. If no timestamp exists (old format), treat as Normal depth.

| Gap | Resume depth | What to load |
|---|---|---|
| < 14 days | Normal | QUICK RESUME + domain context file |
| 14–60 days | Deep | QUICK RESUME + domain file + skim last 3 sessions |
| > 60 days | Cold | Deep resume + check knowledge store + flag for distillation |

**Always load the domain file — regardless of gap.** QUICK RESUME alone is never sufficient for hands-on work. It lacks critical non-obvious facts (source of truth files, dropped services, tooling constraints) that live in the domain file. Loading only QUICK RESUME has caused repeated mistakes in the same session.

### Step 3 — Check domain file staleness

Read the `Updated:` timestamp from the domain context file.
If it's older than 14 days, warn: "Domain file last updated {X} days ago — may be stale. Verify current state before acting."

### Step 4 — Match domain to user's task

- Crawling, scraping, pipeline, data → corpus/ingestion domain
- UI, tabs, product decisions, design → product domain
- Database, schema, import, search → schema/data domain
- Ranking, algorithm, intelligence → algorithm domain
- Unclear → load QUICK RESUME + pointers.md, ask user to clarify domain before loading any domain file

### Step 5 — Load files per depth

Load exactly what the depth table says. Nothing extra.
If a listed file doesn't exist, note it and continue.

For Cold resume: also read `~/.claude/knowledge/projects/{slug}/learnings.md` if it exists.
Surface any patterns from `~/.claude/knowledge/patterns.md` relevant to the current domain.

### Step 6 — Show resume summary

```
Resuming: [domain] on [project]
Gap: [X days since last session]
Resume depth: [Normal / Deep / Cold]
Where we left off: [1–2 sentences]
Staleness warning: [if applicable]
Relevant past patterns: [if Cold resume and patterns found]
Next action: [the specific next step]
```

Wait for user confirmation before starting work.

---

## UPDATE mode — Save progress at session end

### Step 1 — Record session end time

Note the current time. Calculate duration from session start (ask user if start time unknown).

### Step 2 — Detect what changed

Run `git log --oneline -5` to see what was committed this session, then `git show --stat HEAD` for the most recent commit's file summary. Do not use `git diff HEAD` — on a clean workspace after commits it returns nothing.
Scan the conversation for:
- Bugs found and fixed (with commit hashes)
- Decisions made
- Tasks completed / abandoned
- New open questions or blockers
- Current numbers/stats

**Handling large changesets:** if `git show --stat HEAD` shows >50 files, read only files relevant to the current domain.

### Step 3 — Update domain context file

Edit `docs/context/{domain}.md`. Surgical edits only.

Always update:
- `Updated:` timestamp at top
- `RESUME FROM HERE` block — date, what was done, current state, open bugs, next action
- Any stale numbers elsewhere in the file

### Step 4 — Update pointers.md QUICK RESUME block

Update: date+time, where we left off, next action.

### Step 5 — Append to sessions log

Add entry to `docs/sessions/SESSIONS.md` with full timing:

```markdown
## {YYYY-MM-DD} Session {N}
**Start:** {HH:MM}
**End:** {HH:MM}
**Duration:** {Xh Ym}
**Gap since last session:** {X days}
**Domain:** {domain}
**What was done:** {bullets}
**Issues hit:** {list}
**Decisions made:** {list}
**Next:** {next action}
```

### Step 6 — Add backlog items

For each deferred item or open question, add to `docs/backlog/BACKLOG.md`.
Do not duplicate existing items.
If item is cross-project relevant, also add to `~/.claude/knowledge/global-backlog.md`.

### Step 7 — Check distillation trigger

Count session entries: `grep -c "^## " docs/sessions/SESSIONS.md`.
Calculate gap since last distillation (check `~/.claude/knowledge/projects/{slug}/learnings.md` header).

**Trigger distillation if ANY of:**
- Sessions log has > 20 entries since last distillation
- Gap since last distillation > 30 days
- This is a Cold resume (gap > 60 days)

If triggered, run distillation (Step 8). Otherwise skip to Step 9.

### Step 8 — Distillation (when triggered)

Read all sessions since last distillation from `SESSIONS.md`.
Do NOT read old sessions — only new ones since last distillation date.

Extract:
- Recurring issues (same problem appeared 2+ times → pattern)
- Key decisions with rationale
- Resolved bugs (title + fix approach, no code)
- What was deferred and why
- Velocity signal (avg session duration, cadence)

Prioritize by recency: patterns recurring in the last 7 days → extract first. One-off items older than 6 months → skip unless still marked open.

Write / update `~/.claude/knowledge/projects/{slug}/learnings.md`:

```markdown
# {Project} — Distilled Learnings

> Last distilled: {YYYY-MM-DD}
> Sessions covered: {N} sessions from {start-date} to {end-date}
> Velocity: avg {X} min/session, {Y} sessions/month

## Key Decisions
- {decision} — {rationale} ({date})

## Recurring Patterns
- {pattern} — seen {N} times, last {date}

## Resolved Issues
- {issue} — fixed by {approach} ({date})

## Deferred Items
- {item} — reason: {why} ({date})

## Watch: Still open
- {issue still unresolved}
```

Update `~/.claude/knowledge/patterns.md` — add or update any patterns that appeared 2+ times.
Update `~/.claude/knowledge/index.md` — update last distilled date for this project.

### Step 9 — Update memory pointer files

Keep memory files lean — 5–10 lines pointing to docs/context/.

### Step 10 — Commit and push

```bash
git add docs/context/ docs/sessions/ docs/backlog/ docs/changelog/
git commit -m "docs: context update {date} — {one line summary}"
git push
```

---

## Cross-tool compatibility

Context files are plain markdown in `docs/context/`. Any AI tool can read them.

**Claude Code:** `/context-manager` at session start/end.

**Cursor:**
- `.cursor/rules/context.md` at project root (written by SETUP) routes to `docs/context/pointers.md`
- Legacy: `.cursorrules` — still works on older versions

**Windsurf:**
- `.windsurf/rules/context.md` at project root (written by SETUP)
- Legacy: `.windsurfcontext`

**Codex:**
- Pass `docs/context/pointers.md` as the system context file
- Or reference it in your Codex project instructions

**Any tool:**
- Read `pointers.md` → pick domain → load 2–3 files
- Never load sessions/, research/, or knowledge store by default

**Never put Claude-specific syntax in context files.** No memory frontmatter,
no tool directives — just plain markdown that any tool can parse.

---

## Context slicing rules (non-negotiable)

1. Never load full history
2. Max 2–3 files per session (knowledge store = +1 file on Cold resume only)
3. Prefer structured data over prose
4. Drop redundancy — if it's in the code, don't duplicate in context
5. Compress before adding — update existing files, don't append forever
6. pointers.md is the only file that routes — never bypass it
7. Session timing is mandatory — every entry must have start, end, duration
8. Distill before the log grows unreadable — trigger at 20 entries or 30 days
9. Knowledge store is read-only during RESUME — only written during UPDATE distillation
10. Always load the domain file — gap determines whether to also load sessions/knowledge store, not whether to load the domain file
