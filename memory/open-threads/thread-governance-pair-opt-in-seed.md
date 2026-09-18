- [x] **Opt-in seed for the governance pair — sample `docs/arch-decisions/ADR.md` + `RFC.md` templates (v4.42.0).**
  Shipped in v4.42.0: a seventh MANIFEST policy `optional` (installed only on `--adopt <target>`, never touched
  when present, listed for reference when absent — never pending, never re-asked), skeletons under
  `templates/docs/arch-decisions/`, the Step 10 offer made once at enable, both reconcile runtimes + 4 mirrored
  tests each. Lesson: the opt-in stance needed its own policy — `seed-copy` cannot express a file a team
  deliberately does not have (RFC-0002), and that is exactly what "offered, never imposed" is.
  → proposal: RFC-0005 in `docs/arch-decisions/RFC.md` (implemented; promotion to an ADR at the maintainer's gate)
  → serves: vision-agent-memory
  raised in 2026-09-18-232013; closed in 2026-09-18-234620
  <!-- id: governance-pair-opt-in-seed | created: 2026-09-18 | last_used: 2026-09-18 | uses: 1 | tier: working | origin: 2026-09-18-232013 -->
