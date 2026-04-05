---
name: foresight-intelligence
description: >
  Strategic foresight engine using IFTF methodology. Activate for ANY future-oriented question:
  "Will [X]?", "Who will win [X]?", "What happens to [X]?", prediction requests, scenario planning,
  competitive race analysis, technology adoption, geopolitical shifts, or any question about a
  future outcome. Two modes — Soft (instant, works on claude.ai) and Hard (deterministic Python
  pipeline, requires Claude Code). Year is NOT required — the engine infers the horizon.
  Invoke as: /foresight-intelligence or say "predict", "forecast", "foresight", "what are the odds".
---

# Foresight Intelligence

Strategic foresight using IFTF methodology. Two modes — pick based on what you need.

---

## MODE SELECTOR

**Soft Predict** — Claude-native. Instant. Works on claude.ai and Claude Code.
Use for: exploration, quick reads, content, early-stage thinking.
Say: `/foresight-intelligence [your question]` or just ask a future-oriented question.

**Hard Predict** — Deterministic 12-step pipeline. Python computes all arithmetic.
Identical output every run. Full JSON audit trail. Requires Claude Code + Python 3.x.
Say: `hard predict: [your question]` or `run hard foresight: [your question]`

If the user does not specify, default to **Soft Predict**.

---

# SOFT PREDICT — 9-Step Pipeline

Execute ALL steps in order. Never skip. Never combine. Show your work at each step.

---

## Step 1 — Validate Input

Apply exactly 5 binary rules. If ANY rule fails, stop and explain why.

**Rule 1 — Entity Reality:** Does the entity exist in the real world? Fail if fictional or hypothetical.
**Rule 2 — System Existence:** Is the domain observable and researchable? Fail if purely philosophical.
**Rule 3 — Time Horizon:** Observable within 2–30 years? Year NOT required — infer the horizon:
- Competitive race / market dominance → 3–10 years (Strategic)
- Technology adoption → 5–15 years (Strategic)
- Geopolitical / societal shift → 10–20 years (Civilizational)
- Near-term company outcome → 2–5 years (Operational/Strategic)

**Rule 4 — Signal Availability:** Could real-world evidence plausibly exist?
**Rule 5 — Minimum Specificity:** Specific enough to produce distinct scenario outcomes?

Output:
```
VALIDATION
Rule 1 Entity Reality:      PASS / FAIL — [reason]
Rule 2 System Existence:    PASS / FAIL — [reason]
Rule 3 Time Horizon:        PASS / FAIL — [reason] | Inferred horizon: [YYYY–YYYY]
Rule 4 Signal Availability: PASS / FAIL — [reason]
Rule 5 Specificity:         PASS / FAIL — [reason]
Result: PROCEED / STOP
```

---

## Step 2 — Collect Signals

Run exactly 6 web searches. Collect minimum 18 signals total.

1. `"[topic] current status [year]"`
2. `"[topic] growth data market size [year]"`
3. `"[topic] challenges barriers risks"`
4. `"[topic] government policy regulation"`
5. `"[topic] technology infrastructure investment"`
6. `"[topic] historical analogue similar transition"`

For each signal classify all 6 attributes:

| Attribute | Values |
|---|---|
| direction | supporting / opposing / wildcard / neutral |
| steeep_category | Social / Technological / Economic / Environmental / Ethical / Political |
| temporal_layer | Operational (0–3yr) / Strategic (3–10yr) / Civilizational (10+yr) |
| source_type | primary / secondary / opinion |
| recency_days | integer |
| has_evidence | true / false |

---

## Step 3 — Score Signals

Score every signal: `score = recency_weight × reliability_weight × type_weight × evidence_multiplier`. Cap at 1.0.

**Recency:** 0–90d: 1.00 · 91–365d: 0.80 · 1–3yr: 0.60 · 3+yr: 0.40 · unknown: 0.50
**Reliability:** Primary: 1.00 · Major news: 0.90 · Industry report: 0.85 · Analyst: 0.70 · Opinion: 0.50
**Type:** Supporting/Opposing: 1.00 · Neutral: 0.60 · Wildcard: 1.30
**Evidence:** DATA/STATISTIC: ×1.20 · EVENT: ×1.00 · ANALYSIS/OPINION: ×0.70

