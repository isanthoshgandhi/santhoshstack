# santhoshstack

Personal AI skills by [Santhosh Gandhi](https://github.com/isanthoshgandhi) — builder, investor, and writer on venture capital and startups.

---

## What this is

A curated set of Claude Code skills I use every day. Not a framework. Not a platform. Just the tools that make AI sessions faster, cheaper, and less repetitive.

Each skill solves one problem I kept hitting. I open-source them because the problems aren't unique to me.

---

## Philosophy

**AI tools forget. You shouldn't have to repeat yourself.**

Every session starts from zero unless you build systems that survive context resets. Every token wasted on verbose responses or unnecessary file reads is a token not spent on the actual problem.

These skills are my answer to both.

---

## Install

```bash
claude plugin marketplace add isanthoshgandhi/santhoshstack
claude plugin install santhoshstack
```

Or copy any skill directly into `~/.claude/skills/`.

---

## Skills

| Skill | What it does |
|---|---|
| `context-manager` | Sets up `docs/context/` so any AI tool can resume any project without re-reading everything. Three modes: SETUP, RESUME, UPDATE. Works with Claude, Codex, Cursor, Windsurf. |
| `frugal-token-usage` | Mid-session audit. Stops unnecessary Bash, enforces dedicated tools, cuts verbose responses. |

More skills added as I build them.

---

## Recommended: Add rules to CLAUDE.md

Skills are on-demand. For rules you want always active, add them to `~/.claude/CLAUDE.md`.

The frugal rules in particular are more effective as permanent standing orders than as a skill you have to remember to invoke.

**Trade-off:** Rules in CLAUDE.md apply to every session and every project — including casual conversations where you may not want strict token discipline. Skills are opt-in. Pick based on how you work.

A starter CLAUDE.md is in [`claude.md.example`](./claude.md.example).

---

## More from santhoshstack

- [foresight-intelligence](https://github.com/isanthoshgandhi/foresight-intelligence) — Strategic foresight using IFTF methodology. Soft + Hard Predict.
- [venture-capital-intelligence](https://github.com/isanthoshgandhi/venture-capital-intelligence) — Startup screening, pitch decks, cap tables, financial modeling.
- [buildwithclaude](https://github.com/isanthoshgandhi/buildwithclaude) — Plugin marketplace for Claude Code.

---

MIT License
