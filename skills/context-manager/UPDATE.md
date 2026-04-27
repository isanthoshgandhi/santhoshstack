# Context Manager — UPDATE mode

Save progress at session end.

---

### Step 1 — Record session end time

Note the current time. Calculate duration from session start (ask user if start time unknown).

### Step 2 — Detect what changed

Run `git log --oneline -5` to see what was committed this session, then `git show --stat HEAD`
for the most recent commit's file summary. Do not use `git diff HEAD` — on a clean workspace
after commits it returns nothing.

Scan the conversation for:
- Bugs found and fixed (with commit hashes)
- Decisions made
- Tasks completed / abandoned
- New open questions or blockers
- Current numbers/stats

**Large changesets:** if `git show --stat HEAD` shows >50 files, read only files relevant to the current domain.

### Step 3 — Update domain context file

Edit `docs/context/{domain}.md`. Surgical edits only.

Always update:
- `Updated:` timestamp at top
- `RESUME FROM HERE` block — date, what was done, current state, open bugs, next action, Do NOT list
- Any stale numbers elsewhere in the file

### Step 3b — Update reference file (if needed)

Check: did any of these change this session?
- Architecture or data flow
- File paths or entry points
- A significant decision was made (with rationale)
- An alternative was explicitly rejected
- A new capability was built

If yes → edit `docs/context/{domain}-ref.md`. Surgical edits only.
- Replace stale entries, do not append
- Add new decisions to the `## Why it's built this way` section with date
- Update `## Where it lives` table if paths changed
- Update `## What exists` if a new feature shipped

If no → skip this step entirely. Do not touch the ref file.

If `{domain}-ref.md` doesn't exist yet → create it now using the template from SETUP.md Step 4.

### Step 4 — Update pointers.md QUICK RESUME block

Update: date+time, where we left off, next action.

### Step 5 — Append to sessions log

Add entry to `docs/sessions/SESSIONS.md`:

```markdown
## {YYYY-MM-DD} Session {N}
**Start:** {HH:MM}  **End:** {HH:MM}  **Duration:** {Xh Ym}
**Gap since last session:** {X days}
**Domain:** {domain}
**What was done:** {bullets}
**Issues hit:** {list}
**Decisions made:** {list}
**Next:** {next action}
```

### Step 6 — Add backlog items

Add deferred items to `docs/backlog/BACKLOG.md`. Do not duplicate existing items.
If cross-project relevant, also add to `~/.claude/knowledge/global-backlog.md`.

### Step 7 — Check distillation trigger

Count session entries: `grep -c "^## " docs/sessions/SESSIONS.md`.
Check `~/.claude/knowledge/projects/{slug}/learnings.md` header for last distillation date.

**Trigger distillation if ANY of:**
- Sessions log has > 20 entries since last distillation
- Gap since last distillation > 30 days
- This is a Cold resume (gap > 60 days)

If triggered, run Step 8. Otherwise skip to Step 9.

### Step 8 — Distillation (when triggered)

Read only sessions since last distillation from `SESSIONS.md` — not the full file.

Extract:
- Recurring issues (appeared 2+ times → pattern)
- Key decisions with rationale
- Resolved bugs (title + fix, no code)
- What was deferred and why
- Velocity (avg session duration, cadence)

Prioritize by recency: patterns recurring in the last 7 days → extract first.
One-off items older than 6 months → skip unless still marked open.

Write / update `~/.claude/knowledge/projects/{slug}/learnings.md`:

```markdown
# {Project} — Distilled Learnings

> Last distilled: {YYYY-MM-DD}
> Sessions covered: {N} sessions from {start} to {end}
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

Update `~/.claude/knowledge/patterns.md` — add/update patterns that appeared 2+ times.
Update `~/.claude/knowledge/index.md` — update last distilled date for this project.

### Step 9 — Update memory pointer files

Keep memory files lean — 5–10 lines pointing to `docs/context/`.

### Step 10 — Commit and push

```bash
git add docs/context/ docs/sessions/ docs/backlog/ docs/changelog/
git commit -m "docs: context update {date} — {one line summary}"
git push
```
