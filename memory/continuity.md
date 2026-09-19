# Continuity — agent-memory

> Shared ground truth for this tool's own development state.

---

## Project State

- **project:** agent-memory
- **status:** v4.42.0 — official Accenture open source in the Mercury family (graduated 2026-09-10; home `Accenture/mercury-go`, docs `accenture.github.io/mercury-go`); a vendor-neutral, no-code (markdown) shared-AI-memory + AI-enablement tool: backward memory (decay/review/archive), forward VBDI loop, cross-vendor skills layer, declarative enable/upgrade (MANIFEST reconcile), forge-aware ritual triggers (GitHub/GitLab/AzDO), the merge-scale thread layout (`memory/open-threads/`), and the stalled-thread human closure gate (`[thread-stale]` + `REVIEW.md` step 8). Detail: What's Been Built below; per-version history: `UPGRADE.md` + session logs.
- **last_enabled:** 2026-06-12
- **last_review:** 2026-09-18 | through 2026-09-19-000416
- **last_invariant_check:** 2026-08-22 | through 2026-08-22-174808 (all 6 confirmed by Eric — walkthrough with live-tree evidence; no-build-step wording refreshed)
- **vision:** `memory/vision.md` (north star; Blueprint gaps in Open Threads below)

## What's Been Built

**Core protocol & templates**
- `ENABLE.md` — 10-step protocol: detection (Step 2), mode selection (Step 3),
  analysis (4), generate/complete (5), bootstrap install (6), `.gitignore` install
  (7), verify (8), report (9), post-enable actions (10); version-aware Mode B
- `MIGRATE.md` — per-vendor migration protocols for 11 vendors (reached via Mode C)
- `AGENTS.md` — exact one-line universal shim to `memory/PROTOCOL.md`
- `memory/PROTOCOL.md` — dual-mode operator dispatch + internal session protocol;
  `templates/memory/PROTOCOL.md` is the installed target-only source
- `CLAUDE.md`, `GEMINI.md`, `.cursorrules`, `.windsurfrules`, Copilot bootstrap
- `templates/` — bootstrap + memory templates with `{{placeholders}}`, including
  `templates/.gitignore` (v3.1.0), `memory/decay-policy.md`, `.agent/version.md`
- `memory/` — this tool's own memory layer (dogfooded)

**Evolving-memory layer (v3.0.0)**
- `DECAY.md` (deterministic integer tier rules), `REVIEW.md` (review ritual),
  `UPGRADE.md` (in-place version ladder, operator-only), `VERSION` (semver)
- `docs/DESIGN-evolving-memory.md` (design) + `docs/assessments/` (industry-alignment baseline)
- `memory/archive/` cold storage; fact metadata footers + `## Memory References`

**v3.1.0**
- AI-infrastructure `.gitignore` propagation into enabled repos (create-or-append,
  de-duplicating, add-only)

**Governance / licensing**
- `LICENSE` (Apache-2.0), `CHANGELOG.md` (Keep a Changelog; v1.0.0–3.1.0)

**Examples**
- `examples/rust-event-bus/` — Mode A, a REAL fixture (unedited output from enabling
  `~/sandbox/rust/rust_event_bus_example`); replaced the old node-project mock
- `examples/migrated-cursor-aider-project/` — Mode C (Cursor + Aider, originals under
  `legacy/`, 3 converted sessions)
- `examples/evolving-memory-example/` — the review ritual in action (continuity
  before/after, archive, session log with Memory References)

**Field validation (2026-09-16)**
- The `AGENTS.md` one-line shim (v4.37.0) activates the protocol across vendors in live use:
  Codex (mercury-composable PR #341 — Codex co-author trailer), Kiro (tested with Claude, GPT and
  Gemini), Antigravity, and Cursor running Grok (2026-09-05). The v4.37.0 canary
  (`ot-agents-native-activation-canary`) closed on this evidence.
  <!-- id: agents-shim-activation-validated | created: 2026-09-16 | last_used: 2026-09-16 | uses: 1 | tier: archive-candidate | origin: 2026-09-16-235431 -->

