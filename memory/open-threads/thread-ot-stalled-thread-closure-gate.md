- [x] **Stalled open threads → human closure gate — SHIPPED v4.40.0 (MINOR), 2026-09-16.** From the
  mercury-composable field report (2026-09-16): `thread_stale_window` knob (40) + `memory-lint`
  `[thread-stale]` + `REVIEW.md` step 8 (one human closure gate per review; the owner closes or
  re-affirms; the tool never closes) + the one-lifecycle-per-record rule. Eric's design decision is
  recorded as Key Decision `stalled-thread-closure-gate`; release PR pending (org-home PR rule). The
  tool's own two stalled threads await the gate at its next review. Lesson: pinned ≠ examined —
  every never-decay class needs a human re-check. → serves: vision-agent-memory
  <!-- id: ot-stalled-thread-closure-gate | created: 2026-09-16 | last_used: 2026-09-16 | uses: 2 | tier: active | origin: 2026-09-16-231835 -->
