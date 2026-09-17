- [x] **Shipped v4.34.0 (MINOR) — pre-commit secret guard on both surfaces (memory + config).**
  Staged-content scan blocks committed secrets by default (the deliberate, scoped exception
  to the advisory doctrine — secrets carry irreversible cost); knob opts down, `--no-verify`
  bypasses once; probe-tuned to 0 FPs on a 661-file live corpus. Fold-up v4.34.1: guidance
  prints once per run. Full detail: origin log + the `4.33.4→4.34.0` rung.
  → serves: vision-agent-memory
  <!-- id: pre-commit-secret-guard-v4340 | created: 2026-08-14 | last_used: 2026-09-04 | uses: 4 | tier: active | origin: 2026-08-14-021712 -->
