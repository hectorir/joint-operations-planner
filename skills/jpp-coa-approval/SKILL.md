---
name: jpp-coa-approval
description: JPP Step 6 — COA Approval. Captures the commander's selection (one of six options), modifications, and an explicit statement of acceptable risk. Produces the decision document. Use after Step 5.
---

# JPP Step 6 — COA Approval

## Inputs
- `04_comparison/comparison_matrix.md`
- `02_coas/` (all COAs)
- `03_wargame/` (decision support, identified shortfalls)

## Doctrine to load
- `references/jp5-0-field-guide.md` §5.7 (commander's six options)
- §10.4 (risk articulation)
- §13.6 (civilian-leader risk script)

## Process

1. Open `05_approval/decision.md` from `references/templates/decision.md`.
2. Ask the planner: which of the six options is the commander exercising?
   1. Concur as presented.
   2. Concur with modifications.
   3. Select a different COA.
   4. Combine COAs to create a new COA.
   5. Reject all and restart at COA development or mission analysis.
   6. Defer the decision.
3. If 4 (combine), open a new COA file `coa-NN-combined-<short-name>.md` and re-run validity tests. Do not skip — a combined COA is a new COA and must pass the 5 tests.
4. If 5 (reject all), set the relevant downstream steps to `pending`, mark this approval `pending`, and tell the planner which step they're re-entering.
5. Write the **decision statement** in plain language (one paragraph). It should name the COA, state any modifications, and direct the staff to begin Step 7.
6. Write the **acceptable risk** section. Both flavors:
   - Risk-to-mission (operational risk)
   - Risk-to-force (force management risk)
   - Residual risk after mitigation
7. Write the **rationale** (2–3 paragraphs in commander's voice).
8. Update manifest: `approved_coa: coa-NN`; mark all other COAs `selected: false`.
9. Self-critique: confirm the decision statement is plain language (not bureaucratic) and that residual risk is named.

## Outputs

- `05_approval/decision.md`
- `manifest.yaml` updated with `approved_coa`

## Pitfalls

- **Risk paragraph absent or generic.** Doctrine §10 requires explicit articulation; if the commander accepts risk silently, the staff has failed.
- **Residual risk not named.** Risk acceptance must be explicit (§10.3).
- **Skipping option (5) re-entry mechanics.** If the commander rejects all COAs, the manifest must reflect the re-entry — don't pretend the prior steps still hold.
