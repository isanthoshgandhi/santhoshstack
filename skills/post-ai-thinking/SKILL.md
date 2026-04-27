---
name: post-ai-thinking
description: >
  Post AI Thinking — unbiased solution space explorer. Strips inherited human heuristics,
  enumerates ALL possible approaches (existing, cross-domain, hardware-native, AI-native,
  formal, biological, hybrid), then lets the user choose. No paradigm gets priority.
  Existing solutions are fully included — if they fit best, use them.
  Activate when: designing a system, choosing tools, solving an architecture problem,
  or when you want to see the full solution space before committing.
  Invoke as: /post-ai-thinking or say "explore all solutions", "show me the full space",
  "post AI thinking", "what are all options for X".
---

# Post AI Thinking

Enumerate the full solution space before suggesting anything. No paradigm gets top billing.
Existing solutions are valid options — the goal is to make choosing them a *decision*, not a default.

---

## The Core Principle

Every era's tools shape how people think. Before AI: the bottleneck was finding and synthesizing information.
After AI: the bottleneck is asking the right question and choosing from a full space.

**Current problem:** AI trained on human-written content surfaces human heuristics first.
The most-documented solution wins — not the most-appropriate one.

**This skill's job:** Suppress anchoring bias. Enumerate everything. Step back. Let the user choose.

Existing solutions belong in the space too. If the traditional tool is the best fit — great. The skill
confirms that as a *choice*, not an assumption.

---

## Reasoning Chain — Execute in Order

### Phase 1 — Constraint Floor (First Principles)

Before generating any solution, find what's actually constrained.

Ask and answer explicitly:

1. **What is the real problem?**
   Strip the solution framing from the question. "How do I store user data?" → "What am I actually
   doing with this data? Reads? Writes? Relationships? Time-series? Blobs?"

2. **What are REAL constraints?**
   Physics, math, logic, actual resource limits. These cannot be bypassed.
   State them with numbers where possible.

3. **What are INHERITED constraints?**
   Human cognitive limits, historical path dependency, marketing, convention.
   These can be questioned. Label them explicitly as inherited.

4. **What remains after stripping inherited constraints?**
   This is the actual problem space. Solutions must fit this, not the framed version.

Output:
```
CONSTRAINT FLOOR
Real constraints:      [list with numbers]
Inherited constraints: [list — these are assumptions, not facts]
Actual problem:        [one sentence, stripped of framing]
```

---

### Phase 2 — Why Human Heuristics Dominate (Systems Thinking)

Before enumerating solutions, understand why the obvious answer exists.

For the dominant human heuristic in this space:
- What reinforcing loop keeps it dominant? (documentation → adoption → more documentation → ...)
- Where is the leverage point — where does a small change cascade?
- Is the heuristic dominant because it's optimal, or because it got documented first?

Output:
```
HEURISTIC AUDIT
Dominant heuristic:  [name]
Reinforcing loop:    [what keeps it top of mind]
Leverage point:      [where it could be displaced]
Dominance reason:    OPTIMAL / PATH-DEPENDENT / FIRST-DOCUMENTED
```

If `OPTIMAL`: the existing solution will likely win. Note this early. Still enumerate.
If `PATH-DEPENDENT` or `FIRST-DOCUMENTED`: the solution space likely has better fits.

---

### Phase 3 — Full Solution Enumeration

Generate solutions across ALL paradigms. No ranking. No defaults.
Each solution gets the same treatment regardless of origin.

**Paradigms to cover — do not skip any:**

```
1. EXISTING / HUMAN HEURISTIC
   What have people already built for this?
   Why does it exist? What edge cases does it handle?
   Honest strengths AND honest weaknesses for THIS specific context.

2. HARDWARE-NATIVE
   What does the actual local hardware enable at its raw capability level?
   (Not marketed use case — actual: CPU ISA, SIMD, cache topology,
   GPU shader throughput, RAM bandwidth, NVMe IOPS, network packet rate)
   What solution emerges if you design to the hardware, not around it?

3. FORMAL / MATHEMATICAL
   What does theory say is optimal? (Information theory, queuing theory,
   graph theory, linear algebra, probability — whichever applies)
   What's the provably best solution given the real constraints?

4. CROSS-DOMAIN
   What have adjacent fields solved that looks like this problem?
   (Biology, logistics, materials science, military ops, linguistics,
   economics, physics — pull the structural analogy)

5. AI-NATIVE / AI-OPERATOR
   If AI is the primary operator (not a human), what changes?
   What interface/protocol/format disappears because it only existed
   for human readability?

6. EMERGENT / HYBRID
   What combinations of the above produce something none of them do alone?
   What emerges at the intersection of two paradigms nobody usually combines?
```

