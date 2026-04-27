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

| Skill | What it does | Invoke |
|---|---|---|
| `context-manager` | Three-layer context system. SETUP builds `docs/context/` so any AI tool can resume without re-reading everything. Two files per domain — operational (`{domain}.md`) and reference (`{domain}-ref.md`). UPDATE distills sessions into long-term learnings. | `/context-manager` |
| `arch-map` | Generates `docs/ARCHITECTURE.md` — Mermaid system diagram, plain English overview, data flow walkthrough, tech stack with rationale. For humans: share with stakeholders, collaborators, contributors. | `/arch-map` |
| `frugal-token-usage` | Mid-session audit. Stops unnecessary Bash calls, enforces dedicated tools, cuts verbose responses. Run when a session feels bloated. | `/frugal-token-usage` |
| `foresight-intelligence` | Strategic foresight using IFTF methodology. Soft Predict (instant) and Hard Predict (deterministic Python pipeline, identical output every run). | `/foresight-intelligence` |
| `review` | Production-readiness review. Finds real bugs — logic errors, null access, data loss, auth gaps, race conditions, hardcoded secrets. Prioritised findings with exact `file:line` references. No style feedback. | `/review` |
| `security-audit` | Security audit covering OWASP Top 10 — injection, auth gaps, secrets in code, missing validation, info leakage, CORS misconfig, missing rate limiting. Each finding includes attack vector and fix. | `/security-audit` |
| `whybroken` | Root-cause tracer. Forms a hypothesis, follows the execution path to the actual cause, proposes the precise fix. Never patches symptoms. | `/whybroken` |

> **Tip for `frugal-token-usage`:** The rules work better as permanent standing orders than on-demand. Copy them into `~/.claude/CLAUDE.md`. A starter file is in [`claude.md.example`](./claude.md.example).

---

## Install

> Requires [Claude Code](https://claude.ai/code) to be installed.

### AI-native

Just tell Claude Code what you want:

```
Install the context-manager skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the arch-map skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the frugal-token-usage skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the foresight-intelligence skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the review skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the security-audit skill from github.com/isanthoshgandhi/santhoshstack
```
```
Install the whybroken skill from github.com/isanthoshgandhi/santhoshstack
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
