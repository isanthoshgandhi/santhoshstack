---
name: usability-heuristics
description: >
  Audit any system for human usability against Nielsen's 10 heuristics.
  Deterministic checklist — same 10 heuristics, same severity scale, same
  report structure every run. Works on UI screens, CLI flows, API response
  patterns, user journeys, component code, or any described interface. Invoke
  when user says "usability audit", "UX review", "heuristic evaluation",
  "audit for usability", "check this for UX issues", or /usability-heuristics.
---

# Usability Heuristics Audit

You are running a deterministic usability audit. Apply all 10 Nielsen-Norman
heuristics as a structured checklist. Findings are evidence-based — a violation
must be traceable to a specific screen, component, flow step, or code location.
Do not generate hypothetical issues. Do not produce style or aesthetic opinions.

---

## Step 1: Establish Audit Scope

Ask the user (one question, wait for response):

"What are we auditing? Options:
- UI screens or mockups (paste screenshots, describe flows, or share files)
- Component code (share the file paths)
- A CLI or terminal interface (describe the commands and output)
- An API interaction pattern (request/response shapes, error messages)
- A user journey or task flow (describe it step by step)
- Something else — describe it"

If the user has already described the system in their prompt, skip this and
begin the audit immediately using what they provided.

Also establish (from context or ask if not clear):
- Who are the primary users? (technical experts, first-time users, general public)
- What is the primary task users are trying to complete?

---

## Step 2: Run the 10-Heuristic Checklist

Evaluate the system against each heuristic in order. For each heuristic, list
every violation found. If none, mark it PASS. Do not skip any heuristic.

Use this evaluation block for each:

```
H[N]: [HEURISTIC NAME]
Status: PASS | [N] ISSUES
---
[For each issue:]
  Location: [screen name / component / step / file:line]
  Violation: [one sentence — what rule is broken and how]
  Severity: CRITICAL | HIGH | MEDIUM | LOW
  Fix: [exact corrective action]
```

### The 10 Heuristics

#### H1: Visibility of System Status
The system must always inform users of what is going on through timely,
appropriate feedback.

Check for:
- Missing loading/progress states during operations that take time
- No confirmation that an action completed (save, submit, delete)
- Status indicators that exist but are hidden, tiny, or easy to miss
- Asynchronous operations with no feedback at all
- Progress bars or spinners that appear but never update or never disappear

#### H2: Match Between System and the Real World
Language, icons, and workflows must align with users' mental models — not
internal naming conventions or developer terminology.

Check for:
- Technical jargon, error codes, or system-internal labels exposed to users
- Icons that don't match universal conventions (e.g., non-standard "save" icon)
- Workflows that break natural cause-and-effect order
- Date/time formats mismatched to user locale
- Labels that mean one thing in the domain and another to a general user

#### H3: User Control and Freedom
Users make mistakes and need clearly marked exits. Undo and redo must be easy
to find and use.

Check for:
- Destructive actions (delete, overwrite, send) with no undo or confirmation
- Modal dialogs or states the user cannot exit without completing an action
- Multi-step flows with no way to go back to a prior step
- No "cancel" option during long operations
- Session timeouts that discard in-progress work without warning

#### H4: Consistency and Standards
The same words, icons, colors, and interaction patterns must mean the same
thing everywhere in the system.

Check for:
- Same action labeled differently in different parts of the UI (e.g., "Remove"
  vs "Delete" vs "Clear" for the same operation)
- Platform conventions violated (e.g., right-click doing nothing on a web app)
- Inconsistent button placement across similar screens
- Color used to mean different things in different contexts
- Inconsistent capitalization, punctuation, or tone in copy

#### H5: Error Prevention
Design must prevent errors before they occur — not just recover from them.
Preference order: eliminate the error condition, then constrain input, then warn.

Check for:
- Free-text fields that accept obviously invalid input without constraint
- Confirmation dialogs missing for irreversible high-impact actions
- Form submission allowed when required fields are empty or invalid
- Ambiguous affordances that invite the wrong interaction
- Options that look selectable but are not (without explanation)

#### H6: Recognition Rather Than Recall
Users should not have to remember information from one screen to use another.
Options, actions, and objects should be visible or easily retrievable.

Check for:
- Users required to memorize IDs, codes, or values from a previous step
- Actions available only via keyboard shortcuts with no visual indicator
- Context lost when navigating between screens (e.g., current filters disappear)
- Long menus with no search or grouping — user must scan everything
- "Blank slate" states that give no hint of what the user can do next

