# santhoshstack

Personal AI skills by [Santhosh Gandhi](https://github.com/isanthoshgandhi) — VC content creator · systems thinker · author · AI-enabled builder.

---

## What this is

A collection of Claude Code skills I find useful and interesting. I open-source them in case others do too.

---

## Philosophy

**AI tools forget. You shouldn't have to repeat yourself.**

Every session starts from zero unless you build systems that survive context resets. Every token wasted on verbose responses or unnecessary file reads is a token not spent on the actual problem.

I'm not a software engineer. I'm sharing what I'm exploring as someone who came to this from a different direction — and I believe that perspective is useful, especially for others who aren't engineers either.

---

## Skills

| Skill | What it does |
|---|---|
| `context-manager` | Three-layer context system for any project. SETUP builds `docs/context/` so any AI tool can resume without re-reading everything. RESUME detects how long you've been away and loads the right amount of context. UPDATE saves progress and distills sessions into long-term learnings. Works with Claude, Codex, Cursor, Windsurf. |
| `frugal-token-usage` | Mid-session audit. Stops unnecessary Bash, enforces dedicated tools, cuts verbose responses. |
| `foresight-intelligence` | Strategic foresight using IFTF methodology. Two modes: Soft Predict (instant, works on claude.ai) and Hard Predict (deterministic Python pipeline, identical output every run). Say `hard predict: [question]` for the deterministic mode. |

More skills added as I build them.

---

## Install

### Option A — Install all skills at once

```bash
claude plugin marketplace add isanthoshgandhi/santhoshstack
claude plugin install santhoshstack
```

This installs all skills from this repo into `~/.claude/skills/`.

---

### Option B — Install a single skill

Pick only what you need. Each skill is standalone.

**1. Clone or download this repo:**
```bash
git clone https://github.com/isanthoshgandhi/santhoshstack.git
```

**2. Copy the skill you want:**

#### context-manager

Mac / Linux:
```bash
cp -r santhoshstack/skills/context-manager ~/.claude/skills/
```
Windows (PowerShell):
```powershell
Copy-Item -Recurse santhoshstack\skills\context-manager $env:USERPROFILE\.claude\skills\
```

#### frugal-token-usage

Mac / Linux:
```bash
cp -r santhoshstack/skills/frugal-token-usage ~/.claude/skills/
```
Windows (PowerShell):
```powershell
Copy-Item -Recurse santhoshstack\skills\frugal-token-usage $env:USERPROFILE\.claude\skills\
```

#### foresight-intelligence

Mac / Linux:
```bash
cp -r santhoshstack/skills/foresight-intelligence ~/.claude/skills/
```
Windows (PowerShell):
```powershell
Copy-Item -Recurse santhoshstack\skills\foresight-intelligence $env:USERPROFILE\.claude\skills\
```

**3. Verify it's available:**
```bash
claude skills list
```

You should see the skill name in the list. No restart needed.

---

### Which skills should I install?

| Skill | Install if... |
|---|---|
| `context-manager` | You work on multiple projects and lose context between sessions |
| `frugal-token-usage` | You want tighter token discipline mid-session |
| `foresight-intelligence` | You do strategic thinking, scenario planning, or prediction work |

---

## How to use a skill

After installing, invoke in Claude Code by typing the skill name as a slash command:

```
/context-manager
/frugal-token-usage
/foresight-intelligence
```

Or just describe what you want — Claude will trigger the right skill automatically based on what you say.

---

## Recommended: Add rules to CLAUDE.md

Skills are on-demand. For rules you want always active, add them to `~/.claude/CLAUDE.md`.

The frugal rules in particular are more effective as permanent standing orders than as a skill you have to remember to invoke.

**Trade-off:** Rules in CLAUDE.md apply to every session and every project — including casual conversations where you may not want strict token discipline. Skills are opt-in. Pick based on how you work.

A starter CLAUDE.md is in [`claude.md.example`](./claude.md.example).

---

## More from Santhosh Gandhi

[santhoshgandhi.com](https://santhoshgandhi.com)

**Writing & Media**
- [Medium](https://medium.com/@isanthoshgandhi) — Writing on venture capital, startups, and AI
- [YouTube — VC with Santhosh](https://www.youtube.com/@vcwithsanthosh) — VC content
- [Instagram — @vcwithsanthosh](https://www.instagram.com/vcwithsanthosh) — VC content

**Book**
- [Notes of an Unconventional UX Researcher](https://www.santhoshgandhi.com/notesofuxresearcher) — [Kindle](https://www.amazon.in/Notes-Unconventional-Researcher-Santhosh-Gandhi-ebook/dp/B0B8TR339W) · [Paperback](https://www.amazon.in/Notes-Unconventional-Researcher-Santhosh-Gandhi/dp/B0B9RYV44Q)

**Open source**
- [venture-capital-intelligence](https://github.com/isanthoshgandhi/venture-capital-intelligence) — Startup screening, pitch decks, cap tables, financial modeling
- [awesome-vc-opensource](https://github.com/isanthoshgandhi/awesome-vc-opensource) — Curated list of open-source tools for VC and startups

---

MIT License
