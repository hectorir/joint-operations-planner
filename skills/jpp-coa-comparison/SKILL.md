---
name: jpp-coa-comparison
description: JPP Step 5 — COA Comparison. Evaluates each COA independently against each evaluation criterion (not COAs against each other). Produces the comparison matrix and a staff recommendation. Use after wargaming.
---

# JPP Step 5 — COA Comparison

## Inputs
- `02_coas/` (each retained COA)
- `01_mission_analysis/coa_evaluation_criteria.md`
- `03_wargame/` (post-wargame validity, identified shortfalls, refined CCIRs)

## Doctrine to load
- `references/jp5-0-field-guide.md` §5.6

## Process

1. Open `04_comparison/comparison_matrix.md` from `references/templates/comparison_matrix.md`.
2. Confirm with the planner the comparison method:
   - Numerical with weights (most common; defensible)
   - Descriptive
   - Plus/minus/neutral (Appendix F)
3. Score each COA **independently** against each criterion. Do not score "COA-1 vs COA-2"; score "COA-1 against criterion X" then "COA-2 against criterion X."
4. Compute weighted totals.
5. Answer the three §5.6 questions:
   - What are the differences between each COA?
   - What are the advantages and disadvantages?
   - What are the risks?
6. Write a one-paragraph staff recommendation. Make explicit that the commander is not bound by it (§5.7 six options).

## Outputs

- `04_comparison/comparison_matrix.md`
- Manifest updated: `steps.coa_comparison.status`

## Pitfalls

- **Direct head-to-head scoring.** Doctrinally wrong (§5.6). Each COA stands alone against each criterion.
- **Hidden weights.** If criteria are weighted, the weights must be visible in the matrix.
- **Recommendation that ignores wargame results.** A COA that survived comparison but produced major shortfalls in wargaming should be flagged in the recommendation, not buried.
