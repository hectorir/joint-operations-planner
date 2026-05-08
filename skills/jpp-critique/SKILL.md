---
name: jpp-critique
description: Red-team a draft against the doctrinal rubric. Walks the rubric line by line; renders PASS / WARN / FAIL findings with quote, doctrinal cite, and remediation. Writes a structured findings file at log/critiques/. Never mutates the draft. Use whenever a step is being closed out, or on demand.
---

# JPP Critique

## Hard rule

**Never mutate the draft.** The planner is the author. Your output is a structured findings file the planner chooses to act on. The draft files in `01_mission_analysis/`, `02_coas/`, etc. are read-only to this skill.

## Inputs

- The step under review.
- The matching rubric in `references/rubrics/<step>.md`.
- All draft files in the relevant step folder.

## Doctrine

- `references/jp5-0-field-guide.md` §13.2/3/4/5 (checklists)
- §8.6 (COG completion 5 questions)
- §10.4 (risk articulation)
- All rubric files in `references/rubrics/`.

## Process

1. Determine the step to critique. Argument `$1` to the slash command, or ask the planner.
2. Map step → rubric:
   - `mission-analysis` → `references/rubrics/mission_analysis.md`
   - `coa-development` → `references/rubrics/coa.md` (run per COA)
   - `cog` → `references/rubrics/cog.md` (run per COG file)
   - `wargame` → `references/rubrics/wargame.md`
   - `plan` → `references/rubrics/plan.md` (also runs §13.5 two-line test)
   - `risk` → `references/rubrics/risk.md`
3. Read the relevant draft files.
4. Walk the rubric **line by line**. For each rubric item:
   - Render `PASS` / `WARN` / `FAIL`.
   - Quote the relevant text from the draft (or note "missing" if absent).
   - Cite the doctrine (field guide section number).
   - State the remediation in one sentence.
5. Write findings to `log/critiques/<step>-<YYYY-MM-DD-HHMM>.md` with the format below.
6. Update manifest: `steps.<step>.last_critique` = ISO-8601 timestamp; record critique result summary in `log/changes.md`.
7. **Do not edit the draft.**

## Findings file format

```markdown
# Critique: <Step Name> — <YYYY-MM-DD HH:MM>

Plan: <plan-name>
Rubric: references/rubrics/<step>.md
Files reviewed: <list>

## Summary
- N PASS · M WARN · K FAIL

## FAIL — <rubric item title>
File: <path>
Quote: "<quoted text or 'missing'>"
Doctrine: §<section> — <one-line citation>
Why this matters: <one sentence>
Remediation: <one sentence>

## WARN — <rubric item title>
...

## PASS — <rubric item title>
...
```

## Self-critique gate (used by other skills)

Other skills invoke this in **dry-run mode** before transitioning a step to `complete`. In dry-run:
- Walk the rubric.
- Do NOT write a findings file.
- Return: `{ pass: N, warn: M, fail: K }`.
- The calling skill blocks on `fail > 0`; surfaces `warn` to the planner; allows transition on `fail == 0`.

## Pitfalls

- **Editing the draft.** Don't. Surfaces remediation; the planner edits.
- **Vague findings.** Every finding needs a quote (or "missing") + a section cite. "This needs work" is not a finding.
- **Skipping rubric items.** Walk every line — including PASS items. The PASS list is reassuring and shows the work.
- **Inventing doctrine to support a finding.** If the rubric doesn't cover something, the critique doesn't cover it. Tell the planner if the rubric is missing a check; that's a rubric-gap to file, not a freelance call.
