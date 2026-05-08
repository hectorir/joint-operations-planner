# Rubric — Mission Analysis Critique

> Used by `/jp-critique` against the contents of `01_mission_analysis/`. For each line item, render a finding as PASS / WARN / FAIL with quote, doctrinal cite, and remediation.

## R-MA-01 — Mission statement: who/what/when/where/why are all explicit
- **Doctrine:** JP 5-0 §5.3.4
- **PASS:** All five elements present and unambiguous; purpose clause anchors subordinates' intent inference.
- **WARN:** Element present but vague (e.g., "as required" instead of a defined trigger).
- **FAIL:** A required element missing or implied only.

## R-MA-02 — Mission statement contains no ways or means
- **Doctrine:** JP 5-0 §7.2 (objectives do not imply ways/means; mission inherits this discipline).
- **FAIL** if the statement names specific units, weapons systems, or tactics.

## R-MA-03 — Specified, implied, and essential tasks are explicitly separated
- **Doctrine:** JP 5-0 §5.3.3
- **FAIL** if any of the three buckets is missing, or if items are mis-categorized (routine recon listed as "implied").

## R-MA-04 — Constraints and restraints are distinguished
- **Doctrine:** JP 5-0 §5.3.2
- **FAIL** if "must do" and "cannot do" items are mixed; **WARN** if either list is suspiciously empty.

## R-MA-05 — Friendly and threat COGs are identified with critical-factors decomposition
- **Doctrine:** JP 5-0 §8.3
- **FAIL** if either COG is missing, or if critical capabilities/requirements/vulnerabilities are not derived.
- **WARN** if COGs read like mirror-images of each other (likely mirror-imaging error per §8.4).

## R-MA-06 — Each assumption has a validating CCIR
- **Doctrine:** JP 5-0 §5.3.1
- **FAIL** if any assumption lacks a linked PIR/FFIR.
- **WARN** on assumption-list bloat (>~10 entries) — assumptions add error and bias.

## R-MA-07 — CCIRs are short, time-bound, tied to decision points
- **Doctrine:** JP 5-0 §5.3.5
- **WARN** if the list is long (>~10), if any CCIR has no linked decision point, or if any lacks an LTIOV.
- **FAIL** if PIRs and FFIRs are not separated.

## R-MA-08 — Initial risk assessment includes both flavors
- **Doctrine:** JP 5-0 §5.3.6, §10
- **FAIL** if risk-to-mission and risk-to-force are not separately articulated.
- **WARN** if probability × consequence is asserted without rationale.

## R-MA-09 — COA evaluation criteria are defined
- **Doctrine:** JP 5-0 §5.3 (mission analysis activity 10).
- **FAIL** if `coa_evaluation_criteria.md` is missing or empty — Step 5 cannot be performed without it.
- **WARN** if criteria are not weighted or not measurable.

## R-MA-10 — Operational approach is coherent and links problem to JPP
- **Doctrine:** JP 5-0 §6.4
- **WARN** if the approach reads as a list of activities without a transformation logic from current to desired conditions.
