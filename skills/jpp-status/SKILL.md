---
name: jpp-status
description: Reports the current state of a plan dir — step status, gaps, unanswered CCIRs, unvalidated assumptions, recommended next action. Read-only with the optional ability to append to log/changes.md.
---

# JPP Status

## Inputs
- `~/joint-plans/<plan>/manifest.yaml`
- All step folders (read-only)

## Process

1. List plans under `~/joint-plans/`. If the planner specified one, use it. Otherwise show the list and ask.
2. Load `manifest.yaml`. If missing or malformed, say so and offer to scaffold.
3. For each step, check:
   - Status field in manifest (`pending`, `in_progress`, `complete`, `stale`).
   - Files in the step folder. If status is `complete` but key files are empty, flag it.
   - Last critique timestamp. If older than the step's last_modified, flag as stale-critique.
4. For mission analysis specifically:
   - Count assumptions without linked CCIRs.
   - Count CCIRs without linked decision points.
5. For COA development:
   - Per-COA: any validity test set to `fail` or `pending`?
   - For wargame readiness: are at least two COAs distinguishable?
6. Compose a report (format below).

## Report format

```
Plan: <name> (<level>)
Profile: <path or "none">

Step status:
  [ check | arrow | space ] 1. Initiation
  [ check | arrow | space ] 2. Mission Analysis        (last critique: <result>, <relative time>)
  [ check | arrow | space ] 3. COA Development         (in progress — N of M COAs drafted)
  ...

Cross-cutting:
  [ check | arrow | space ] COG analysis               (note)
  [ check | arrow | space ] Assessment plan

Open issues:
  - <issue 1>
  - <issue 2>

Recommended next: <skill>
```

Use `[x]` for complete, `[>]` for in-progress, `[ ]` for pending, `[!]` for stale.

## Doctrine to cite when calling out gaps
- Field guide §11.4 — MOPs/MOEs hierarchy
- §11.5 — Four plan-assessment outcomes
- §13 — All practitioner checklists

## Pitfalls

- Don't lie about state. If the manifest says `complete` but the file is empty, the file's emptiness wins — surface it.
- Don't recommend a step that's structurally impossible (can't recommend wargame without at least two COAs).
