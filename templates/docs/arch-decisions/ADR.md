# Architecture Decision Records (ADR)

> **For humans.** This is the project's governance-facing log of significant, durable
> **architecture decisions** — one decision per entry, with its rationale and the
> trade-offs it accepts. It is read **on demand**, not part of the per-session agent
> read path, so it adds **zero default token cost**. **Proposals are not ADRs:** work under
> consideration lives in the sibling register `RFC.md` (`RFC-NNNN`, its own sequence) and
> reaches this ledger only on acceptance.

## What an ADR is (and is not)

An ADR records *why* a load-bearing architectural choice was made — the kind of decision
that is expensive to reverse and that a newcomer or auditor needs the reasoning behind. It
is the **Design** altitude of the VBDI loop made durable: Current State → Vision → Blueprint
→ **Design** → Implementation → Feedback.

**Map, don't duplicate.** The live constraint text stays in `memory/continuity.md`
(`## Architectural Invariants` / `## Key Decisions`) — the *what* that holds *now*, carries an
`id`, and is read every session. An ADR is the durable *why*: context, alternatives, and
consequences. They cross-link: `formalizes:` here points to the continuity `id`, and each
invariant/decision carries a visible `(ADR-NNNN)` tag in its title (a pointer for humans —
**not** a cue for the agent to open this file). The constraint is never restated as
competing truth.

## Lifecycle (mirrors `DECAY.md` §9)

- **Status:** `Accepted` → `Superseded` / `Deprecated`. An entry is written only when a
  decision is accepted; work under consideration lives in `RFC.md`, never here as `Proposed`
  — a withdrawn proposal has no honest ledger status.
- **Never deleted.** A decision that no longer holds is **superseded** (replaced by a newer
  ADR) or **deprecated** (no longer relevant, not replaced) — the old entry stays in place,
  its `Status` updated. History is the point.
- To supersede: add a new ADR, set the old one to `Status: Superseded by ADR-NNNN`, and the
  new one to `Supersedes: ADR-NNNN`.
- Numbering is monotonic; entries are listed **newest first**.

## Format

```
## ADR-NNNN — <Title>
**Status:** Accepted · **Date:** YYYY-MM-DDThh:mm:ss.mmmZ · **Serves:** <vision-id>
<!-- id: adr-NNNN | status: accepted | formalizes: <continuity-id> -->

**Abstract.** One paragraph: what was decided and its scope.

**Rationale.** Why this, why now, the alternatives weighed, **and the consequences /
trade-offs** the decision accepts.
```

---

*(No entries yet. The first accepted decision goes here, newest first — promoted from its
`RFC.md` proposal at the maintainer's gate.)*
