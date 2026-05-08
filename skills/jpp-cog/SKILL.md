---
name: jpp-cog
description: COG / critical-factors analysis (cross-cuts JPP steps). Identifies the COG, decomposes critical capabilities → requirements → vulnerabilities, derives decisive points. Use during mission analysis, revisited as the OE shifts.
---

# COG / Critical-Factors Analysis

> "COG identification is a linchpin in the planning effort." — JP 5-0 §8.1

## Inputs
- `01_mission_analysis/` (especially mission statement, tasks, OE description)
- `context.md`

## Doctrine to load
Read **§8 entire** from `references/jp5-0-field-guide.md`:
- §8.1 — why it matters
- §8.2 — key principles (adversarial context, change over time, levels of war, multiple COGs possible, peacetime exception)
- §8.3 — critical-factors framework
- §8.4 — identifying a COG (analyst's playbook)
- §8.5 — attacking a COG (target trade-offs)
- §8.6 — five completion questions

Also: `references/templates/cog_critical_factors.md`, `references/rubrics/cog.md`.

## Process

Ask the planner: friendly COG, threat COG, or both?

For each:

1. **Establish the adversarial context.** No adversarial relationship = no COG. If the planner is in peacetime/shaping, document why an enemy COG may be absent.

2. **Tie to objective and end state.** The COG must serve a specific objective. Cross-reference the mission statement.

3. **Identify the COG.** Apply the §8.4 playbook:
   - Identify the actor's critical strengths.
   - Decompose how the actor organizes, fights, thinks, decides — physical AND psychological.
   - Avoid mirror-imaging.
   - Test: would defeat/destruction/neutralization cause the actor to abandon objectives or change COA?

4. **Decompose into critical factors** per §8.3:
   - **Critical Capabilities** — primary abilities essential to mission accomplishment.
   - **Critical Requirements** — what each CC needs to function.
   - **Critical Vulnerabilities** — aspects of CRs vulnerable to attack.

5. **Derive decisive points** — keys to attacking or protecting the COG. Decisive points are usually **not** the COG itself.

6. **Apply attack discipline** (§8.5). For each CV, score:
   - Criticality to the COG
   - Accessibility (can we reach it?)
   - Redundancy / resiliency (will the adversary route around it?)
   - Escalation risk and impact on other objectives.

7. **Choose direct vs indirect approach** (§7.7):
   - Direct → target the COG itself (requires positional strength).
   - Indirect → target critical vulnerabilities (preferred against well-protected COGs or from a position of disadvantage).

8. **Run the five completion questions** (§8.6) at the bottom of the file.

## Outputs

- `cog/friendly.md` and/or `cog/threat.md`
- A pointer note in `01_mission_analysis/cogs.md` if invoked from inside mission analysis.

## Self-critique

Walk `references/rubrics/cog.md`. Watch especially for:
- Mirror-imaging (R-COG-05)
- Decisive points labeled as COGs (R-COG-09)

## Pitfalls

- **Confusing decisive points with COGs.** Decisive points are *keys* to the COG, not the COG. (§8.5)
- **Listing the adversary's every weakness as "vulnerabilities."** Critical vulnerabilities trace specifically from critical requirements.
- **Treating the COG as static.** COGs change over time as the strategic environment, OE, or relative power shifts (§8.2). If you've inherited a COG analysis from an earlier draft, re-test it.
- **Forgetting friendly-COG protection.** Question 5 in §8.6: should we strengthen or protect *our own* COG (alliance cohesion, public will, interoperability)?
