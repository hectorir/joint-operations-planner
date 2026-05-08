---
name: jpp-mission-analysis
description: JPP Step 2 — Mission Analysis. The most important step of the JPP. Walks the planner through the 14 mission analysis activities and produces the full set of mission analysis artifacts. Use after Step 1 is complete.
---

# JPP Step 2 — Mission Analysis

> "Mission analysis lays the foundation for everything that follows." — JP 5-0 §5.3.

## Inputs
- `00_initiation/` (all files)
- `context.md`
- `manifest.yaml`
- Optional: profile

## Doctrine to load
Read these sections from `references/jp5-0-field-guide.md`:
- **§5.3 entire** — the heart of this skill (14 activities, facts/assumptions, constraints/restraints, S/I/E tasks, mission statement template, CCIRs, risk scaffolding)
- **§2.4** — understanding problems before solving them
- **§13.1** — pre-planning checklist
- **§13.2** — mission analysis hygiene checklist

Also load the relevant rubric: `references/rubrics/mission_analysis.md`.

## Process — the 14 activities

Run these as a guided dialogue. They are not strictly sequential; some run concurrently. Track what's been captured against the list and surface gaps.

1. **Begin logistics supportability analysis.** Ask whether logistics has been engaged; capture early supportability concerns. (Output captured later in `01_mission_analysis/risk_assessment_initial.md` and during plan development.)
2. **Analyze higher HQ planning activities and strategic guidance.** Cross-reference `00_initiation/strategic_guidance.md`. Note one-up and two-up mission/intent.
3. **Review commander's initial planning guidance.** From `00_initiation/initial_planning_guidance.md`.
4. **Determine known facts and develop planning assumptions.** Write `01_mission_analysis/facts.md` and `assumptions.md`. For each assumption, identify a CCIR that validates it (forward-link to step 12). Apply the §5.3.1 discipline — minimum required, never assume away adversary capabilities.
5. **Determine and analyze operational limitations.** Distinguish constraints ("must do") from restraints ("cannot do"). Write `01_mission_analysis/constraints_restraints.md`.
6. **Determine specified, implied, and essential tasks.** Write `01_mission_analysis/tasks.md` with three explicitly-labeled sections. Apply §5.3.3: implied tasks exclude routine actions (recon, flank protection); essential tasks must succeed for the directed end state.
7. **Develop mission statement.** Use the template at `references/templates/mission_statement.md`. Verify all five elements (who/what/when/where/why) and that the purpose clause is explicit. Write to `01_mission_analysis/mission_statement.md`.
8. **Conduct initial force identification.** Light pass: what kinds of forces and capabilities will likely be needed? Note in `01_mission_analysis/risk_assessment_initial.md` (logistics implications).
9. **Develop risk assessment.** Use the template at `references/templates/risk_assessment.md`. Address both risk-to-mission and risk-to-force. Apply §5.3.6 P×C scaffolding. Write to `01_mission_analysis/risk_assessment_initial.md`.
10. **Develop COA evaluation criteria.** Define 4–7 criteria with measurable definitions and weights. These will drive Step 5 comparison. Write to `01_mission_analysis/coa_evaluation_criteria.md`.
11. **Develop initial military objectives.** Objectives are clearly defined, decisive, attainable, single results — they do not imply ways or means and are not tasks (§7.2). Capture in `01_mission_analysis/operational_approach.md` (refined from initiation).
12. **Develop CCIRs.** Use the template at `references/templates/ccirs.md`. Separate PIRs from FFIRs. Each must tie to a decision point and have an LTIOV. Cross-link assumptions from step 4 to validating CCIRs.
13. **Prepare staff estimates.** (Out of scope to fully run; note as a deliverable that staff sections must produce.)
14. **Prepare and deliver mission analysis brief.** Use the template at `references/templates/mission_analysis_brief.md`. Generate via `/jp-generate mission-brief` when ready.
15. **Publish updated planning guidance, intent statement, and refined operational approach.** Update `01_mission_analysis/operational_approach.md`.

In parallel: kick off **COG analysis** for both friendly and threat. Invoke `/jp-cog` (or do it inline using the §8 doctrine and the cog template). Write to `cog/friendly.md` and `cog/threat.md`. Cross-reference from `01_mission_analysis/cogs.md` (a thin pointer file).

Also kick off **assessment plan** drafting. Invoke `/jp-assess` for initial MOEs/MOPs/indicators tied to the early objectives — assessment starts at planning initiation, not after execution (§11.1).

## Outputs

- `01_mission_analysis/facts.md`
- `01_mission_analysis/assumptions.md`
- `01_mission_analysis/constraints_restraints.md`
- `01_mission_analysis/tasks.md`
- `01_mission_analysis/mission_statement.md`
- `01_mission_analysis/ccirs.md`
- `01_mission_analysis/cogs.md` (pointer file)
- `01_mission_analysis/risk_assessment_initial.md`
- `01_mission_analysis/coa_evaluation_criteria.md`
- `01_mission_analysis/operational_approach.md` (refined from Step 1)
- `cog/friendly.md`, `cog/threat.md`
- Initial entries in `assess/`
- `manifest.yaml` updated; mission analysis brief produced via `/jp-generate` when planner asks

## Self-critique gate

Before transitioning `steps.mission_analysis.status` to `complete`, mentally walk the rubric `references/rubrics/mission_analysis.md`. If any FAIL exists, leave the step `in_progress`, log the issue in `log/changes.md`, and tell the planner what to fix. WARN-level issues are surfaced but don't block.

## Commit message

`step:mission-analysis complete` (or `step:mission-analysis in-progress`)

## Pitfalls

- **Mission statement without explicit purpose.** Common error — subordinate intent inference depends on the *why*. Don't accept "to defeat the enemy" as a purpose; that's a task.
- **Tasks list with mis-categorized items.** Routine flank security listed as "implied" — that's a category error per §5.3.3.
- **Long CCIR list.** If you've got more than ~10 PIRs+FFIRs, consolidate. Long lists don't drive collection — they paralyze it.
- **Assumption inflation.** Each assumption adds error and bias (§5.3.1). Push back on every assumption that isn't *essential* for planning to continue.
- **Mirror-imaging the threat COG.** A rational adversary decision may look irrational from the friendly perspective (§8.4). Watch for COG analysis that frames the enemy as a degraded version of "us."
