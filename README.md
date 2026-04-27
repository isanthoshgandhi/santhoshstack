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

### context-manager

Three-layer context system for any project. SETUP builds `docs/context/` so any AI tool can resume without re-reading everything. RESUME loads both the operational file (where you left off) and the reference file (what exists, how it works, why it's built this way). UPDATE saves progress and distills sessions into long-term learnings. Works with Claude, Codex, Cursor, Windsurf.

Each domain gets two files: `{domain}.md` for operational resume state, `{domain}-ref.md` for what/where/how/why reference. Never mixed.

**Invoke**
```
/context-manager
```
Or say: *"set up context for this project"* / *"resume"* / *"save session"*

---

### arch-map

Generates a human-readable architecture document for any codebase. Outputs `docs/ARCHITECTURE.md` with a Mermaid system diagram, plain English system overview, step-by-step data flow, tech stack table with rationale, and key constraints. Built for stakeholders, contributors, and anyone who needs to understand the system without reading the code.

Not a resume artifact — a communication artifact. Share it in your README, send it to collaborators, or use it to onboard new contributors.

**Invoke**
```
/arch-map
```
Or say: *"map the architecture"* / *"document the system"* / *"explain this to a non-technical person"*

---

### frugal-token-usage

Mid-session audit. Stops unnecessary Bash, enforces dedicated tools, cuts verbose responses. Run it when a session feels bloated or slow.

**Invoke**
```
/frugal-token-usage
```
Or say: *"be frugal"* / *"reduce token usage"*

> **Tip:** The frugal rules are more effective as permanent standing orders than as an on-demand skill. Copy them into `~/.claude/CLAUDE.md` to apply them every session. A starter file is in [`claude.md.example`](./claude.md.example).

---

### foresight-intelligence

Strategic foresight using IFTF methodology. Two modes — Soft Predict (instant, works on claude.ai and Claude Code) and Hard Predict (deterministic Python pipeline, identical output every run).

**Invoke**
```
/foresight-intelligence
```
Or say: *"predict: [question]"* for Soft mode · *"hard predict: [question]"* for deterministic mode

---

## Install

> Requires [Claude Code](https://claude.ai/code) to be installed.

### AI-native

Just tell Claude Code what you want:

```
Install the context-manager skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the frugal-token-usage skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the foresight-intelligence skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install all skills from github.com/isanthoshgandhi/santhoshstack
```

Claude will handle the rest. No commands, no paths, no platform differences.

---

### Manual (fallback)

**Clone once:**
```bash
git clone https://github.com/isanthoshgandhi/santhoshstack.git
```

**Copy what you need:**

Mac / Linux:
```bash
cp -r santhoshstack/skills/context-manager ~/.claude/skills/
cp -r santhoshstack/skills/frugal-token-usage ~/.claude/skills/
cp -r santhoshstack/skills/foresight-intelligence ~/.claude/skills/

# or all at once
cp -r santhoshstack/skills/* ~/.claude/skills/
```

Windows (PowerShell):
```powershell
Copy-Item -Recurse santhoshstack\skills\context-manager $env:USERPROFILE\.claude\skills\
Copy-Item -Recurse santhoshstack\skills\frugal-token-usage $env:USERPROFILE\.claude\skills\
Copy-Item -Recurse santhoshstack\skills\foresight-intelligence $env:USERPROFILE\.claude\skills\

# or all at once
Copy-Item -Recurse santhoshstack\skills\* $env:USERPROFILE\.claude\skills\
```

**Verify:**
```bash
ls ~/.claude/skills/        # Mac / Linux
```
```powershell
ls $env:USERPROFILE\.claude\skills\   # Windows
```

No restart needed.

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
