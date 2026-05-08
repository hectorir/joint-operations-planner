---
name: jpp-initiation
description: JPP Step 1 — Planning Initiation. Loads strategic guidance, captures the commander's initial planning guidance, drafts the operational approach. Use at the start of a new plan or to refresh after a major change in direction.
---

# JPP Step 1 — Planning Initiation

## Inputs
- `context.md` (especially Higher HQ + Strategic Guidance Citations)
- `manifest.yaml`
- Optional: profile at `~/.config/joint-planner/profile.md`
- Any directives the planner has (paste-in is fine, file-by-reference is fine)

## Doctrine to load
Read the following sections from `references/jp5-0-field-guide.md`:
- §5.2 — Step 1 specifics
- §6.1 — Operational design 9-step methodology
- §6.2 — OE frameworks (PMESII / ASCOPE / METT-T)
- §6.3 — Defining the problem
- §6.4 — Operational approach

Also load the field guide's §2.4 (understanding problems before solving them) and §2.5 (seven principles).

## Process

1. **Capture strategic guidance.** Ask the planner what authorizes this planning effort (NSS, NDS, NMS, UCP, CPG, JSCP, GIF, or a CCDR directive). For each, record its title, date, and the directing language relevant to this plan. Write to `00_initiation/strategic_guidance.md`.

2. **Capture commander's initial planning guidance.** Ask the planner for:
   - The commander's current understanding of the OE.
   - The commander's current framing of the problem (symptom vs root cause — apply §2.4).
   - Initial intent (one paragraph).
   - Anything explicitly off the table (preview restraints).
   Write to `00_initiation/initial_planning_guidance.md`.

3. **Draft the operational approach.** Walk the operational design 9 steps (§6.1):
   1. Strategic direction and guidance.
   2. Strategic environment.
   3. Operational environment (use PMESII/ASCOPE/METT-T as a checklist).
   4. **Define the problem** — one paragraph. This is a *contextual hypothesis*; small wording changes matter.
   5. Identify assumptions (strategic and operational; defer most to mission analysis).
   6. Develop options — the operational approach itself: how the force transforms current conditions into desired conditions.
   7. Identify external decision points.
   8. Refine the approach.
   9. Note the planning and assessment guidance the commander wants.
   Write to `00_initiation/operational_approach.md`.

4. **Update manifest.** Set `steps.initiation.status = complete` if all three files have substantive content; otherwise leave `in_progress`. Set `steps.initiation.last_modified` to now.

5. **Commit.** `git add 00_initiation/ manifest.yaml && git commit -m "step:initiation complete"` (or "step:initiation in-progress" if not done).

6. **Self-critique.** Before declaring `complete`, run `/jp-critique --step initiation` mentally — but Step 1 has no rubric file (out of scope for v1; the critic skill flags this as N/A). Instead, sanity-check: is the problem statement a hypothesis (testable), or a slogan?

## Outputs

- `00_initiation/strategic_guidance.md`
- `00_initiation/initial_planning_guidance.md`
- `00_initiation/operational_approach.md`
- `manifest.yaml` updated

## Pitfalls

- **Skipping the problem definition.** The problem statement is the most important output of Step 1; it shapes everything downstream. If the planner can't articulate it in one paragraph, keep working — don't move to mission analysis.
- **Confusing symptom and root cause.** A common failure mode for COIN/HADR/IW. Apply the field guide's example: killing or detaining insurgents ≠ addressing the underlying causes of an insurgency. Push back when you see it.
- **Inventing forces.** The operational approach assumes currently available capabilities, not future ones (§2.5 principle 3).
