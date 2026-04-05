# santhoshstack

Personal Claude Code skills by [Santhosh Gandhi](https://github.com/isanthoshgandhi).

Two skills. Both designed to make every AI coding session faster and cheaper.

---

## Skills

### context-manager
Sets up a file-based context system (`docs/context/`) so any AI tool can resume any project without re-reading everything.

Three modes:
- **SETUP** — first time on a project. Audits the codebase, builds `docs/context/` scaled to project size.
- **RESUME** — session start. Reads `pointers.md`, loads 2-3 domain files, shows exactly where you left off.
- **UPDATE** — session end. Saves progress, updates context files, commits.

Works with Claude Code, Codex, Cursor, Windsurf, Antigravity — plain markdown, no tool-specific syntax.

**Install:**
```bash
# Copy to your Claude skills directory
cp -r skills/context-manager ~/.claude/skills/context-manager
```

**Use:**
```
/context-manager
```

---

### frugal-token-usage
Mid-session audit that enforces minimal-token behaviour. Reviews what Claude is doing and corrects it: stops unnecessary Bash commands, enforces dedicated tools (Read/Grep/Glob), cuts preamble and trailing summaries.

**Install:**
```bash
cp -r skills/frugal-token-usage ~/.claude/skills/frugal-token-usage
```

**Use:**
```
/frugal-token-usage
```

---

## Recommended: Add to Claude Global (CLAUDE.md)

Both skills work best when their rules are always active — not just when explicitly invoked.

Add this to `~/.claude/CLAUDE.md`:

```markdown
## Frugal Token Usage

### Hand off CLI commands — don't run them
Give the exact command and say "Run this in your terminal." Do NOT run via Bash:
- Builds, installs, test runs when outcome is already known

Run via Bash ONLY when you need the output to decide your next step.

### Use dedicated tools, not Bash
- Read files → Read tool (with offset+limit)
- Search content → Grep tool (with head_limit)
- Find files → Glob tool
- Edit files → Edit tool

### Read only what you need
- Grep first, then Read with offset+limit — never read full files speculatively
- If you already read a file this session, use what you noted — don't re-read

### Keep responses short
- Lead with the answer — not the reasoning
- No preamble, no trailing summary
- One sentence if one sentence is enough

### Minimise tool calls
- Parallel tool calls when independent — one message, multiple tools
- Don't spawn an Agent when Grep or a direct Read would find it

## On Session Start
Run /context-manager at the start of any session on a project that has docs/context/.
```

### Trade-offs of adding to CLAUDE.md

| | Benefit | Cost |
|---|---|---|
| **Frugal rules in CLAUDE.md** | Always enforced, no invocation needed | Claude may be overly terse in casual conversations |
| **context-manager on session start** | Consistent resume across all tools | Adds 2-3 file reads at session start (~30 seconds) |
| **Skills only (not global)** | Opt-in — use when you want it | Easy to forget, inconsistent across sessions |

**Recommendation:** Put frugal rules in CLAUDE.md permanently. Use `/context-manager` explicitly — don't auto-trigger it, since not every session needs a full resume.

---

## Philosophy

AI tools forget everything between sessions. Most developers compensate by re-explaining context every time — burning tokens, losing momentum.

The right fix is a file-based context system outside the AI's memory. `docs/context/pointers.md` as a single entry point. Load 2-3 files max. Never load everything.

Frugal token usage is the other half: Claude's default behaviour is verbose and tool-heavy. Explicit rules fix that.

Both skills are about getting more done with less overhead.

---

## Author

Santhosh Gandhi — building [Prezeed](https://github.com/isanthoshgandhi/prezeed) (vertical search for Indian founders), [Viveka Compass](https://github.com/isanthoshgandhi/wisdom-calculator-playbook), and [foresight-intelligence](https://github.com/isanthoshgandhi/foresight-intelligence).