Apply regional multiplier (tables at bottom). Show scoring table with all columns.

---

## Step 4 — Extract Structural Drivers

Group signals by STEEEP. For each cluster of 3+ signals, identify the underlying driver — the deep force explaining WHY those signals exist.

Extract exactly 3 top drivers, ranked by sum of final_scores.

For each driver:
- **Name:** 3–5 word label
- **Force:** One sentence — the structural reality
- **Signals:** Which signal IDs it explains
- **Temporal reach:** Operational / Strategic / Civilizational
- **Stability:** LOCKED / SHIFTING / FRAGILE

---

## Step 5 — Build 6×3 STEEEP Matrix

Each cell = average final_score of signals in that STEEEP × Temporal combination.

|  | Operational | Strategic | Civilizational |
|---|---|---|---|
| **Social** | | | |
| **Technological** | | | |
| **Economic** | | | |
| **Environmental** | | | |
| **Ethical** | | | |
| **Political** | | | |

Identify: hot zones (>0.50), gap zones (0.00), dominant zone.

---

## Step 6 — Cross-Impact Analysis

For each temporal layer:
- ≥2 hot zones → **CONVERGENCE** (state which categories reinforce each other)
- 1 hot zone → **ISOLATED**
- 0 hot zones → **BLIND LAYER**

Identify **FRICTION POINTS**: hot zones in opposing STEEEP categories.
Convergence bonus: if Strategic = CONVERGENCE → +5% to probable score.

---

## Step 7 — Find 3 Historical Analogues

3 real past cases structurally similar to the question. For each:
- Similarity (%), tipping event, equivalent today (YES/NO/PARTIAL), validates D1/D2/D3.

Prefer similarity ≥ 60%. Below 40% = confidence penalty.

---

## Step 8 — Compute Probabilities + Confidence

Scores are independent (do NOT sum to 100):

```
R_probable  = (supporting signals score > 0.70) × 3
            + (best analogue similarity / 100) × 4
            + (hot zone count) × 2 + convergence_bonus

R_plausible = (supporting signals score 0.40–0.70) × 2
            + (second analogue similarity / 100) × 3

R_possible  = (wildcard signals) × 2
            + (opposing signals score > 0.60) × 2
            + (gap zones / 18) × 3

probable_score  = min(100, round((1 − e^(−R_probable  / 18)) × 100))
plausible_score = min(100, round((1 − e^(−R_plausible / 9))  × 100))
possible_score  = min(100, round((1 − e^(−R_possible  / 5))  × 100))

confidence = signal_count (×0.30) + signal_diversity (×0.30) + recency (×0.20) + evidence (×0.20)
```

---

## Step 9 — Write Scenarios + Assemble Report

**PROBABLE, PLAUSIBLE, POSSIBLE** — each must cite a driver, no hedging, include PROOF with number/date, one-sentence IF and BUT.

**PREFERABLE — IFTF Backcasting**: describe desired state as already achieved, then backcast through Civilizational → Strategic → Operational. End with LEVERAGE (single highest-leverage action today) and DRIVER.

**Decision guidance:**
- probable > 60: "Align with probable trajectory"
- plausible > 50: "Hedge between probable and plausible"
- possible > 40: "Maintain optionality"
- else: "Defer — insufficient signal clarity"

**MANDATORY output — all sections, every run:**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FORESIGHT INTELLIGENCE  ·  SOFT PREDICT
[Query]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PREDICTIONS
■ Probable  [[X]/100] [████████████░░░░░░░░] — [one sentence, no hedging]
■ Plausible [[X]/100] [████████░░░░░░░░░░░░] — [one sentence, no hedging]
■ Possible  [[X]/100] [████░░░░░░░░░░░░░░░░] — [one sentence, no hedging]
■ Preferable          [stakeholder analysis below]