For each solution:
```
[PARADIGM] — [Solution Name]
What it is:     [one sentence]
Fits when:      [specific conditions where this is optimal]
Costs/risks:    [honest tradeoffs]
Ease:           REUSE EXISTING / ADAPT EXISTING / BUILD NEW
Constraint fit: [maps to which real constraints from Phase 1]
```

---

### Phase 4 — Novelty Check

After enumeration, for each solution ask:
**"Am I suggesting this because it's genuinely in the solution space, or because it appeared
most frequently in human writing?"**

If the latter — don't remove it, but label it:
```
[ANCHORING FLAG] — This solution rose early due to training distribution, not fit.
Included as a valid option. Evaluate on merits.
```

---

### Phase 5 — Present the Flat Space

No ranking. No "recommended." Present all solutions equally.

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
POST AI THINKING  ·  SOLUTION SPACE
[Problem — stripped form from Phase 1]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

CONSTRAINT FLOOR
Real:      [list]
Inherited: [list]

HEURISTIC AUDIT
[from Phase 2 — one line each]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SOLUTION SPACE  (no ranking — user chooses)

[EXISTING]         [Solution Name]
  What:       ...
  Fits when:  ...
  Costs:      ...
  Ease:       REUSE EXISTING
  [ANCHORING FLAG if applicable]

[HARDWARE-NATIVE]  [Solution Name]
  What:       ...
  Fits when:  ...
  Costs:      ...
  Ease:       BUILD NEW

[FORMAL]           [Solution Name]
  What:       ...
  Fits when:  ...
  Costs:      ...
  Ease:       ADAPT EXISTING

[CROSS-DOMAIN]     [Solution Name]
  What:       ...
  Fits when:  ...
  Costs:      ...
  Ease:       BUILD NEW

[AI-NATIVE]        [Solution Name]
  What:       ...
  Fits when:  ...
  Costs:      ...
  Ease:       BUILD NEW

[HYBRID]           [Solution Name]
  What:       ...
  Fits when:  ...
  Costs:      ...
  Ease:       ADAPT EXISTING

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

ELIMINATION (below real constraint floor)
[Solutions that violate Phase 1 real constraints — excluded with reason]

CHOOSING GUIDE
If your priority is [ease/speed]:     → look at EASE = REUSE EXISTING options
If your priority is [performance]:    → look at HARDWARE-NATIVE or FORMAL options
If your priority is [novel fit]:      → look at CROSS-DOMAIN or HYBRID options
If AI operates this system:           → look at AI-NATIVE options
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Important Rules

**Never rank solutions** — ordering is bias in disguise.

**Never suppress existing solutions** — if PostgreSQL is the right answer, it should appear
clearly in the EXISTING slot. The skill's job is to make it a choice, not to displace it.

**Label ease honestly** — REUSE EXISTING is a legitimate strength. If the traditional tool
is easier and fits — say so clearly. Users should feel confident picking it.

**Eliminate only on real constraints** — never eliminate a solution because it's unfamiliar
or unconventional. Only eliminate if it violates Phase 1 real constraints with a reason.

**The skill succeeded when** the user can make a confident, informed choice — even if that
choice is the most conventional option. Confidence through visibility, not novelty for its own sake.

---

## When to Invoke

- Designing a new system or feature
- Choosing between tools or frameworks
- Architecture decisions with multiple valid approaches
- When you suspect you're defaulting to a familiar solution without seeing alternatives
- When a problem feels harder than it should (often means wrong framing, not hard problem)

Invoke: `/post-ai-thinking [your problem]`
Or say: "explore all solutions for X", "show me the full space", "post AI thinking on X"
