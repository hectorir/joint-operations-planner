---
name: jpp-plan-development
description: JPP Step 7 — Plan or Order Development. Produces the CONOPS (centerpiece) and, at BPLAN level, major forces / support concept / timeline. Surfaces shortfalls. Final §13.5 plan check is part of this step. Use after Step 6.
---

# JPP Step 7 — Plan or Order Development

## Inputs
- `05_approval/decision.md` (the approved COA)
- `02_coas/<approved-coa>.md`
- `cog/`, `assess/`, `03_wargame/decision_support.md`
- `01_mission_analysis/mission_statement.md`

## Doctrine to load
- `references/jp5-0-field-guide.md` §5.8 (force/support/deployment planning, transition)
- §5.8.1 (main effort & supporting efforts)
- §5.8.2 (transition)
- §4 (planning products & orders)
- §4.3 (5-paragraph format)
- §13.5 (final plan check)

Also: `references/templates/conops.md`, `references/rubrics/plan.md`.

## Process

### A. CONOPS (always — both Estimate and BPLAN)

1. Open `06_plan/concept_of_operations.md` from the conops template.
2. Pull the mission statement verbatim from `01_mission_analysis/mission_statement.md`.
3. Write commander's intent (purpose, key tasks, end state) — derived from the approved COA.
4. Write the concept of operation:
   - General approach (direct/indirect, mechanism).
   - Phasing — **condition-driven, not time-driven** (general rule §7.9). Each phase's ending conditions = next phase's starting conditions.
   - Sequencing (simultaneous, sequential, combination).
   - Main effort and supporting efforts per phase (when main effort shifts, support priorities shift).
   - Decision points, branches, sequels carried forward from `03_wargame/decision_support.md`.
5. Tasks to subordinate units.
6. Coordinating instructions (CCIRs, ROE references, battle rhythm).
7. Risk paragraph — both flavors, civilian-script-ready (§13.6).

### B. BPLAN-only artifacts (level == bplan)

Read manifest's `plan.level`. If `bplan`:

1. **Major forces** (`major_forces.md`) — task org sourcing concept; mission-priority sequencing.
2. **Support concept** (`support_concept.md`) — concept of logistics support, key supportability conclusions, key assumptions.
3. **Timeline** (`timeline.md`) — phase boundaries with the conditions that trigger transitions; key dates if any are externally fixed.

If `estimate`, skip these.

### C. Shortfalls (always)

`shortfalls.md` — list every shortfall identified in wargaming with proposed mitigation. Plan development does not halt awaiting resolution (§5.8); this is the public list.

### D. Final §13.5 plan check

Run the §13.5 checklist. Specifically the two-line test:
1. Plan achieves the objective / attains the end state within acceptable risk?
2. Plan does **not foreclose future options**?

If either fails, the step stays `in_progress` and the issue goes to `log/changes.md`.

### E. Self-critique

Run `references/rubrics/plan.md`. Any FAIL blocks step completion.

### F. Optionally generate the OPORD shell

If the planner wants the 5-paragraph order, invoke `/jp-generate oporder` to produce `06_plan/oporder.md` from `references/templates/oporder_5para.md`.

## Outputs

- `06_plan/concept_of_operations.md` (always)
- `06_plan/major_forces.md`, `support_concept.md`, `timeline.md` (BPLAN only)
- `06_plan/shortfalls.md` (always)
- `06_plan/oporder.md` (optional, on request)

## Out of scope (v1)

- TPFDD/TPFDL — at all levels. The skill teaches the considerations but does not produce force-flow data.
- CONPLAN/OPLAN annexes A–Z. Levels 3–4 are deferred to a future version.

## Pitfalls

- **Time-driven phasing.** Phases bounded by dates with no ending conditions. Push back per §7.9.
- **Main effort that doesn't shift support priorities.** §5.8.1 — when the main effort moves, support must move with it. Catch this in the sync matrix.
- **Risk paragraph that doesn't separate flavors.** §10 requires both — risk-to-mission AND risk-to-force.
- **Foreclosing future options.** Common failure: committing the strategic reserve, exhausting political capital. The §13.5 second line is non-negotiable.
