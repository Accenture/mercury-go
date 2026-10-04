- [ ] **`[overdue-subject-seen]` — a memory-lint pointer from an overdue fact to the window logs that
  mention its subject (proposal — measured 2026-10-04; maintainer decision next).** The optional half of
  the mercury-composable / mercury field report (2026-10-04); its guidance half shipped as v4.42.1
  (`REVIEW.md` step 6, *declaration gaps (facts)*). Advisory only and **never a use** — counting mentions
  would reintroduce the `ot-review-step6-prose` livelock. **Measured on this repo's nine faded fact
  archivals:** the log-text signal as proposed found 0 of the 2 true sessions behind the wrongful
  `git-hook-fragment-dispatch` archival and flagged 18 of 20 logs per correct archival; commits touching a
  path the fact names, keeping paths touched by ≤ 5% of earlier commits, found 2 of 2 with no flag on any
  correct archival. So the diff, not the log text, is where a declaration gap shows — and step 6's lexical
  log search shares the miss. Next, the maintainer's choice among the revised options: (c) a step-6 PATCH
  adding the commit check and the decision test for event records (the agent's first recommendation), (b)
  validating the path signal on the downstream's three instances, (a) shipping `[overdue-path-touched]`.
  → serves: vision-agent-memory (drift is detectable, never silent)
  → proposal: RFC-0006 in `docs/arch-decisions/RFC.md` (the reasoning lives there; this thread holds the state)
  <!-- id: overdue-subject-seen-advisory | created: 2026-10-04 | last_used: 2026-10-04 | uses: 1 | tier: working | origin: 2026-10-04-162944 -->
