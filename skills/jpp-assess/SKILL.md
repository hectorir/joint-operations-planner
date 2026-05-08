---
name: jpp-assess
description: Operation assessment plan. Builds MOEs / MOPs / indicators tied to objectives, effects, and tasks. Defines the assessment battle rhythm. Identifies the four plan-assessment outcomes (refine/adapt/terminate/execute). Use throughout planning — assessment starts at planning initiation, not execution.
---

# Operation Assessment

> Assessment is continuous and **starts with the initiation of joint planning**, not after execution begins. — JP 5-0 §11.1

## Inputs
- `01_mission_analysis/` (objectives, effects, mission statement)
- `06_plan/concept_of_operations.md` (if present)

## Doctrine to load
- `references/jp5-0-field-guide.md` §11 (entire — what it is, seven tenets, six-step process, hierarchy, four outcomes)
- `references/templates/assessment_plan.md`

## The assessment hierarchy (memorize)

```
Tasks → Conditions → Effects → Objectives → End State
  └── MOPs               └── MOEs
```

- **MOPs** answer "are we doing things right?" (task accomplishment).
- **MOEs** answer "are we doing the right things?" (effect creation, objective progress).
- **Indicators** are observable, collectable items that feed MOPs and MOEs.

## Process

1. **Develop the assessment approach** (§11.3 step 1) — informed by the operational design. State the commander's central question and how the assessment battle rhythm ties to the commander's decision cycle.
2. **Build the objective → effect → MOE table** in `assess/moes.md`. For each MOE, identify indicators and their source/collector.
3. **Build the task → MOP table** in `assess/mops.md`. Same pattern: each MOP has indicators and a collector.
4. **Consolidate indicators** in `assess/indicators.md`. This avoids duplication and gives intel/staff a single collection list.
5. **Tie to decision points** — a MOE that doesn't trigger any decision is decorative. List the trigger conditions.
6. **Set the battle rhythm** — Assessment Working Group cadence, Commander's Update Brief, etc. Synchronize with the commander's decision cycle (§11 tenet 4).
7. **Acknowledge the four outcomes** (§11.5):
   - Refine — orderly process; FRAGORDs in execution.
   - Adapt — major modifications driven by changes in strategic direction, OE, or problem.
   - Terminate — recommend termination; CPG/JSCP plans require approval to archive.
   - Execute — review the plan, validate assumptions, issue orders.

## Outputs

- `assess/moes.md`
- `assess/mops.md`
- `assess/indicators.md`

## Pitfalls

- **MOPs masquerading as MOEs.** "Number of patrols conducted" is a MOP, not a MOE. The MOE asks whether those patrols *created the desired effect*. Watch this carefully.
- **No collector named.** An indicator without a source is unobservable. Either name a collector or drop the indicator.
- **Battle rhythm decoupled from decision cycle.** §11 tenet 4 — if assessment doesn't reach the commander before the relevant decision, it's noise.
- **Assessment as a one-time product.** §11.7 — assessment is continuous; products may follow a schedule, but the activity does not stop.