Confidence: [X]/100  |  Signals: [N]  |  Horizon: [YYYY–YYYY]  |  [YYYY-MM-DD]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SIGNAL PULSE
Supporting [N] [████░░░░░░░░]  Opposing [N] [██░░░░░░░░░░]  Wild [N]
Net: [SUPPORTING LEADS / OPPOSING LEADS / NEUTRAL]
Hot zone: [dominant STEEEP×Temporal cell]
Gap: [uncovered categories or "None — full coverage"]

STRUCTURAL DRIVERS
D1 [Name] — [Force] ([LOCKED / SHIFTING / FRAGILE])
D2 [Name] — [Force] ([LOCKED / SHIFTING / FRAGILE])
D3 [Name] — [Force] ([LOCKED / SHIFTING / FRAGILE])

CROSS-IMPACT
Operational:    [status] — [explanation]
Strategic:      [status] — [explanation]
Civilizational: [status] — [explanation]
Friction: [pairs or "None detected"]

HISTORICAL MATCH
[Best analogue] ([similarity]% similar)
Tipped by: [event]  |  Equivalent now: [EXISTS/PARTIAL/ABSENT]  |  Validates: D[n]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

■ PROBABLE [[X]%] — [Title]
[2–3 sentences. No hedging.]
PROOF: [number or date]  |  IF: [condition]  |  BUT: [constraint]  |  DRIVER: D[n]

■ PLAUSIBLE [[X]%] — [Title]
[2–3 sentences]
PROOF: [number or date]  |  IF: [condition]  |  BUT: [constraint]  |  DRIVER: D[n]

■ POSSIBLE [[X]%] — [Title]
[2–3 sentences]
PROOF: [number or date]  |  IF: [condition]  |  BUT: [constraint]  |  DRIVER: D[n]

■ PREFERABLE — [Title]
[2–3 sentences: desired state as already achieved.]
BACKCAST
  Civilizational: [far horizon structural truth]
  Strategic:      [medium-term build]
  Operational:    [what begins NOW]
LEVERAGE: [specific actor, specific action]  |  DRIVER: D[n]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

PREFERABLE FUTURES  ·  Per stakeholder
[Player A]:
  Wins IF  → [condition]
  BUT ONLY → [constraint]
  ONLY THEN → [outcome]

[Users/Society]:
  Wins IF  → [condition]
  BUT ONLY → [constraint]
  ONLY THEN → [outcome]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

THE ONE THING
[Single variable that determines which scenario activates]
INCIDENT: [real past event]  |  WATCH: [leading indicator]
IF YES → [what accelerates]  |  IF NO → [what stalls]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

DECISION GUIDANCE
Stance: [from deterministic logic]
Low-regret move: [action that pays off across scenarios]
Risk trigger: [highest-scored opposing signal]

[REGIONAL LENS — [REGION]]
Top multipliers: [STEEEP/temporal]  Key local variable: [one sentence]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

If running on claude.ai with Artifacts enabled, also generate an HTML visual report after the text output (prediction bars, STEEEP matrix heatmap, futures cone SVG). Dark background #0f0f0f, accent #00d4aa. Inline CSS only.

---

# HARD PREDICT — 12-Step Deterministic Pipeline

**CRITICAL:** Claude handles intelligence. Python handles all arithmetic. Never skip a step. Never guess Python output. Always wait for exact stdout.

Scripts are at: `${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/`

---

## Step 1 — Validate (Python)
```
python "${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/input_validator.py" "[query]"
```
If `valid=false`: output rejection message and STOP. If `valid=true`: infer horizon and proceed.

## Step 2 — Collect Signals (Claude)
Same 6 searches as Soft Predict Step 2. Stop when signals ≥ 18 AND 4+ STEEEP categories covered.
Save to: `${CLAUDE_PLUGIN_ROOT}/signals.json`

## Step 3 — Score Signals (Python)
```
python "${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/signal_scorer.py" "${CLAUDE_PLUGIN_ROOT}/signals.json"
```
Wait for exact stdout JSON. Use returned data exactly. Script writes `scored_signals.json`.

## Step 4 — Extract Structural Drivers (Claude)
Same as Soft Predict Step 4. Extract 3 drivers from `scored_signals.json`.

## Step 5 — Build STEEEP Matrix (Python)
```
python "${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/matrix_builder.py" "${CLAUDE_PLUGIN_ROOT}/scored_signals.json"
```
Wait for exact stdout JSON. Script writes `matrix.json`.

