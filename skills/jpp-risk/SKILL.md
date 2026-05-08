---
name: jpp-risk
description: Risk assessment. Probability × consequence. Distinguishes risk-to-mission (operational risk) from risk-to-force (force management risk). Produces the civilian-leader risk script on demand. Use throughout planning.
---

# Risk Assessment

> Risk = probability × consequence of an event causing harm to something valued. — JP 5-0 §10

## Inputs
- The relevant plan-dir file: mission analysis (`01_mission_analysis/risk_assessment_initial.md`), a COA file's risk discussion, or the CONOPS risk paragraph.

## Doctrine to load
- `references/jp5-0-field-guide.md` §5.3.6 (probability and consequence scales, risk levels)
- §10 (entire)
- §13.6 (civilian-leader risk script)
- `references/templates/risk_assessment.md`
- `references/rubrics/risk.md`

## Process

1. Ask the planner: what stage are we at? (initial mission analysis, post-wargame, post-approval). This determines depth.
2. For each risk event:
   - Score probability (Very Likely / Probable / Improbable / Highly Unlikely).
   - Score consequence (Extreme / Major / Moderate / Minor).
   - Derive risk level (High / Significant / Moderate / Low) per §5.3.6.
   - Identify mitigation across the three §10.3 categories: reduce likelihood, reduce cost, increase nonorganic support. (Acceptance is the residual after mitigation, not a primary mitigation.)
3. Separate risk-to-mission from risk-to-force. Both must appear.
4. Name **residual risk** explicitly. Risk acceptance must be visible (§10.3).
5. If the planner is preparing to brief civilian leaders, build the §13.6 script:
   - Mission-success terms.
   - Quantification ("6 months vs. 2 months", casualty bounds).
   - Risk-to-mission vs risk-to-force separated.
   - Opportunity cost.
   - Mitigation options across the three categories.
   - Residual risk.

## Outputs

- Update or create the relevant risk file.
- Optional standalone `<plan>/risk_assessment.md` if requested.

## Self-critique

Walk `references/rubrics/risk.md`. Especially:
- R-RISK-01 — both flavors named.
- R-RISK-04 — residual risk stated.
- R-RISK-06 — no language assuming away adversary capabilities (§5.3.1, §2.5 principle 5).

## Pitfalls

- **One-flavor risk.** A risk paragraph that only addresses risk-to-mission is incomplete. Force-management risk is the "breaking the force" failure mode and must be visible.
- **Asserting risk levels without rationale.** "Probable / Major / Significant" with no reason behind the P or C is not a useful artifact.
- **Mitigation only in one category.** Defaulting to "acceptance" without considering the other three categories is doctrinally weak.
- **Risk paragraph in military jargon for a civilian audience.** Translate (§13.6).
