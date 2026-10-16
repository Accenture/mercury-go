# Agent Instructions — agent-memory

> Project context + architecture for **any** agent (Claude, Gemini, Cursor, …) working on
> this repo. Vendor-neutral by design — the bootstrap files (`CLAUDE.md`, `GEMINI.md`, …)
> are thin pointers; this is where the substance lives.

## What This Project Is

`agent-memory` is a **no-code, markdown-only** system with three jobs in one repo:

1. **A shared memory system** — a `memory/` layer that persists project context across
   sessions and across different AI vendors. It *evolves*: facts carry usage metadata,
   fade through tiers, and archive when stale, recomputed deterministically from the
   session-log event stream (`DECAY.md`). On top of that backward-looking substrate sits
   the **forward cognitive loop (VBDI, v4.0.0)**: Current State → Vision → Blueprint →
   Design → Implementation → Feedback (`DECAY.md` §12).
2. **An AI-enablement tool** — point it at any other repo to generate a tailored memory
   system there.
3. **A migration tool** — when the target repo already has vendor AI files (Cursor,
   Aider, Continue, Cline, …), fold them into the unified format.

**Type:** Developer tooling / meta-framework. **Primary language:** Markdown — there is
**no build, lint, or test step**; the markdown files *are* the product, and the "runtime"
is an AI agent reading them. Validation is manual: confirm the protocol files read
unambiguously and that `examples/` still reflect documented behavior.

> **Control flow.** Every agent enters via its bootstrap pointer (`CLAUDE.md`, `GEMINI.md`,
> `.cursorrules`, …) or the exact one-line root **`AGENTS.md`** shim →
> **`memory/PROTOCOL.md`**, which branches: working *within* this repo → activate shared
> memory; *AI-enabling another repo* → `ENABLE.md` (then `MIGRATE.md`/`UPGRADE.md` as it
> directs). Don't improvise from memory — read the protocol file.

## Repository Structure — how the files relate

The system is layered, and the layering is the design (README "Two Layers"):

- **Root bootstrap files** (`CLAUDE.md`, `GEMINI.md`, `AGENTS.md`, `.cursorrules`,
  `.windsurfrules`, `.github/copilot-instructions.md`) — thin activation pointers;
  `AGENTS.md` is the universal one-line shim to `memory/PROTOCOL.md`.
- **`ENABLE.md`** — enablement protocol (detect footprint → Mode A/B/C → analyze →
  generate). **`MIGRATE.md`** — per-vendor detection + conversion, only via Mode C.
  **`UPGRADE.md`** — in-place version-upgrade ladder, only via Mode B. `MIGRATE.md` and
  `UPGRADE.md` are tool-operator-only (never installed into targets).
- **Evolving-memory layer (backward)** — `DECAY.md` (metadata, tiers, deterministic decay
  — no floating-point scoring) and `REVIEW.md` (the review ritual). Generic and *installed
  into every enabled repo's root*. `VERSION` = the tool's semver; each enabled repo stamps
  `.agent/version.md`.
- **Forward layer (VBDI, v4.0.0)** — `memory/vision.md` (north star) + Blueprint as typed
  `(blueprint)` Open Threads + the altitude trace (`serves:` / `id`). Rules in `DECAY.md`
  §12 (+ the §10 drift check); design rationale in `docs/DESIGN-vbdi-lifecycle.md`
  (tool-only). Enable/upgrade **bootstrap a DRAFT Vision and gate it** — never fabricated.
- **`templates/`** — exactly what installs into a target repo: bootstrap files + `memory/`
  files with `{{UPPER_SNAKE_CASE}}` placeholders (incl. `decay-policy.md`, `vision.md`),
  `.agent/schema.md` (canonical memory-file format, copied verbatim), `.agent/version.md`.
- **`memory/`** — this repo's *own* memory layer (it eats its own dog food):
  `PROTOCOL.md` (dual-mode operator/session protocol), this file,
  `continuity.md` (live state + Architectural Invariants + Blueprint), `vision.md`,
  `decay-policy.md`, `sessions/` (immutable event log), `archive/`, `smoke-test.md`.
- **`examples/`** — real filled-in output, not placeholders: `rust-event-bus/` (Mode A),
  `migrated-cursor-aider-project/` (Mode C), `evolving-memory-example/` (the review cycle).
- **`docs/`** — design rationale + assessments (`DESIGN-evolving-memory.md`,
  `DESIGN-vbdi-lifecycle.md`, `architecture/security.md`,
  `agent-cognitive-framework.md`, `assessments/`).

