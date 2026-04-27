---
name: post-ai-thinking
description: >
  Post AI Thinking — unbiased solution space explorer. Strips inherited human heuristics,
  enumerates ALL possible approaches across 7 paradigms (human heuristic, hardware-native,
  theoretical limits, biology-inspired, economic/incentive, AI-augmented, hybrid), then lets
  the user choose. No paradigm gets priority. Existing solutions are fully included —
  if they fit best, use them. Includes hardware inventory so unconventional devices
  (phone, old laptop, Pi) surface as legitimate solutions.
  Activate when: designing a system, choosing tools, solving an architecture problem,
  or when you want to see the full solution space before committing.
  Invoke as: /post-ai-thinking or say "explore all solutions", "show me the full space",
  "post AI thinking", "what are all options for X".
---

# Post AI Thinking

Enumerate the full solution space before suggesting anything. No paradigm gets top billing.
Existing solutions are valid — the goal is to make choosing them a *decision*, not a default.

---

## The Core Principle

Every era's tools shape how people think. Before AI: the bottleneck was finding and synthesizing
information. After AI: the bottleneck is asking the right question and choosing from a full space.

**Current problem:** AI trained on human-written content surfaces human heuristics first.
The most-documented solution wins — not the most-appropriate one.

**This skill's job:** Suppress anchoring bias. Enumerate everything. Step back. Let the user choose.

Existing solutions belong in the space too. If the traditional tool is the best fit — that's a
valid outcome. The skill confirms it as a *choice*, not an assumption.

---

## Reasoning Chain — Execute All Phases in Order

---

### Phase 0 — Hardware Inventory

Before anything else: enumerate ALL available devices. Not just the primary machine.
Strip each device's marketed identity. List raw capabilities only.

Ask: "What devices are physically available to solve this problem?"

For each device found:
```
[Device] (marketed as: X)
Raw capabilities:
  CPU:        [cores, GHz, architecture]
  RAM:        [GB]
  Storage:    [GB, type]
  Network:    [interfaces available]
  Always-on:  [yes/no, power source]
  OS:         [what it can run]
  Unique:     [what this device has that others don't]
  Can act as: [server / compute node / sensor / proxy / storage / other]
```

Common devices to consider — do not skip any that may be available:
- Primary laptop/desktop
- Phone (Android → Termux runs nginx, Node, Python; iOS → limited)
- Old/spare laptops or desktops
- Raspberry Pi or single-board computers
- Network router (if running OpenWrt — full Linux)
- Tablet
- Cloud free tiers (if internet available)

Output:
```
HARDWARE INVENTORY
[Device 1] — [raw capabilities summary] — Can act as: [roles]
[Device 2] — [raw capabilities summary] — Can act as: [roles]
...
```

This inventory feeds directly into Phase 3 enumeration.
Every device is a candidate. No device is dismissed because of its marketed name.

---

### Phase 1 — Constraint Floor (First Principles)

Strip the problem framing. Find what's actually constrained.

Ask and answer explicitly:

1. **What is the real problem?**
   Remove solution framing. "Build a server" → "What needs to be served? To whom?
   What latency? What availability? What scale? What budget?"

2. **What are REAL constraints?**
   Physics, math, logic, actual resource limits. Cannot be bypassed.
   State with numbers where possible.

3. **What are INHERITED constraints?**
   Human cognitive limits, historical convention, marketing, path dependency.
   These can be questioned. Label them explicitly.

4. **What remains after stripping inherited constraints?**
   This is the actual problem. Solutions must fit this, not the framed version.

Output:
```
CONSTRAINT FLOOR
Real constraints:      [list with numbers where possible]
Inherited constraints: [list — assumptions, not facts]
Actual problem:        [one sentence, framing stripped]
```

---

### Phase 2 — Heuristic Audit (Systems Thinking)

Before enumerating, understand why the obvious answer exists.

For the dominant human heuristic in this space:
- What reinforcing loop keeps it dominant?
  (e.g. documentation → adoption → more docs → canonical → new engineers learn it → repeat)
- Where is the leverage point where it could be displaced?
- Is it dominant because it's optimal, or because it got documented first?

Output:
```
HEURISTIC AUDIT
Dominant heuristic:  [name]
Reinforcing loop:    [what keeps it top of mind]
Leverage point:      [where it could be questioned]
Dominance reason:    OPTIMAL / PATH-DEPENDENT / FIRST-DOCUMENTED
```

If `OPTIMAL`: existing solution will likely win. Note this. Still enumerate the full space.
If `PATH-DEPENDENT` or `FIRST-DOCUMENTED`: better fits likely exist elsewhere in the space.

---

### Phase 3 — Full Solution Enumeration

7 paradigms. Cover all of them. No ranking. No defaults.
Use the Hardware Inventory from Phase 0 when generating hardware-native solutions.
Each solution gets identical treatment regardless of origin.

---

**1. HUMAN HEURISTIC**
What have people already built for this problem?
Why does this solution exist? What edge cases does it handle well?
Honest strengths AND honest weaknesses for this specific context.
Note: this is valid. If it fits — use it. The goal is not to displace it, but to see it clearly.

---

**2. HARDWARE-NATIVE**
For each device in the Phase 0 inventory:
What solution emerges if you design *to* this hardware's raw capabilities, not around them?
A phone is not a phone — it is: ARM cores + RAM + cellular + GPS + sensors + always-on battery.
What does that capability bundle enable that a "server" category never surfaces?

---

