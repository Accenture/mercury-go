- [ ] **Drop the redundant `thread-` filename prefix in `memory/open-threads/` (backlog — parked).**
  Inside a directory already named `open-threads/`, `thread-<id>.md` adds nothing (mercury-composable
  note, 2026-09-18, filed as cosmetic and accepted as such; the second layer of the stutter —
  kind-prefixed ids — was fixed as guidance in v4.41.1). Parked, not planned: reactivate only when a
  field installation asks; if still untouched at a closure gate, close it as deliberately dropped. If
  ever done, the whole of it is: (1) the one production line per runtime — memory-lint check 12's
  `expect = f"thread-{fid}.md"` / `thread-${fid}.md` — accepting `<id>.md` (everything else globs
  `*.md` and keys on the footer id: `refresh-metadata`, `archive-fact`, `[undeclared-reference]`), then
  a `git mv` of each file with **ids untouched** (an id is permanent; renaming one orphans its
  immutable-log declarations — `DECAY.md` §1); (2) ~22 doc lines across 15 lockstep surfaces plus the
  shell-test fixtures; (3) the schema sentence "the filename is the identity and never changes",
  reworded in the same release; (4) the in-flight-branch hazard — a branch adding `thread-foo.md`
  while main has `foo.md` merges cleanly into two files for one thread; `[duplicate-id]` catches it
  before merge on GitHub (the floor lints the PR's merge commit) but after merge on GitLab
  source-branch pipelines and local merges — so an upgrade step should detect and collapse that case
  rather than leave it to the lint. Not additive-only (accept both shapes forever): a mixed directory
  for the life of long-lived blueprint threads undercuts the legibility gain that motivates the change.
  <!-- id: open-threads-filename-prefix | created: 2026-09-18 | last_used: 2026-09-18 | uses: 1 | tier: working | origin: 2026-09-18-215724 -->
