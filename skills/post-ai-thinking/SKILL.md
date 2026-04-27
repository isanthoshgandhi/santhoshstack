---
name: post-ai-thinking
description: >
  Post AI Thinking — unbiased solution space explorer. Strips inherited human heuristics,
  enumerates ALL possible approaches, then lets the user choose. No paradigm gets priority.
  Auto-calibrates depth: simple problems get a quick scan (3 paradigms), architectural
  decisions get the full space (7 paradigms, all phases). Existing solutions are fully
  included — if they fit best, use them.
  Invoke as: /post-ai-thinking or say "explore all solutions", "show me the full space",
  "post AI thinking", "what are all options for X".
---

# Post AI Thinking

Enumerate the full solution space before suggesting anything. No paradigm gets top billing.
Depth auto-calibrates to the problem. Don't over-engineer simple choices.

---

## Step 0 — Calibrate Depth First

Read the problem. Classify it. Choose mode. State the mode before proceeding.

**QUICK mode signals** — any of these present:
- Tool or library comparison ("X vs Y", "which X should I use")
- Single-component decision
- Narrow, well-defined problem space
- Answer space is small (fewer than ~5 serious candidates exist)

**FULL mode signals** — any of these present:
- System architecture or design from scratch
- Multiple components or services involved
- Scale mentioned (users, requests, data volume, cost)
- Hardware resources are relevant to the solution
- Problem involves a paradigm choice, not a tool choice
- "Build", "design", "architect", "platform", "system" in the problem
- No obvious right answer exists

Output before proceeding:
```
MODE: QUICK / FULL
Reason: [one line — what signal triggered this]
```

If user said `--full` → always run FULL regardless of classification.
If user said `--quick` → always run QUICK regardless of classification.

---

# QUICK MODE

3 phases. 3 paradigms. Tight output.

## Q1 — Constraint Floor

One pass only. No sub-questions.
Strip the framing. State the actual problem in one sentence.
List real constraints (2-3 max). Note any obvious inherited constraints.

## Q2 — Pick 3 Paradigms

Always include **Human Heuristic**.
Pick the 2 most applicable from the remaining 6 based on the problem type:

```
Hardware-native     → if physical resources matter
Theoretical limits  → if performance or correctness is the core concern
Biology-inspired    → if the problem is about resilience, adaptation, or scale
Economic/incentive  → if coordination or motivation is the core problem
AI-augmented        → if AI will be part of the system
Hybrid              → if two known approaches have an obvious combination
```

## Q3 — Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
POST AI THINKING  ·  QUICK SCAN
[Actual problem]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[HUMAN HEURISTIC]    [Name]
  What:   ...
  Fits:   ...
  Costs:  ...
  Ease:   REUSE EXISTING

[PARADIGM 2]         [Name]
  What:   ...
  Fits:   ...
  Costs:  ...
  Ease:   ...

[PARADIGM 3]         [Name]
  What:   ...
  Fits:   ...
  Costs:  ...
  Ease:   ...

Need the full space? Run: /post-ai-thinking --full [problem]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

# FULL MODE

5 phases. 7 paradigms. Complete space.

---

## Phase 0 — Hardware Inventory

Enumerate ALL available devices. Strip marketed identity. List raw capabilities.

Ask: "What devices are physically available to solve this problem?"

For each device:
```
[Device] (marketed as: X)
  CPU / RAM / Storage / Network / Always-on / OS
  Unique:     [what this device has that others don't]
  Can act as: [server / compute / sensor / proxy / storage]
```

Devices to consider — do not skip:
- Primary laptop/desktop
- Phone (Android → Termux runs nginx, Node, Python; iOS → limited)
- Old/spare machines
- Raspberry Pi or single-board computers
- Router (OpenWrt → full Linux)
- Cloud free tiers

Output:
```
HARDWARE INVENTORY
[Device] — [capabilities summary] — Can act as: [roles]
```

Skip Phase 0 if problem is purely software with no hardware dimension.

---

## Phase 1 — Constraint Floor

1. **Real problem** — strip framing, one sentence
2. **Real constraints** — physics, math, logic, actual limits (with numbers)
3. **Inherited constraints** — convention, path dependency, marketing (label explicitly)

```
CONSTRAINT FLOOR
Real:      [list with numbers]
Inherited: [list — assumptions, not facts]
Actual:    [one sentence]
```

---

## Phase 2 — Heuristic Audit

For the dominant human heuristic:
- What reinforcing loop keeps it dominant?
- Is it dominant because it's optimal or because it got documented first?

