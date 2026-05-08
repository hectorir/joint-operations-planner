---
description: Red-team a draft against the doctrinal rubric. Writes a structured findings file at log/critiques/. Never mutates the draft.
argument-hint: [step-name]
---

Run the `jpp-critique` skill.

Argument `$1` (optional): the step to critique — one of `mission-analysis`, `coa-development`, `wargame`, `plan`, `cog`, `risk`. If omitted, ask the planner.

The skill MUST:
1. Walk the matching rubric in `references/rubrics/<step>.md` line by line.
2. Render each finding as `PASS` / `WARN` / `FAIL` with a quote, doctrinal cite, and remediation.
3. Write findings to `log/critiques/<step>-<YYYY-MM-DD-HHMM>.md`.
4. Never mutate the draft.
