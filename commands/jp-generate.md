---
description: Generate a planning artifact (mission analysis brief, CONOPS, OPORD shell, comparison matrix, etc.) from current plan-dir state.
argument-hint: [artifact-type]
---

Run the `jpp-generate` skill.

Argument `$1` (optional): one of `mission-brief`, `conops`, `oporder`, `comparison-matrix`, `decision`, `risk-assessment`, `assessment-plan`, `transition-brief`. If omitted, ask the planner which artifact.

The skill reads the relevant plan-dir files, opens the matching template under `references/templates/`, fills it with current plan content (asking the planner for any missing fields), and writes the artifact to the appropriate step folder.
