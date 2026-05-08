---
name: jpp-generate
description: Generate a planning artifact from current plan-dir state. Reads relevant step files, fills the matching template, asks the planner for missing fields, writes the artifact. Use when you want a deliverable (mission analysis brief, CONOPS, OPORD shell, comparison matrix, risk assessment, assessment plan, transition brief).
---

# JPP Generate

## Inputs

- The plan-dir files relevant to the requested artifact.
- The matching template in `references/templates/`.

## Artifact catalog

| Artifact | Argument | Reads | Template | Writes to |
|---|---|---|---|---|
| Mission analysis brief | `mission-brief` | `01_mission_analysis/`, `cog/`, `00_initiation/` | `mission_analysis_brief.md` | `01_mission_analysis/mission_analysis_brief.md` |
| CONOPS | `conops` | approved COA, `cog/`, `assess/`, `03_wargame/decision_support.md` | `conops.md` | `06_plan/concept_of_operations.md` |
| OPORD (5-paragraph) | `oporder` | CONOPS, mission statement, task org | `oporder_5para.md` | `06_plan/oporder.md` |
| Comparison matrix | `comparison-matrix` | `02_coas/`, `coa_evaluation_criteria.md`, wargame outputs | `comparison_matrix.md` | `04_comparison/comparison_matrix.md` |
| Decision document | `decision` | comparison matrix, all COAs | `decision.md` | `05_approval/decision.md` |
| Risk assessment | `risk-assessment` | step-relevant risk content | `risk_assessment.md` | per-step or standalone |
| Assessment plan | `assessment-plan` | mission analysis (objectives/effects), CONOPS | `assessment_plan.md` | `assess/` (split across moes/mops/indicators) |
| Transition brief | `transition-brief` | full plan dir | (inline format from §5.8.2 / §12.2) | `06_plan/transition_brief.md` |

## Doctrine

- §4 (planning products & orders) for OPORDs and order types
- §4.3 (5-paragraph format)
- §5.8 (plan development outputs)
- Specific section per artifact (cited in the template).

## Process

1. Determine the artifact requested. Argument `$1` or ask.
2. Read the relevant plan-dir files. Note any missing sections needed by the template.
3. Open the template; fill what you can from existing plan content. Quote when appropriate.
4. For each missing field, ask the planner one at a time. Don't fabricate.
5. Write the artifact to its destination.
6. Update manifest where applicable (e.g., generating the CONOPS doesn't change `steps.plan_development.status`; that's the per-step skill's job).
7. Tell the planner where the file lives.

## Pitfalls

- **Fabricating content.** If the plan dir doesn't have it, ask the planner. Never invent.
- **Overwriting existing artifacts without confirmation.** If the destination file exists and has substantive content, ask before overwriting.
- **Using a template that doesn't fit the plan level.** OPORDs at Estimate level are uncommon; if level is `estimate`, confirm before producing.