```
HEURISTIC AUDIT
Dominant:  [name]
Loop:      [documentation → adoption → ... → canonical]
Reason:    OPTIMAL / PATH-DEPENDENT / FIRST-DOCUMENTED
```

If `OPTIMAL` → note it. Still enumerate the full space.

---

## Phase 3 — Full Enumeration (7 Paradigms)

No ranking. No defaults. Identical treatment for all.

---

**1. HUMAN HEURISTIC**
What have people built? Why does it exist? What edge cases does it handle?
Honest strengths AND weaknesses for this specific context.

---

**2. HARDWARE-NATIVE**
Use Phase 0 inventory. For each device:
Strip marketed identity. What solution emerges from raw capabilities?
A phone = ARM cores + cellular + GPS + sensors + always-on. What does that enable?

---

**3. THEORETICAL LIMITS**
- *Math/formal*: what's provably optimal? (algorithms, information theory, queuing)
- *Physics ceiling*: hard upper bound (thermodynamics, speed of light, heat)
State both. Gap between them = engineering headroom.

---

**4. BIOLOGY-INSPIRED**
What has evolution, immune systems, swarm behavior, or neural adaptation solved
that structurally resembles this problem?
Map the biological analogy to the actual problem. What does it suggest?
Skip if no structural similarity exists — don't force it.

---

**5. ECONOMIC/INCENTIVE**
What if the solution is aligned incentives, not engineering?
Open source, markets, reputation, token incentives, distributed coordination.
Skip if problem is purely technical with no coordination or motivation dimension.

---

**6. AI-AUGMENTED**
What changes structurally when AI is part of this system?
- What interface existed only for human readability? → remove it
- What pre-agreed schema existed for human contracts? → negotiate at runtime
- What monitoring existed for human alerts? → continuous inference
What solution emerges from this reorganized system?

---

**7. HYBRID**
After enumerating 1-6: what combinations produce something none achieve alone?
Only propose hybrids grounded in the enumerated solutions. No speculation.

---

For each solution:
```
[PARADIGM] — [Name]
What:      [one sentence]
Fits when: [specific conditions]
Costs:     [honest tradeoffs]
Ease:      REUSE EXISTING / ADAPT EXISTING / BUILD NEW
Device:    [if hardware-specific]
```

---

## Phase 4 — Elimination

Remove only solutions violating Phase 1 real constraints.
Never eliminate for unfamiliarity. State the constraint violated.

---

## Phase 5 — Full Output

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
POST AI THINKING  ·  FULL SPACE
[Actual problem]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

HARDWARE INVENTORY      [from Phase 0, or SKIPPED]
CONSTRAINT FLOOR        [real / inherited / actual]
HEURISTIC AUDIT         [dominant / loop / reason]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SOLUTION SPACE  (no ranking — you choose)

[HUMAN HEURISTIC]      [Name]   Ease: REUSE EXISTING
[HARDWARE-NATIVE]      [Name]   Device: [X]
[THEORETICAL LIMITS]   Optimal: [X]  |  Ceiling: [X]  |  Headroom: [X]
[BIOLOGY-INSPIRED]     [Name]   Analogy: [biological system]
[ECONOMIC/INCENTIVE]   [Name]
[AI-AUGMENTED]         [Name]   Changes: [what disappears]
[HYBRID]               [Name]   Combines: [A] + [B]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ELIMINATED
[Solution] — violates: [constraint] — [reason]

CHOOSING GUIDE
Speed/ease:       → HUMAN HEURISTIC (if OPTIMAL) or lowest-ease option
Performance:      → HARDWARE-NATIVE or THEORETICAL LIMITS
Novel fit:        → BIOLOGY-INSPIRED or HYBRID
No engineering:   → ECONOMIC/INCENTIVE
AI in system:     → AI-AUGMENTED
Unconventional:   → HARDWARE-NATIVE (all devices in inventory)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Rules

**Never rank solutions.** Order is bias in disguise.

**Never suppress existing solutions.** If nginx is the right answer it appears clearly.
The skill makes it a choice, not an assumption.

**Skip paradigms that don't apply.** Biology-inspired for a tool comparison = noise.
Economic/incentive for a pure engineering problem = noise. Skip cleanly, don't force it.

**Eliminate only on real constraints.** Never on unfamiliarity.

**The skill succeeded when** the user makes a confident informed choice —
even the most conventional option. Confidence through visibility, not novelty.

---

## Invocation

`/post-ai-thinking [problem]`          → auto-calibrates depth
`/post-ai-thinking --full [problem]`   → always runs full space
`/post-ai-thinking --quick [problem]`  → always runs quick scan

Or say: "explore all solutions for X", "show me the full space for X", "post AI thinking on X"