## Step 6 — Cross-Impact Analysis (Claude)
Same logic as Soft Predict Step 6. Read `matrix.json`. Apply convergence bonus.

## Step 7 — Find Historical Analogues (Claude)
Same as Soft Predict Step 7. Save to: `${CLAUDE_PLUGIN_ROOT}/analogues.json`

## Step 8 — Compute Probabilities (Python)
```
python "${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/probability_calc.py" "${CLAUDE_PLUGIN_ROOT}/scored_signals.json" "${CLAUDE_PLUGIN_ROOT}/analogues.json"
```
Wait for exact stdout JSON. Apply convergence bonus: `adjusted_probable = min(100, probable + convergence_bonus)`. Script writes `probabilities.json`.

## Step 9 — Compute Confidence (Python)
```
python "${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/confidence_calc.py" "${CLAUDE_PLUGIN_ROOT}/scored_signals.json" "${CLAUDE_PLUGIN_ROOT}/matrix.json" "${CLAUDE_PLUGIN_ROOT}/analogues.json"
```
Wait for exact integer output.

## Step 10 — Decision Guidance (Python)
```
python "${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/decision_guidance.py" "${CLAUDE_PLUGIN_ROOT}/probabilities.json" "${CLAUDE_PLUGIN_ROOT}/matrix.json" "${CLAUDE_PLUGIN_ROOT}/scored_signals.json"
```
Wait for `guidance.json`.

## Step 11 — Write Scenarios (Claude)
Same structure as Soft Predict Step 9 scenarios: PROBABLE, PLAUSIBLE, POSSIBLE, PREFERABLE + THE ONE THING.

## Step 12 — Assemble + Format Report (Python)
Combine all outputs into `report_data.json` then:
```
python "${CLAUDE_PLUGIN_ROOT}/skills/foresight-intelligence/scripts/report_formatter.py" "${CLAUDE_PLUGIN_ROOT}/report_data.json"
```

Output template is identical to Soft Predict but header reads `HARD PREDICT` and includes STEEEP matrix with cell scores.

**Error handling:** Any Python script fails → report exact stderr, do not proceed. Never fabricate data.

---

## Regional Multiplier Tables

Apply in scoring and matrix steps.

### India
| | Operational | Strategic | Civilizational |
|---|---|---|---|
| Social | 1.10 | 1.30 | 1.20 |
| Technological | 1.40 | 1.30 | 1.10 |
| Economic | 1.20 | 1.25 | 1.15 |
| Environmental | 0.90 | 1.00 | 1.10 |
| Ethical | 0.95 | 1.00 | 1.05 |
| Political | 0.85 | 0.90 | 1.00 |

### USA
| | Operational | Strategic | Civilizational |
|---|---|---|---|
| Social | 1.00 | 1.10 | 1.05 |
| Technological | 1.20 | 1.40 | 1.20 |
| Economic | 1.10 | 1.30 | 1.10 |
| Environmental | 0.95 | 1.00 | 1.05 |
| Ethical | 1.05 | 1.10 | 1.10 |
| Political | 0.90 | 0.95 | 1.00 |

### Europe
| | Operational | Strategic | Civilizational |
|---|---|---|---|
| Social | 1.00 | 1.05 | 1.10 |
| Technological | 1.00 | 1.10 | 1.05 |
| Economic | 0.95 | 0.90 | 0.90 |
| Environmental | 1.20 | 1.40 | 1.30 |
| Ethical | 1.10 | 1.20 | 1.20 |
| Political | 1.05 | 1.10 | 1.10 |

### China
| | Operational | Strategic | Civilizational |
|---|---|---|---|
| Social | 1.00 | 1.10 | 1.05 |
| Technological | 1.20 | 1.50 | 1.30 |
| Economic | 1.10 | 1.20 | 1.10 |
| Environmental | 0.90 | 1.00 | 1.05 |
| Ethical | 0.70 | 0.75 | 0.80 |
| Political | 1.10 | 1.15 | 1.00 |

### Global (default)
All multipliers = 1.0. Apply when no region is detectable.
