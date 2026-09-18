- [ ] **Opt-in seed for the governance pair — sample `docs/arch-decisions/ADR.md` + `RFC.md` templates (v4.42.0).**
  Eric (2026-09-18): ship the two skeletons with placeholders so a team that adopts the ledger and the
  register starts from the canonical shape — **opt-in**: `ENABLE.md` asks once at enable and copies the
  pair only on yes; Mode B never re-offers it (half the family adopted ledgers by hand: mercury-composable
  24 ADRs + a register, mercury 18). Needs a new MANIFEST policy `optional` (offered once, never
  re-offered — RFC-0002 option b made concrete) with reconcile support in both runtimes + tests,
  `templates/docs/arch-decisions/ADR.md` + `RFC.md`, an ENABLE step, a schema note; the ledger stays
  optional ("never heavyweight"). Build after 4.41.2 ships; promote RFC-0005 to an ADR once the policy
  design is fixed.
  → proposal: RFC-0005 in `docs/arch-decisions/RFC.md` (the reasoning lives there; this thread holds the state)
  → serves: vision-agent-memory (adoption stays "point it at a repo": governance is offered, never imposed)
  <!-- id: governance-pair-opt-in-seed | created: 2026-09-18 | last_used: 2026-09-18 | uses: 1 | tier: working | origin: 2026-09-18-232013 -->