## Supported Migration Sources (v2)

Claude Code, Cursor, Cline, Roo Code, Aider, Continue.dev, Codeium/Windsurf,
GitHub Copilot, GPT/Codex agents, Zed AI, Gemini CLI.

## Architectural Invariants

> Hard constraints — the tool's core safety philosophy. These never decay (`core`).
> (Added 2026-06-13 when this repo adopted the evolving-memory layer.)
>
> Each invariant's `(ADR-NNNN)` tag points to its full Architecture Decision Record in
> `docs/arch-decisions/ADR.md` (rationale + trade-offs) — a **pointer for humans**. The invariant text here
> is authoritative for the agent; **don't open `docs/arch-decisions/ADR.md` to orient** — read it on demand only.

- Target-repo scope only (ADR-0001) — never read/modify/move anything outside the resolved
  target-repo root (never `~`, `~/.claude/`, Application Support, AppData, system paths)
  <!-- id: target-repo-scope-only | created: 2026-06-13 | last_used: 2026-06-18 | uses: 12 | tier: core -->
- Never delete vendor files (ADR-0002) — move originals to `legacy/<vendor>/`, preserving paths
  <!-- id: never-delete-vendor-files | created: 2026-06-13 | last_used: 2026-06-18 | uses: 8 | tier: core -->
- Never overwrite, never pick a winner (ADR-0003) — fold vendor steering under
  `## Migrated rules from <vendor>`; surface contradictions as Open Threads
  <!-- id: never-pick-a-winner | created: 2026-06-13 | last_used: 2026-06-18 | uses: 14 | tier: core -->
- No build step; agent-run (ADR-0006) — the tool itself runs no code and needs none (no install, no
  daemon). The markdown files are the product and the agent is the runtime. Optional helpers
  MAY ship — skill-bundled scripts, the operator-side reconcile twins (`scripts/`), the
  committed git-hook fragments, and the forge CI wrappers — but every one is invoked by the
  agent, vendor, git, or CI at the user's direction, never required: the no-runtime fallback
  is real (`MANIFEST.md` is walkable by hand) and nothing daemonizes. (Wording refreshed
  2026-08-22 at invariant re-verify to name the grown helper family — substance unchanged.)
  <!-- id: no-build-step-agent-run | created: 2026-06-16 | last_used: 2026-06-20 | uses: 31 | tier: core | supersedes: no-code-markdown-only | origin: 2026-06-16-002134 -->
- Upgrades are additive and non-destructive (ADR-0005) — enrich and add, never rewrite or delete —
  **except the tool's own managed built-ins** (`memory-lint`, `second-opinion`, `apply-critique`,
  `sync-adapters`, `harvest-knowledge`, `archive-fact`, `refresh-metadata`), which are re-copied (overwritten) on upgrade; that overwrite is scoped to those tool-owned files,
  and a user customizes only by forking under a new skill name (see `ENABLE.md` §5i). For everything
  the user authors, the invariant holds unchanged.
  <!-- id: upgrades-additive | created: 2026-06-13 | last_used: 2026-06-20 | uses: 22 | tier: core -->

## Key Decisions

- Originals preserved under `legacy/<vendor>/`, never deleted
- Steering content folded into `memory/instructions.md` as
  `## Migrated rules from <vendor>` sections
- History (JSONL, markdown chat logs, JSON sessions) converted to dated
  `memory/sessions/YYYY-MM-DD-HHMMSS.md` files (one per session; filename =
  persist time UTC; title = `# Session (startZ - endZ)` with full ISO 8601 ms;
  lexicographic sort = chronological sort, resolves last-session unambiguously
  across multiple contributors)
