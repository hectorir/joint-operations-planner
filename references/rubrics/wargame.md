# Rubric — Wargame Critique

> Used by `/jp-critique` against `03_wargame/`.

## R-WG-01 — Each retained COA wargamed against most-likely AND most-dangerous enemy COA
- **Doctrine:** JP 5-0 §5.5
- **FAIL** if any retained friendly COA was not run against both. This is structural; the wargame is incomplete without it.

## R-WG-02 — Red cell played aggressively with realistic capabilities
- **Doctrine:** JP 5-0 §5.5
- **FAIL** if the wargame log shows Red taking soft moves, ignoring known capabilities, or missing predictable responses.
- **WARN** if Red's actions read as scripted-to-fail.

## R-WG-03 — Action / Reaction / Counteraction documented per critical event
- **Doctrine:** JP 5-0 §5.5
- **FAIL** if any critical event is summarized without the cycle structure.

## R-WG-04 — Synchronization matrix updated
- **Doctrine:** JP 5-0 §5.5 outputs
- **WARN** if `synchronization_matrix.md` has empty rows for critical events that were wargamed.

## R-WG-05 — Decision support outputs captured
- **Doctrine:** JP 5-0 §5.5 outputs
- **FAIL** if `decision_support.md` lacks decision points OR branches OR sequels OR refined CCIRs.

## R-WG-06 — Shortfalls identified, not buried
- **Doctrine:** JP 5-0 §5.5
- **FAIL** if the wargame surfaced no shortfalls (likely Red was too soft) OR identified shortfalls aren't logged.

## R-WG-07 — No mid-wargame patching
- **Doctrine:** JP 5-0 §5.5; field guide §13.4 ("stop, revise, restart")
- **FAIL** if the wargame log shows the friendly COA was edited inline mid-game.

## R-WG-08 — Branches and sequels are real, not generic
- **Doctrine:** JP 5-0 §7.9
- **WARN** if listed branches/sequels are platitudes ("plan to defend"), not specific to this OE and decision points.

## R-WG-09 — Anticipation discipline observed
- **Doctrine:** JP 5-0 §7.10
- **WARN** if the wargame relied on a single-source assumption about enemy behavior; deception is enabled when anticipation is monolithic.
