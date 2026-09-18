# Requests for Comments (RFC) — the proposal register

> **For humans.** Work under consideration at the Design altitude: proposals that may become an
> Architecture Decision Record, be reshaped, merge with another, or be withdrawn. It is the
> sibling of `ADR.md` and exists so that **the ledger records decisions only** — an ADR is written
> when a proposal is accepted, never before (`memory/PROTOCOL.md` *Work from intent*, `DECAY.md`
> §12, v4.41.2). Read **on demand**, not part of the per-session agent read path (zero default token
> cost, the same footing as `ADR.md` and `docs/DESIGN-*.md`).

## Rules

- **Separate sequences.** `RFC-NNNN` and `ADR-NNNN` never share numbers: a proposal does not
  reserve an ADR number, because proposals and decisions do not map one-to-one — some merge, some
  split, some die.
- **Two exits, both recorded here.** *Promoted:* the human accepted it; the ADR is written in
  `ADR.md` and this entry keeps a pointer (`Promoted → ADR-NNNN`, date). *Withdrawn:* the entry stays
  with the reason. An entry is **never deleted**; a proposal may be revised freely while open, and
  only its final form reaches the ledger.
- **Status:** `Open` (under consideration) · `Parked` (deliberately deferred — reactivate on demand)
  · `Promoted → ADR-NNNN` · `Withdrawn`.
- **Map, don't duplicate.** The live work item stays in memory — an Open Thread in
  `memory/open-threads/` carrying a `→ proposal: RFC-NNNN` pointer — exactly as an accepted ADR is
  pointed to by a `(ADR-NNNN)` tag on its continuity fact. The register holds the proposal's
  reasoning (options, trade-offs, what a decision would commit to); the thread holds its state.
- **The human decides.** The agent raises and revises proposals here; promotion is the Design-altitude
  human gate (`DECAY.md` §12). Newest first.

## Format

```
## RFC-NNNN — <Title>
**Status:** Open · **Raised:** YYYY-MM-DD · **Serves:** <vision-id> · **Thread:** `<thread-id>`
<!-- id: rfc-NNNN | status: open | thread: <thread-id> -->

**Proposal.** What would change, and what a decision would commit the project to.
**Options.** The alternatives on the table, with their trade-offs.
**Resolution.** Empty while open; `Promoted → ADR-NNNN (date)` or `Withdrawn (date): <reason>`.
```

---

## RFC-0005 — An opt-in seed for the governance pair: sample `ADR.md` + `RFC.md` templates
**Status:** Promoted → ADR-0009 · **Raised:** 2026-09-18 · **Serves:** vision-agent-memory · **Thread:** `governance-pair-opt-in-seed` (closed — shipped)
<!-- id: rfc-0005 | status: promoted | adr: ADR-0009 | thread: governance-pair-opt-in-seed -->

**Proposal.** Ship `templates/docs/arch-decisions/ADR.md` and `RFC.md` as skeletons with placeholders,
so a team that adopts the governance pair starts from the canonical shape instead of copying this
repo's files by hand (half the family adopted ledgers by hand: mercury-composable 24 ADRs and a
register, mercury 18 ADRs). Raised by the maintainer (2026-09-18).

**Options.** (a) Opt-in seed: `ENABLE.md` asks once at enable and copies the pair only on yes; Mode B
never re-offers it. Requires a new MANIFEST policy, `optional` — offered once, never re-offered — which
is RFC-0002's option (b) made concrete, with reconcile support in both runtimes and tests. Keeps the
ledger optional and the tool never heavyweight. (b) Plain `seed-copy`: fastest, but installs governance
ceremony into every enabled repo and re-offers the pair on every upgrade after a team deletes it — the
very hazard RFC-0002 records. (c) Do nothing: this repo's files remain the reference shape.

**Resolution.** Maintainer go for option (a) as **v4.42.0** (2026-09-18), after 4.41.2 ships. Design
fixed and implemented in v4.42.0: MANIFEST policy `optional` — installed only on an explicit
`--adopt <target>` (a path ending in `/` adopts every optional row under it), never touched when
present, listed for reference when absent and never pending; `ENABLE.md` Step 10 offers the pair once;
Mode B never re-asks; skeletons at `templates/docs/arch-decisions/`. **Promoted → ADR-0009 (2026-09-18)**
at the maintainer's gate — the accepted form is in `ADR.md`; this entry stays as the pointer.

## RFC-0004 — Formalize the ledger rule itself as ADR-0008
**Status:** Promoted → ADR-0008 · **Raised:** 2026-09-18 · **Serves:** vision-agent-memory · **Thread:** — (Key Decision `adr-ledger-decisions-only`)
<!-- id: rfc-0004 | status: promoted | adr: ADR-0008 | formalizes-candidate: adr-ledger-decisions-only -->

**Proposal.** Record "the ADR ledger records decisions only; proposals live in `RFC.md`" as
ADR-0008, `formalizes: adr-ledger-decisions-only`, with the continuity fact gaining its
`(ADR-0008)` tag. The rule governs the ledger's own integrity — the property an auditor relies on
(every entry is a commitment the project made, dated) — which is the class of durable, expensive-to-
reverse choice the ledger exists to hold; ADR-0007 (hook dispatch) is a comparable structural rule.