- Contradictions between vendors surface as Open Threads — the tool never picks a winner
- Three modes: Fresh Enable (A), Already Ours (B, idempotent), Migrate Vendor (C)
- Dry-run support so users can preview before committing
- **`origin` is GitHub `Accenture/mercury-go` — the official home since graduation
  (2026-09-10); assume GitHub for git ops.** agent-memory joined the Mercury family
  (Accenture open source for human–AI collaboration) by commit transfer, not GitHub repo
  transfer: full history + 23 tags + `gh-pages` pushed to `main` of the repurposed `mercury-go`
  repo (its two placeholder commits joined as unrelated history; fast-forward, nothing forced)
  — a one-time exception Eric granted for the graduation step; the tool keeps its name and its
  version. `acn-ericlaw/agent-memory` is the pre-graduation home — PR/issue links in older logs
  and threads still resolve there. **Contribution workflow for the org home from here on: PR
  required** (Eric, 2026-09-10 — "since mercury-go is an official repo, a PR is required").
  **Org-home PR and release creation need the `acn-ericlaw` account** — the Enterprise Managed User
  account is refused for `createPullRequest` and lacks the `workflow` scope for releases (2026-09-10,
  2026-09-16/17): switch, create, switch back.
  <!-- id: github-origin-mercury-go | created: 2026-09-10 | last_used: 2026-09-18 | uses: 11 | tier: active | supersedes: github-origin-git-ops | origin: 2026-09-10-152543 -->
- **A long-stalled open thread is a signal for closure, rectified through a human gate — never
  auto-closed** (Eric, 2026-09-16; shipped v4.40.0). Unreferenced for more than
  `thread_stale_window` sessions (default 40), an unchecked thread is *stalled*: `memory-lint`
  flags it (`[thread-stale]`) and the review lists it in one closure gate (`REVIEW.md` step 8)
  where the owner closes it (undelivered items recorded as *deliberately dropped*) or re-affirms
  it under `## Memory References` — the only reset. Inspecting a stalled thread is not a use.
  Why: under competing priorities loose ends get filed in a thread and left behind without a
  trace — pinned had come to mean unexamined (mercury-composable field report); and closing a
  `(blueprint)` gap is an altitude decision, so `DECAY.md` §12 already required the human.
  **v4.41.0 (2026-09-17): a closure is declared under `## Memory References` too** — the close record is
  the completion event that starts the sweep clock; an edit or a closure is a use, inspecting alone is
  not. The v4.40.0 wording named only re-affirmation and a field session left two gate closures
  undeclared, so `refresh-metadata` read the human's decision as non-use; memory-lint check 16
  `[undeclared-reference]` now catches a fact edited without a declaration at commit time.
  <!-- id: stalled-thread-closure-gate | created: 2026-09-16 | last_used: 2026-09-18 | uses: 4 | tier: active | origin: 2026-09-16-234024 -->