**Changes span layers in lockstep:** a new vendor → a row in `MIGRATE.md`'s table + a
per-vendor section + the supported-vendor tables in `README.md` and `memory/PROTOCOL.md`. A
memory-file shape change → `templates/`, `templates/.agent/schema.md`, and `examples/`
together. An evolving-memory change → `DECAY.md`, `REVIEW.md`,
`templates/memory/decay-policy.md`, the schema, and `examples/evolving-memory-example/`;
if the shape changes, bump `VERSION` and add an `UPGRADE.md` rung.

## Non-Negotiable Constraints

The core safety philosophy (also pinned as Architectural Invariants in `continuity.md`):

- **Target-repo scope only.** Never read/modify/move/list anything outside the resolved
  target-repo root — never `~`, `~/.claude/`, Application Support, AppData, or system
  paths. Resolve symlinks first; report any path that escapes. The user's home dir is
  *their* personal AI environment; the repo's `memory/` is the *team's* shared layer.
- **Never delete vendor files** — move originals to `legacy/<vendor>/`, preserving paths.
- **Never overwrite, never pick a winner** — fold vendor steering under `## Migrated rules
  from <vendor>`; surface contradictions as Open Threads.
- **Never modify source code or package manifests** in a target repo.
- **Idempotent + additive** — Mode B detects "already ours" (older → upgrade in place via
  `UPGRADE.md`); dry-run supported; upgrades only enrich and add, never rewrite or delete.

## Conventions

- Placeholders use `{{UPPER_SNAKE_CASE}}`; templates mirror final output exactly; examples
  show real content, never placeholders.
- "Ours vs. vendor" for shared filenames (`CLAUDE.md`, `AGENTS.md`, …) is decided by
  content: ours references the agent-memory system / `memory/instructions.md`.
- Remind the user to commit memory changes:
  `git add memory/ && git commit -m "session YYYY-MM-DD [agent]"`.

## Core Rules

1. If asked to AI-enable a repo, read `ENABLE.md` before anything; never copy templates
   blindly — analyse the target first.
2. Never modify source code in target repos — only create memory and bootstrap files.
3. Templates in `templates/` are the structure guide; keep the layers in lockstep.
4. Record every session in this repo's own session log; update `continuity.md` after.
5. If you see a TODO, contradiction, or drift, surface it as an Open Thread — never
   silently reconcile or pick a winner.
6. **Compartmentalize downstream secrets (standing instruction, Eric, 2026-09-30).** This
   repository and its siblings — `mercury`, `mercury-composable`, `mercury-python`,
   `mercury-nodejs`, `mercury-go` — are open source. Nothing that identifies a downstream
   adopter may enter them: **customer or company names and brands, project and repository
   names, people's names, and other project-identifiable data** (pilot lengths and dates,
   internal RFC/ticket ids, business-domain specifics, hostnames, cloud accounts). This
   covers code, tests, docs, commit messages, PR text, and above all `memory/` — session
   logs, `continuity.md`, `open-threads/`, archives, and any ADR/RFC entries. A downstream
   brand name is never recorded in session memory or in any open thread.
   - **Refer to it generically:** "a downstream adopter", "the field" (client production
     installations that consume Mercury releases through their own governed pipelines), "a
     field installation". Describe the *technical* need, not whose need it was or what
     business it serves; generalize a domain-specific example (e.g. "financial contracts",
     not the adopter's industry niche).
   - **Input documents from a downstream project** (feature requests, design drafts) may name
     their origin. Read them, but scrub before anything is copied into this repo: names,
     "prepared in <their repo>", their internal RFC numbers, adopter-specific use cases.
     Cite them in memory only as "a downstream design draft" — never by path or repo name.
   - **Scan before committing or opening a PR:** `git diff` (and staged memory) for any
     identifier from the source material. If something leaks, stop and tell Eric before
     pushing; history on `main` is append-only, so a leak cannot be quietly undone.
   - **The field's infrastructure cost and setup issues are out of scope too (Eric, 2026-10-16):**
     an API credit balance, cloud account setup, expired credentials, model access gating and
     similar matters are outside this open-source project's control and are escalated to the
     field admin. They are never logged here, in memory or in docs; a record says what the
     project did and learned, not what the field's infrastructure did.
   - Applies to every agent and every session, including lightweight logs, and to any memory
     this tool generates for a target repo. The rule's history lives in mercury-composable
     (`memory/instructions.md` Core Rule 6, fact `conv-compartment-downstream-secrets`).

## Testing & CI / CD

None — no build/lint/test step. Validation is manual: the protocol files must read
unambiguously, and `examples/` must reflect documented behavior.
