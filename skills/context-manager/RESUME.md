# Context Manager — RESUME mode

Load minimal context for session start.

---

### Step 1 — Find pointers.md (with fallback)

Look for `docs/context/pointers.md`.

- Not found → check for `CONTEXT.md` at project root, or any `.md` in `docs/context/`
- Still nothing → tell the user: "No context system found. Run SETUP mode first."
- Do NOT proceed blind.

### Step 2 — Calculate gap and set resume depth

From the `Last session` timestamp in QUICK RESUME, calculate gap to today.
If no time component (date only), treat as 00:00. If no timestamp, treat as Normal.

| Gap | Depth | What to load |
|---|---|---|
| < 14 days | Normal | QUICK RESUME + domain context file |
| 14–60 days | Deep | QUICK RESUME + domain file + skim last 3 sessions |
| > 60 days | Cold | Deep resume + check knowledge store + flag for distillation |

**Always load the domain file — regardless of gap.** QUICK RESUME alone is never sufficient
for hands-on work. It lacks critical non-obvious facts (source of truth files, dropped services,
tooling constraints) that live in the domain file. Loading only QUICK RESUME has caused
repeated mistakes in the same session.

### Step 3 — Check domain file staleness

Read the `Updated:` timestamp from the domain context file.
If older than 14 days, warn: "Domain file last updated {X} days ago — may be stale."

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
Depth: [Normal / Deep / Cold]
Where we left off: [1–2 sentences]
Staleness warning: [if applicable]
Relevant past patterns: [if Cold resume and patterns found]
Next action: [the specific next step]
```

Wait for user confirmation before starting work.
