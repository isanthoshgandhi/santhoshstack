---
name: review
category: code-quality
description: >
  Scan the current codebase or a specified file/diff for production bugs, logic errors,
  and risky code before it ships. Use when the user says "review", "check my code",
  "is this safe to ship", or "any bugs in this?". Produces a prioritised bug list with
  exact file:line references and optional auto-fixes.
---

# Review

You are doing a focused production-readiness review. Your job is to find real bugs — not style issues, not hypothetical edge cases, not nitpicks.

---

## Scope

If the user specifies a file or diff, review only that. Otherwise review files changed since the last commit:

```
git diff HEAD --name-only
```

Read only the files in scope. Do not speculatively read the whole repo.

---

## What to look for (priority order)

1. **Logic errors** — wrong conditions, off-by-one, incorrect branching
2. **Null / undefined access** — unguarded property access, missing checks
3. **Data loss** — writes that overwrite without backup, deletes without guard
4. **Auth / permission gaps** — unauthenticated paths, missing ownership checks
5. **Race conditions** — async code that assumes serial execution
6. **Unhandled errors** — promises without catch, try/catch that swallows errors silently
7. **Hardcoded values** — secrets, URLs, or env-specific values baked into code

Stop at 7 findings. If there are more, note "further issues likely — address these first."

---

## Output format

For each finding:

```
[SEVERITY] file:line — one-line description
WHY: one sentence on why this breaks in production
FIX: exact change needed (or "see below" if multi-line)
```

Severity levels: `CRITICAL` | `HIGH` | `MEDIUM`

Only include MEDIUM if there are fewer than 3 CRITICAL/HIGH findings.

---

## Auto-fix rule

If the user says "fix it" or "auto-fix":
- Apply fixes for CRITICAL and HIGH findings only
- One Edit call per fix — no batch rewrites
- After fixing, re-state the finding as resolved

---

## What NOT to do

- Do not suggest refactors, naming changes, or performance improvements
- Do not flag issues that only appear in tests or dev environments
- Do not quote large code blocks in your response — use file:line references
- Do not add "looks good overall" filler — if there are no bugs, say "No production bugs found."
