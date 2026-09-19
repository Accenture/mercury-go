- [x] **Stalled open threads → human closure gate — SHIPPED v4.40.0 (MINOR), 2026-09-16.** Mercury-composable
  field report → `thread_stale_window` knob (40) + `memory-lint` `[thread-stale]` + `REVIEW.md` step 8 (one
  human closure gate per review; the owner closes or re-affirms; the tool never closes) + one lifecycle per
  record. Eric's decision → Key Decision `stalled-thread-closure-gate`. PR Accenture/mercury-go#5 merged
  2026-09-17 (`af22727`); tag `v4.40.0`; release published; the same-day dogfood review ran the first gate (three
  closed). Lesson: pinned ≠ examined — every never-decay class needs a human re-check. → serves: vision-agent-memory
  <!-- id: ot-stalled-thread-closure-gate | created: 2026-09-16 | last_used: 2026-09-17 | uses: 3 | tier: archive-candidate | origin: 2026-09-16-231835 -->
