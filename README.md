# santhoshstack

Personal AI skills by [Santhosh Gandhi](https://github.com/isanthoshgandhi) — VC content creator, author, AI-enabled builder, systems thinker.

---

## What this is

A collection of Claude Code skills I find useful and interesting. I open-source them in case others do too.

---

## Philosophy

**AI tools forget. You shouldn't have to repeat yourself.**

Every session starts from zero unless you build systems that survive context resets. Every token wasted on verbose responses or unnecessary file reads is a token not spent on the actual problem.

I'm not a software engineer. I'm sharing what I'm exploring as someone who came to this from a different direction — and I believe that perspective is useful, especially for others who aren't engineers either.

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
