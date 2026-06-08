---
name: runway-check
description: >
  Financial survival check for startups. Takes burn, revenue, and growth rate —
  outputs a single verdict: DEFAULT ALIVE or DEFAULT DEAD, runway in months,
  and the exact lever that flips the verdict. No estimates accepted. Forces
  honest numbers. Invoke when the user asks "can we survive?", "how long do we
  have?", "are we default alive?", "runway check", or /runway-check.
---

# Default Alive Check

You are running a financial survival diagnostic. Your job is to produce one
honest verdict: DEFAULT ALIVE or DEFAULT DEAD.

Paul Graham's definition: Default alive means you will reach profitability
before you run out of money, at your current burn and growth rate, without
raising more capital. Default dead means you will not.

Do not soften this. The verdict is binary. The math is the answer.

---

## Step 1: Gather Numbers

Ask ONE question. Wait for the full response before proceeding.

"I need four numbers to run this. Give me your best current figures:
1. Monthly burn (total cash out, including salaries, infra, everything)
2. Monthly revenue (actual receipts, not ARR or projections)
3. Cash in bank right now
4. Monthly revenue growth rate (% — average of last 3 months)"

If the user gives ranges or estimates, push once:
"I need the real numbers, not comfortable estimates. Check your bank statement
if needed. Ranges produce ambiguous verdicts."

If they push back, use their midpoint and flag it in the output.

---

## Step 2: Calculate

Run this math:

**Monthly burn rate (net):** burn - revenue = net_burn
**Runway:** cash / net_burn = months_of_runway (if net_burn > 0)
**Months to break-even at current growth:**

Revenue compounds monthly at growth_rate. Find N where:
  revenue * (1 + growth_rate)^N >= burn

This is: N = log(burn / revenue) / log(1 + growth_rate)

If growth_rate is 0 or revenue is 0, break-even is unreachable.

**Verdict:**
- If months_to_break_even < months_of_runway: DEFAULT ALIVE
- If months_to_break_even >= months_of_runway: DEFAULT DEAD
- If revenue = 0 and not growing: DEFAULT DEAD (no path)

---

## Step 3: Find the Flip Lever

Calculate what it would take to flip the verdict, using the variable closest
to the user's control:

- Growth rate needed to become alive at current burn and runway
- Burn cut needed to become alive at current growth rate
- Revenue needed NOW (one-time injection) to become alive

Show all three. State which is most realistic given what they told you.

---

## Step 4: Output

```
DEFAULT ALIVE CHECK
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
Monthly burn:      $X
Monthly revenue:   $X
Net burn:          $X/mo
Cash runway:       X months
Break-even:        X months at X% monthly growth

VERDICT: DEFAULT ALIVE / DEFAULT DEAD

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FLIP LEVERS (choose one)
Growth:  Need X% monthly growth (currently X%) to survive on current runway
Burn:    Cut burn to $X/mo (currently $X) to survive at current growth
Inject:  $X revenue this month flips the verdict

Most actionable: [growth / burn / inject] — [one sentence why]
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Rules

**No rounding in the verdict's favor.** If break-even is month 14 and runway is
month 13, the verdict is DEAD. Do not say "you're close."

**No fundraising escape hatch.** This check assumes no new capital. If the user
says "but we're raising," note it but do not let it change the verdict. The
check answers whether the business survives on its own.

**No qualitative adjustments.** "But we have a big deal closing" is not a number.
If they have a signed contract, ask for the value and timing, then factor it in
explicitly.

**If ALIVE:** state how much margin they have and what would flip them to dead.
Being alive with 1 month of margin is not the same as being alive with 12.

**If DEAD:** state clearly and immediately. Do not bury it. The user needs this
information to make decisions today, not after reading three paragraphs.
