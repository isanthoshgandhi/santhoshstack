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
| < 14 days | Normal | QUICK RESUME + `{domain}.md` + `{domain}-ref.md` |
| 14–60 days | Deep | Normal + skim last 3 sessions in SESSIONS.md |
| > 60 days | Cold | Deep + knowledge store + flag for distillation |

**Always load both domain files — regardless of gap.** `{domain}.md` has resume state.
`{domain}-ref.md` has what exists, where it lives, how it works, and why it's built this way.
Neither is sufficient alone. QUICK RESUME alone has caused repeated mistakes in the same session.

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

Always load:
1. `docs/context/{domain}.md` — operational resume state
2. `docs/context/{domain}-ref.md` — reference (what/where/how/why)

If `{domain}-ref.md` doesn't exist (pre-v2 context setup), note it and flag to user at the end: "Reference file missing — create it during next UPDATE."

Additional by depth:
- Deep: also skim last 3 sessions in `docs/sessions/SESSIONS.md`
- Cold: also read `~/.claude/knowledge/projects/{slug}/learnings.md` if it exists, and surface relevant patterns from `~/.claude/knowledge/patterns.md`

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
