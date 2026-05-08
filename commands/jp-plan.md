---
description: Sherpa mode — walk me through a JPP step. Asks which step, then runs the per-step skill in walk-me-through mode.
---

Force sherpa mode. Ask the planner which JPP step they want to work on, then invoke the matching per-step skill (`/jp-initiation`, `/jp-mission-analysis`, etc.) with explicit instruction to operate in sherpa mode (interactive, question-led, writes to plan dir as it goes).

If the plan dir is empty for the chosen step, that's expected — sherpa mode is the default for empty step folders.