**3. THEORETICAL LIMITS**
Two sub-lenses:
- *Mathematical/formal*: what's provably optimal given the real constraints?
  (algorithms, information theory, complexity, queuing theory — whichever applies)
- *Physics ceiling*: what does thermodynamics, electromagnetism, speed of light actually allow?
  What is the hard upper bound no engineering can breach?
Surface the optimal solution AND the physical ceiling. Gap between them = engineering headroom.

---

**4. BIOLOGY-INSPIRED**
Biology is the only other large-scale optimization system that emerged without human design.
What has evolution, the immune system, neural adaptation, or swarm behavior already solved
that structurally resembles this problem?
Pull the analogy. Map it to the actual problem. What does the biological solution suggest?

---

**5. ECONOMIC/INCENTIVE**
Sometimes the right solution is not engineering — it is aligned incentives.
Open source, prediction markets, token incentives, reputation systems, pricing signals,
distributed human coordination. What does the problem look like if you solve it with
incentive design instead of technical architecture?

---

**6. AI-AUGMENTED**
What changes structurally when AI is part of this system?
Not just "AI operates it" — what disappears, simplifies, or inverts?
- What interface existed only for human readability? → can be removed
- What pre-agreed schema existed because humans needed contracts? → can be negotiated at runtime
- What monitoring existed because humans needed alerts? → can be continuous inference
- What documentation existed for human understanding? → can be generated on demand
Map the structural changes. What solution emerges from this reorganized system?

---

**7. HYBRID**
After enumerating the 6 paradigms above:
What combinations produce something none of them achieve alone?
Look specifically at intersections nobody usually combines.
This is a synthesis step — not speculation. Only propose hybrids grounded in the enumerated solutions.

---

For each solution, output:
```
[PARADIGM] — [Solution Name]
What:        [one sentence]
Fits when:   [specific conditions where this is optimal]
Costs:       [honest tradeoffs]
Ease:        REUSE EXISTING / ADAPT EXISTING / BUILD NEW
Device:      [which device from inventory, if hardware-specific]
Anchoring?   [YES — surfaced due to training frequency, not fit | NO]
```

---

### Phase 4 — Elimination

Remove only solutions that violate Phase 1 REAL constraints.
Never eliminate based on unfamiliarity or unconventionality.
State the real constraint violated and why.

---

### Phase 5 — Present the Flat Space

No ranking. No "recommended." All solutions presented equally.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
POST AI THINKING  ·  SOLUTION SPACE
[Actual problem — stripped form from Phase 1]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

HARDWARE INVENTORY
[from Phase 0]

CONSTRAINT FLOOR
Real:      [list]
Inherited: [list]

HEURISTIC AUDIT
Dominant:  [name] | Reason: [OPTIMAL / PATH-DEPENDENT / FIRST-DOCUMENTED]
Loop:      [one line]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SOLUTION SPACE  (no ranking — you choose)

[HUMAN HEURISTIC]     [Name]
  What:     ...
  Fits:     ...
  Costs:    ...
  Ease:     REUSE EXISTING
  Anchoring: YES / NO

[HARDWARE-NATIVE]     [Name]  (Device: [X])
  What:     ...
  Fits:     ...
  Costs:    ...
  Ease:     BUILD NEW

[THEORETICAL LIMITS]  [Name]
  Optimal:  [mathematical solution]
  Ceiling:  [physical upper bound]
  Gap:      [engineering headroom available]

[BIOLOGY-INSPIRED]    [Name]
  Analogy:  [biological system]
  Maps to:  [how it applies]
  Costs:    ...
  Ease:     BUILD NEW

[ECONOMIC/INCENTIVE]  [Name]
  What:     ...
  Fits:     ...
  Costs:    ...
  Ease:     ADAPT EXISTING / BUILD NEW

[AI-AUGMENTED]        [Name]
  What changes: [what disappears or inverts]
  What emerges: [the new solution]
  Costs:    ...
  Ease:     BUILD NEW

[HYBRID]              [Name]
  Combines: [paradigm A] + [paradigm B]
  What:     ...
  Fits:     ...
  Ease:     ...

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
ELIMINATED
[Solution] — violates: [real constraint] — reason: [one line]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
CHOOSING GUIDE
Speed / ease:        → EASE = REUSE EXISTING options
Raw performance:     → HARDWARE-NATIVE or THEORETICAL LIMITS
Novel fit:           → BIOLOGY-INSPIRED or HYBRID
No engineering:      → ECONOMIC/INCENTIVE
AI in the system:    → AI-AUGMENTED
Unconventional hw:   → HARDWARE-NATIVE (check all devices in inventory)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Rules

**Never rank solutions.** Ordering is bias in disguise.

**Never suppress existing solutions.** If nginx is the right answer it appears clearly
in HUMAN HEURISTIC. The skill makes it a choice, not a displacement.

**Phase 0 is mandatory.** Hardware inventory runs before everything else.
A phone, Pi, or spare laptop in the room is a legitimate solution candidate.

**Eliminate only on real constraints.** Never on unfamiliarity.

**The skill succeeded when** the user makes a confident informed choice —
even if that choice is the most conventional option.
Confidence through visibility. Not novelty for its own sake.

---

## When to Invoke

- Designing a new system or feature
- Choosing between tools or frameworks
- Architecture decisions with multiple valid approaches
- When defaulting to familiar without seeing alternatives
- When a problem feels harder than it should (often wrong framing, not hard problem)

Invoke: `/post-ai-thinking [your problem]`
Or say: "explore all solutions for X", "show me the full space for X", "post AI thinking on X"