- **The secret-scan waiver file is a last-resort escape hatch, not a default** (Eric, 2026-09-17, on
  the mercury-composable team's suggestion; shipped v4.40.1). `.agent/secret-scan-ignore` is no longer
  seeded or recommended: zero secret leakage is the goal, and even dummy test values are false
  positives in field security scanners (they key on the `key=<literal>` shape regardless of value) —
  a fixture that trips the guard is restructured to `${ENV_VAR:placeholder}`. The mechanism stays
  (the hook and CI floors honor a committed file) for a team that knows the implications, and the
  hook states them each time it exempts a file.
  <!-- id: secret-waiver-last-resort | created: 2026-09-17 | last_used: 2026-09-17 | uses: 1 | tier: active | origin: 2026-09-17-012400 -->
- **An id names the thing, never its kind — and an existing id is never renamed** (Eric, 2026-09-18,
  first recorded in mercury-composable; the tool's rule since v4.41.1). Every open thread lives at
  `memory/open-threads/thread-<id>.md`, so an id beginning `ot-`/`thread-`/`bp-` stutters
  (`thread-ot-…`, `thread-thread-…`) — near-universal across the family repos, and mostly the tool's
  doing: the mandated `ot-close-stalled-threads-<date>` gate id (now `close-stalled-threads-<date>`),
  this repo's own `ot-` habit, and `thread-` ids in the evolving-memory example. Renaming an existing
  id is never the fix: session logs are immutable and their `## Memory References` are
  `refresh-metadata`'s only input, so the fact would decay while live. This repo's 21 `thread-ot-…`
  files stay as they are. The `thread-` filename prefix itself is a parked backlog
  (`open-threads-filename-prefix`).
  <!-- id: id-naming-no-kind-prefix | created: 2026-09-18 | last_used: 2026-09-18 | uses: 2 | tier: active | origin: 2026-09-18-215724 -->
- **The ADR ledger records decisions only; proposals live in an `RFC.md` register (ADR-0008)** (Eric, 2026-09-18,
  on the mercury-composable team's report; shipped v4.41.2). The protocol's old "propose a newer ADR …
  and wait for human approval" put non-decisions into the decision record — their ledger held five
  `Proposed` ADRs for decisions that had already shipped, and a withdrawn proposal has no honest ledger
  status (`Superseded` implies a successor, `Deprecated` implies it was once in force). Rule: an ADR is
  written only when a decision is accepted; work under consideration lives in the repo's proposal
  register — the tool's example is a sibling `docs/arch-decisions/RFC.md` with its own `RFC-NNNN`
  sequence (Eric chose `RFC-` over `P-` as the industry-recognised marker for a proposal open to
  comment, and the file is named after the prefix). Separate sequences: a proposal does not reserve an
  ADR number. Guidance only — nothing in the tool reads ADR status; a repo with `Proposed` entries
  resolves them once by hand (mercury holds six as of 2026-09-18). Adopted here the same day:
  `docs/arch-decisions/RFC.md` opened with RFC-0001…0004 (three from open threads, one proposing to
  formalize this rule as ADR-0008 — the maintainer's gate).
  <!-- id: adr-ledger-decisions-only | created: 2026-09-18 | last_used: 2026-09-18 | uses: 5 | tier: active | origin: 2026-09-18-230858 -->
- **The governance pair is an opt-in seed — offered once, never imposed (ADR-0009)** (Eric, 2026-09-18, RFC-0005;
  shipped v4.42.0). Sample `docs/arch-decisions/ADR.md` + `RFC.md` skeletons ship as `templates/`, but under a
  new MANIFEST policy `optional`: installed only on an explicit `--adopt <target>` (a `dir/` prefix adopts every
  optional row under it), never touched when present, listed in the dry-run for reference when absent and
  **never pending, never re-asked on upgrade**; `ENABLE.md` Step 10 offers the pair once, at enable. Why not
  `seed-copy`: it would install governance ceremony into every enabled repo ("never heavyweight") and re-offer
  the pair after a team deletes it — the "deliberately absent" shape `seed-copy` cannot express
  (`ot-seed-copy-deliberate-absence`, RFC-0002 option b, now concrete). Half the family adopted ledgers by
  hand before this existed (mercury-composable 24 ADRs + a register, mercury 18).
  <!-- id: governance-pair-optional-seed | created: 2026-09-18 | last_used: 2026-09-18 | uses: 2 | tier: active | origin: 2026-09-18-234620 -->

## Open Threads

> Open Threads live **one per file** in `memory/open-threads/` (`thread-<id>.md`;
> filename = the thread's fact id) so concurrent thread work never merge-conflicts
> (v4.39.0 — `docs/DESIGN-merge-scale.md`). List that directory to see them; unchecked
> `- [ ]` threads are the live workstreams and never decay. Mark a completed thread
> `- [x]` in its file and leave it — the review sweeps it to the archive once older than
> `archive_window` sessions. Don't archive by hand. See `.agent/schema.md`.


## User Preferences

- Never expose the user's absolute home path (`/Users/<name>/…`) in file content —
  use `~`-relative paths. (Stated 2026-06-12; now enforced in ENABLE.md Step 5b +
  schema `repo:` guidance, and flagged by `memory-lint` `[secret-material]` since v4.33.0.)
- Any secrets — PII and credentials — must be redacted from session memory, never
  committed. (Stated 2026-08-13, after a client-side DLP catch; enforced via the
  `memory/PROTOCOL.md` redaction rule + `memory-lint` `[secret-material]`, v4.33.0.)
