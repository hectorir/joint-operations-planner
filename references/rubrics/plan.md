# Rubric — Final Plan Critique

> Used by `/jp-critique --step plan` against `06_plan/`. Includes the §13.5 two-line test.

## R-PLAN-01 — CONOPS contains commander's intent (purpose, key tasks, end state)
- **Doctrine:** JP 5-0 §5.8
- **FAIL** if any of the three intent elements missing.

## R-PLAN-02 — Phasing is condition-driven, not time-driven (general rule)
- **Doctrine:** JP 5-0 §7.9 (phasing)
- **WARN** if phases are bounded by dates only, with no ending conditions defined.

## R-PLAN-03 — Each phase's ending conditions are the next phase's starting conditions
- **Doctrine:** JP 5-0 §7.9
- **FAIL** if there are gaps or contradictions between adjacent phases' conditions.

## R-PLAN-04 — Main effort and supporting efforts named per phase
- **Doctrine:** JP 5-0 §5.8.1
- **FAIL** if any phase lacks a main effort. **WARN** if main-effort shifts don't shift support priorities.

## R-PLAN-05 — Joint functions addressed and reinforcing
- **Doctrine:** JP 5-0 §13.5
- **FAIL** if any joint function (C2, Information, Intelligence, Fires, Movement & Maneuver, Protection, Sustainment) is unaddressed.

## R-PLAN-06 — Decision points, branches, sequels carried forward from wargame
- **Doctrine:** JP 5-0 §5.8, §7.9
- **WARN** if the plan does not reference DPs/branches/sequels established in `03_wargame/decision_support.md`.

## R-PLAN-07 — Sustainment concept present (BPLAN only)
- **Doctrine:** JP 5-0 §5.8 (force/support/deployment planning)
- **FAIL** at BPLAN level if `06_plan/support_concept.md` is missing or empty.
- **N/A** at Estimate level.

## R-PLAN-08 — Risk articulated for both flavors
- **Doctrine:** JP 5-0 §10
- **FAIL** if the plan's risk paragraph does not separately address risk-to-mission and risk-to-force.

## R-PLAN-09 — Shortfalls identified, not hidden
- **Doctrine:** JP 5-0 §5.8 (shortfall identification)
- **WARN** if `shortfalls.md` is empty (real plans have shortfalls); **PASS** if shortfalls are real and have proposed mitigations.

## R-PLAN-10 — §13.5 two-line test
- **Doctrine:** JP 5-0 §13.5; field guide §1
- **FAIL #1:** Plan does not achieve the objective / attain the end state within acceptable risk.
- **FAIL #2:** Plan **forecloses future options** (e.g., commits the only strategic reserve, exhausts political capital, locks in a posture that prevents pivot).

## R-PLAN-11 — Plan does not violate principles of joint operations
- **Doctrine:** JP 5-0 §13.5; cross-ref to JP 3-0 (principles).
- **WARN** on visible violations (e.g., unity of command compromised; objective subordinated to means).