**Options.** (a) Promote: the ledger states its own admission rule in its own record. (b) Leave it a
Key Decision: the continuity fact, the protocol text and this register already carry it, and an ADR
about the ledger's bookkeeping may read as ceremony ("never heavyweight"). The maintainer decides.

**Resolution.** Promoted → ADR-0008 (2026-09-18) at the maintainer's gate — the accepted form is in
`ADR.md`; this entry stays as the pointer.

## RFC-0003 — Drop the redundant `thread-` filename prefix in `memory/open-threads/`
**Status:** Parked · **Raised:** 2026-09-18 · **Serves:** vision-agent-memory · **Thread:** `open-threads-filename-prefix`
<!-- id: rfc-0003 | status: parked | thread: open-threads-filename-prefix -->

**Proposal.** Name thread files `<id>.md`: inside a directory already called `open-threads/`, the
`thread-` prefix adds nothing and stutters against kind-prefixed ids (mercury-composable note,
2026-09-18, filed as cosmetic). The whole of it: memory-lint check 12's one filename expectation per
runtime accepting `<id>.md`, a `git mv` of every file with **ids untouched** (an id is permanent —
renaming one orphans its immutable-log declarations, `DECAY.md` §1), ~22 doc lines across 15
lockstep surfaces, the schema sentence "the filename is the identity and never changes" reworded in
the same release, and an upgrade step that detects and collapses the in-flight-branch case (a branch
adding `thread-foo.md` while main has `foo.md` merges cleanly into two files for one thread —
`[duplicate-id]` catches it before merge on GitHub, after merge elsewhere).

**Options.** (a) Do it as a pure file rename, as above. (b) Accept both shapes forever (additive
only) — rejected: a mixed directory for the life of long-lived blueprint threads undercuts the
legibility gain that motivates the change. (c) Leave it — the second layer of the stutter,
kind-prefixed ids, was fixed as guidance in v4.41.1, and prefixed files retire as threads close.
Parked on (c) by the maintainer (2026-09-18): reactivate only when a field installation asks.

**Resolution.** —

## RFC-0002 — Let `seed-copy` express "deliberately absent"
**Status:** Open · **Raised:** 2026-09-17 · **Serves:** vision-agent-memory · **Thread:** `ot-seed-copy-deliberate-absence`
<!-- id: rfc-0002 | status: open | thread: ot-seed-copy-deliberate-absence -->

**Proposal.** A `seed-copy` MANIFEST row copies whenever the target lacks the file, so a file a team
removed on purpose is re-installed by the next upgrade and re-offered forever — "never touched when
present" has no counterpart for "removed on purpose" (surfaced upgrading mercury-composable to
v4.40.0, where a deliberately deleted waiver stub came back). The motivating row is gone since
v4.40.1; the general question stands for the remaining seed-copy rows (PR template, archive INDEX,
forge floors). *Progress (v4.42.0):* option (b) now exists as the MANIFEST policy `optional` (first
used for the governance pair, RFC-0005) — the open question narrows to *which* existing `seed-copy`
rows, if any, should move to it.

**Options.** (a) A target-side tombstone the reconcile honours — an `.agent/absent` list or a marker
file — so the target, not the tool, records the deletion. (b) An `optional` MANIFEST policy for seeds
that are pure guidance: offered once at enable, never re-offered. Either must keep `upgrades-additive`
intact — the fix must never delete. Trade-off: (a) adds a target-side artefact the human must know
about; (b) moves the judgement into the manifest and loses the "converged" guarantee for those rows.

**Resolution.** —

## RFC-0001 — Protocol-text propagation: keep the per-release Semantic row, or make the protocol `verbatim`
**Status:** Open · **Raised:** 2026-08-21 · **Serves:** vision-agent-memory · **Thread:** `ot-protocol-text-propagation`
<!-- id: rfc-0001 | status: open | thread: ot-protocol-text-propagation -->

**Proposal.** `memory/PROTOCOL.md` is `seed-copy`, so an installed protocol is never re-copied —
deliberate (a re-copy could drop a target's local directives irrecoverably), but it ends the automatic
propagation the old `verbatim` `AGENTS.md` hub had, and about half of recent releases edit protocol
text. Today every such release ships a Semantic steps row (re-copy a still-stock protocol; arbitrate a
customized one per `ENABLE.md` §5i) — a per-release obligation, not a mechanism.

**Options.** (a) Keep the obligation: explicit, auditable per rung, and it preserves customized
protocols without loss (AC-MP-07/08). (b) Move the row to `verbatim` and lean on §5i drift
arbitration at upgrade time — truer to the house model and it closes the propagation gap, but it
weakens "preserved without loss" for a customized protocol. (c) A hybrid: `verbatim` when the target
protocol is byte-identical to the previous template (the common case, four of four family repos at
every rung since v4.40.0), the Semantic row only for customized copies. Open for the maintainer.

**Resolution.** —
