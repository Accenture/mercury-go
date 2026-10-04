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

## RFC-0006 — `[overdue-subject-seen]`: a memory-lint pointer from an overdue fact to the logs that mention its subject (measured: the diff, not the log text)
**Status:** Open · **Raised:** 2026-10-04 · **Serves:** vision-agent-memory · **Thread:** `overdue-subject-seen-advisory`
<!-- id: rfc-0006 | status: open | thread: overdue-subject-seen-advisory -->

**Proposal.** The optional half of the mercury-composable / mercury field report (2026-10-04) whose
guidance half shipped as v4.42.1: for each `[overdue]` fact, `memory-lint` lists the `archive_window`
session logs whose body mentions the fact's distinctive terms (backticked identifiers, words from its bold
title), e.g. `[overdue-subject-seen] <id>: <session> mentions '<term>'`. Advisory only — a prompt for
`REVIEW.md` step 6's declaration-gap read and **never a use**: counting prose mentions would reintroduce
the `ot-review-step6-prose` archival livelock. Committing to it means a term-selection heuristic
implemented identically in both runtimes, mirrored tests, and one more advisory in every review.

**Measurement (2026-10-04, option b — this repo's logs; session `2026-10-04-170020`).** Corpus: every fact this
repo ever archived as faded — nine of 67 faded archivals (the other 58 were completed threads, which step 5
governs, not step 6). One was wrongful: `git-hook-fragment-dispatch`, archived 2026-09-18 although v4.40.1
and v4.41.0 changed its `50-` fragment in the window — two true sessions. Eight were correct: release
records whose substance lives in `CHANGELOG.md` / `UPGRADE.md`. Each fact was evaluated at the review that
archived it, over the 20 logs before it, with `## Memory Review` / `## Memory References` excluded.

| Signal | True sessions found | Flags per correct archival (mean / max) |
|---|---|---|
| As proposed: backticked terms + bold-title words in log text | 0 of 2 | 18.0 / 20 |
| Backticked terms in ≤ 10% of earlier logs, ≥ 2 co-occurring | 0 of 2 | 0.4 / 3 |
| Window commits touching a path the fact names | 2 of 2 | 14.4 / 20 |
| … only paths touched by ≤ 5% of earlier commits | 2 of 2 | 0 / 0 |
| … ≤ 10% | 2 of 2 | 1.3 / 3 |

Findings. (1) **Log text is the wrong place to look.** The two true sessions describe the work in prose ("the
pre-commit fragment", "hook fragment runs `--staged`"), not by the paths the fact names — so the advisory as
proposed, and the lexical log search `REVIEW.md` step 6 prescribes since v4.42.1, both miss this repo's
motivating case. (2) **The diff is the right place.** The commits that touched the fact's paths are exactly
the two true sessions; a rarity cut removes hub files (`AGENTS.md`, `UPGRADE.md`, `continuity.md`) that
change in most releases. (3) **Event records need the decision test.** At looser cuts every flag on a correct
archival is later work on code a *release record* describes (memory-lint changed after "Shipped v4.9.0") —
an exercise of the code, not reliance on the record; step 6's "changed, tested, applied" reads as keeping
such records alive. Caveats: one wrongful archival is a small positive set; the path signal needs a fact that
names paths (the downstream's retry contract and release-sweep convention may not); a commit maps to the
session log it carries, else the next one.

**Options (revised after the measurement).** (a) Ship `[overdue-path-touched]` instead of the log-text
advisory: for each `[overdue]` fact that is not a thread, list the window's commits that touch a path it
names, keeping paths touched by ≤ 5% of earlier commits — advisory, never a use; both runtimes, mirrored
tests, `git` already present wherever the hooks run. (b) Validate first on the downstream's three field
instances — their repositories, so their maintainer's go. (c) Prose regardless, as a PATCH: `REVIEW.md` step
6 adds the commit check (`git log` over the window for the fact's paths) beside the log search, and applies
the decision test to each hit, so a fact that records an event is not kept alive by later work on the same
code. The agent recommends (c) now, then (b), then (a) on the downstream result; the proposal as first
written is not recommended.

*Progress (v4.42.2):* option (c) chosen by the maintainer (2026-10-04) and shipped — `REVIEW.md` step 6 checks
the window's commits first and holds every hit to the decision test. Open: (b), then (a).

**Resolution.** —

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