#### H7: Flexibility and Efficiency of Use
Interfaces must serve both novices and experts. Accelerators should exist but
not get in the way.

Check for:
- No keyboard shortcuts for power users performing repetitive tasks
- No way to set defaults or preferences for frequently used options
- Bulk actions missing when users regularly need to act on multiple items
- Expert-only features buried so deep novices can never find them
- Novice-oriented confirmations and wizards that cannot be bypassed by experts

#### H8: Aesthetic and Minimalist Design
Every piece of information in the UI competes for attention. Remove anything
that doesn't serve the user's primary goal on that screen.

Check for:
- Competing CTAs with no clear primary action
- Decorative elements that reduce signal-to-noise without adding value
- Dense information blocks that should be progressive-disclosed
- Marketing or promotional copy mixed into task-completion flows
- Redundant labels that state what the input field's placeholder already says

#### H9: Help Users Recognize, Diagnose, and Recover from Errors
Error messages must be in plain language, identify the exact problem, and tell
the user what to do next.

Check for:
- Error messages that show raw codes, stack traces, or internal identifiers
- Generic messages: "Something went wrong", "Error 500", "Request failed"
- Errors that identify the problem but don't tell the user what to do
- Error messages not visually distinct from normal UI (wrong color, no icon)
- Inline validation errors that only appear after final submission, not at input

#### H10: Help and Documentation
Even well-designed systems sometimes need help. Documentation should be easy
to find, task-focused, and actionable.

Check for:
- No help, tooltip, or onboarding for non-obvious or first-time actions
- Help content that is generic rather than tied to the current task context
- Documentation that describes UI elements rather than how to complete tasks
- Help that is only available from a separate, hard-to-find help center
- Empty error states or blank screens with no guidance on next steps

---

## Step 3: Severity Rating Criteria

Apply these criteria consistently — severity is not a gut feeling.

| Severity | Definition |
|----------|------------|
| CRITICAL | Blocks the user from completing the primary task. Cannot proceed without workaround or assistance. |
| HIGH | Causes repeated frustration or significant effort. Most users will notice and struggle. |
| MEDIUM | Causes friction for some users or in specific scenarios. Reduces efficiency. |
| LOW | Minor polish issue. Affects delight or edge-case users but does not impede normal use. |

---

## Step 4: Produce the Audit Report

Output the report in this exact structure. Do not vary the structure between
runs — determinism is the point.

```
USABILITY HEURISTICS AUDIT
System: [name/description of what was audited]
User: [primary user type]
Primary task: [what they're trying to do]
Date: [current date]
Evaluator: Claude (Heuristic audit per Nielsen-Norman Group, 1994/2005)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
HEURISTIC SCAN
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

H1 Visibility of System Status         [PASS | N issue(s)]
H2 Match Between System and Real World [PASS | N issue(s)]
H3 User Control and Freedom            [PASS | N issue(s)]
H4 Consistency and Standards           [PASS | N issue(s)]
H5 Error Prevention                    [PASS | N issue(s)]
H6 Recognition Rather Than Recall      [PASS | N issue(s)]
H7 Flexibility and Efficiency of Use   [PASS | N issue(s)]
H8 Aesthetic and Minimalist Design     [PASS | N issue(s)]
H9 Recognize, Diagnose, Recover Errors [PASS | N issue(s)]
H10 Help and Documentation             [PASS | N issue(s)]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
FINDINGS (severity-sorted)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

[CRITICAL — list all CRITICAL findings first]
[HIGH — then HIGH]
[MEDIUM — then MEDIUM]
[LOW — then LOW, limit to 3 max; note count of remaining]

Each finding:
  [SEVERITY] H[N] · [Location]
  Violation: [what is broken and why it violates the heuristic]
  Fix:       [precise corrective action]

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
SUMMARY
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Total issues: [N] (C:[n] H:[n] M:[n] L:[n])
Heuristics with most violations: [list top 2-3]
Worst area of the system: [location with the most issues]

Top 3 fixes (highest impact, simplest to implement):
1. [fix]
2. [fix]
3. [fix]
```

---

## Rules

- Every heuristic must appear in the report — no skipping even if no issues found
- Findings must trace to a specific location (screen, component, step, file:line)
- Do not generate more than 15 total findings — depth over breadth
- Do not add design opinions outside the 10 heuristics
- Do not quote large code blocks — use file:line references
- If a finding could belong to two heuristics, assign it to the primary one only
- If the system cannot be evaluated on a heuristic (e.g., a static diagram has no
  error states), mark it N/A with a one-line reason
