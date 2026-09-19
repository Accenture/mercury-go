- [ ] **Reconcile: `seed-copy` cannot express "deliberately absent".** Surfaced upgrading mercury-composable
  to v4.40.0 (2026-09-17, PR Accenture/mercury-composable#407): the team had deleted `.agent/secret-scan-ignore`
  on 2026-09-12 on purpose (guard at zero exceptions; credential-shaped literals restructured away), and the
  reconcile re-installed the comments-only seed because a `seed-copy` row copies whenever the target lacks the
  file — and will re-offer it on every future upgrade. Harmless this time (zero patterns), but "never touched
  when present" has no counterpart for "removed on purpose". Options for the maintainer: a target-side
  tombstone the reconcile honours (e.g. an `.agent/absent` list or a marker file), or an `optional` MANIFEST
  policy for seeds that are pure guidance. Keep `upgrades-additive` intact either way — the fix must never
  delete. → serves: vision-agent-memory (adoption stays "point it at a repo": an upgrade should not resurrect
  a deliberate deletion)
  Progress (2026-09-17, v4.40.1): the motivating row is gone — `.agent/secret-scan-ignore` is no longer
  seeded (Eric: a last-resort escape hatch; `secret-waiver-last-resort`), so the reconcile stops re-offering
  it. The general question — a target-side tombstone or an `optional` policy for the remaining seed-copy
  rows (PR template, archive INDEX, forge floors) — stays open.
  Progress (2026-09-18, v4.42.0): option (b) now exists — the MANIFEST policy `optional` (installed only on
  `--adopt`, never touched, listed for reference, never pending), first used for the governance pair (RFC-0005 →
  ADR-0009). Still open: which of the remaining `seed-copy` rows, if any, should move to it (RFC-0002).
  → proposal: RFC-0002 in `docs/arch-decisions/RFC.md` (the reasoning lives there; this thread holds the state)
  <!-- id: ot-seed-copy-deliberate-absence | created: 2026-09-17 | last_used: 2026-09-18 | uses: 5 | tier: working | origin: 2026-09-17-002547 -->
