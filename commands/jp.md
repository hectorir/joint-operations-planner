---
description: Joint Planner — top-level router. Use when you don't know where to start or want a guided dispatch.
---

Run the `joint-planner` agent (umbrella).

Your job: identify the plan (new or existing), load `manifest.yaml` and `context.md`, and dispatch to the right per-step or per-mode skill. If the planner is starting fresh, scaffold the plan dir per the README, run `git init`, and invoke `/jp-initiation`.

Read first:
- `references/jp5-0-field-guide.md` §1 (Quick Reference), §2.5 (seven principles), §5.1 (JPP map)
- The agent file at `agents/joint-planner.md` for routing rules

Hard rule: UNCLASSIFIED only. The planner must not paste classified content.
