# Context Manager — SETUP mode

Use this when the project has no `docs/context/` folder yet.

---

### Step 1 — Audit the project

Read the project root. Look for:
- Existing docs (README, CONTEXT.md, CHANGELOG, any markdown)
- Code structure (main concerns — frontend, backend, crawler, API, etc.)
- Git history (`git log --oneline -20`) — what has been worked on recently
- Any existing notes, backlogs, or decision records

Ask the user: "What are the main domains of work in this project?"
Examples: corpus/ingestion, product/UI, schema/database, algorithm/ranking, frontend, backend

### Step 2 — Design the structure (fit the project, don't impose)

- How many distinct concerns? (1 → flat; 5+ → subfolders)
- Does it have operational logs worth keeping? (long-running → yes; small script → no)
- Is there a backlog worth tracking? (active development → yes; maintenance → maybe not)
- Will multiple tools work on it? (yes → more structure; solo → less)

**The only fixed requirement:**
```
{project-root}/docs/context/pointers.md    ← single entry point, always
```

**Small project (1–2 domains):** `docs/context/pointers.md` + `docs/context/main.md` + `docs/context/main-ref.md`

**Medium project (2–4 domains):**
```
docs/context/{domain-N}.md
docs/context/{domain-N}-ref.md
docs/sessions/SESSIONS.md
docs/backlog/BACKLOG.md
```

**Large project (multi-domain, long-running):**
```
docs/context/        sessions/        changelog/
backlog/             {domain}/        research/
```

Every domain always gets two files: `{domain}.md` (operational) + `{domain}-ref.md` (reference). No exceptions.

If a folder has no content, don't create it. Add structure when you need it.

### Step 3 — Write pointers.md

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
1. `docs/context/{domain-1}.md` — resume state, next tasks
2. `docs/context/{domain-1}-ref.md` — what exists, where it lives, how it works, why
3. `docs/backlog/BACKLOG.md` — pending work (skim relevant section only)

Skip: all other domain files, sessions history, changelog

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

Two files per domain. Do not merge them.

**`docs/context/{domain}.md`** — operational only, changes every session:

```markdown
# {Domain} — Operational Context

> Domain: {domain}
> Updated: {YYYY-MM-DD HH:MM}
> Staleness threshold: 14 days

## RESUME FROM HERE
Last session: {YYYY-MM-DD HH:MM}
What was done: {bullet points}
Current state: {one sentence — specific numbers/status}
Open bugs: {list with status}
Next action: {single most important next step}
Do NOT: {dead ends or approaches already ruled out this sprint}

## Current Status
## Next Tasks (in order)
## Known Issues / Open Questions
```

**`docs/context/{domain}-ref.md`** — reference only, changes when architecture or decisions change:

```markdown
# {Domain} — Reference

> Domain: {domain}
> Updated: {YYYY-MM-DD HH:MM}
> Snapshot, not a log. Replace stale entries — never append without pruning.
> For human-readable architecture map, see docs/ARCHITECTURE.md (run /arch-map to generate)

## What exists
{Feature and capability inventory — what the system can do today}

## Where it lives
| Component | Path | Notes |
|---|---|---|
| {component} | {file/folder path} | {what to know} |

## How it works
{Architecture, data flow, key patterns — bullet facts, not prose}

## Why it's built this way
{Key decisions with rationale and rejected alternatives}
- {decision}: {why this approach} [{YYYY-MM}] — Rejected: {alternatives and why not}
```

### Step 5 — Create operational files

**`docs/sessions/SESSIONS.md`:**
```markdown
# Sessions Log
> Append only. One entry per session. Include timing always.

## {YYYY-MM-DD} Session {N}
**Start:** {HH:MM}  **End:** {HH:MM}  **Duration:** {Xh Ym}
**Gap since last session:** {X days / first session}
**Domain:** {domain}
**What was done:** **Issues hit:** **Decisions made:** **Next:**
```

**`docs/backlog/BACKLOG.md`:** Priority: Next / Domain sections / Deferred / Decided: Do Not Do

**`docs/changelog/CHANGELOG.md`:** All changes, most recent first. Unreleased section at top.

### Step 6 — Bootstrap the knowledge store

Check if `~/.claude/knowledge/` exists. If not, create it now — Layer 3 must exist before any project uses distillation or Cold resume. Do not skip this step.

```
~/.claude/knowledge/
├── index.md            ← project registry
├── patterns.md         ← recurring patterns across projects
├── global-backlog.md   ← cross-project backlog
└── projects/{slug}/learnings.md
```

See UPDATE.md for the full file templates.

### Step 7 — Wire up memory

Update `~/.claude/projects/.../memory/` files to point at `docs/context/`:
```markdown
## Source of truth
`docs/context/{domain}.md` — always read this, not this file.
- Status: {current status}  · Next: {next action}  · Root: {path}
```

Update `MEMORY.md` session bootstrap:
```markdown
Any session working on {Project} must:
1. Read `docs/context/pointers.md` FIRST
2. Load ONLY the files listed for your domain
3. Gap > 60 days → also load `~/.claude/knowledge/projects/{slug}/learnings.md`
```

### Step 8 — Wire up cross-tool config

**Cursor** — `.cursor/rules/context.md` (legacy: `.cursorrules`):
```
Context entry point: docs/context/pointers.md
Load this file first. Pick your domain. Load only 2-3 files listed.
```
> Cursor moved from `.cursorrules` to `.cursor/rules/*.md` — check current docs for your version.

**Windsurf** — `.windsurf/rules/context.md` (legacy: `.windsurfcontext`):
```
entry: docs/context/pointers.md
```
> Windsurf moved from `.windsurfcontext` to `.windsurf/rules/` — check current docs for your version.

**Any other tool** — add to README:
```markdown
## For AI Tools
Read `docs/context/pointers.md` first. Pick your domain. Load only what it lists.
```

### Step 9 — Commit

```bash
git add docs/context/ docs/sessions/ docs/changelog/ docs/backlog/ .cursor/ .windsurf/
git commit -m "docs: add context management system"
git push
```

> "Context system created. Start every future session with `/context-manager`."
