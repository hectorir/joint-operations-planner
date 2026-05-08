---
description: Where am I in this plan? Reports step status, gaps, unanswered CCIRs, and the recommended next action.
argument-hint: [plan-name]
---

Run the `jpp-status` skill.

Read `~/joint-plans/$1/manifest.yaml` (or, if no argument, list plans under `~/joint-plans/` and ask the planner to pick). Then walk every step folder and produce a status report per the format in `skills/jpp-status/SKILL.md`.
