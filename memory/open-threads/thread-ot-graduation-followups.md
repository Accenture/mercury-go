- [ ] (ops) **Graduation follow-ups — the org home `Accenture/mercury-go`** (opened 2026-09-10 at
  graduation; each item is Eric's call or a repo setting only an admin can flip):
  1. ~~Enable GitHub Pages~~ — done by GitHub itself: pushing `gh-pages` auto-enabled Pages
     (source `gh-pages` / root); `accenture.github.io/mercury-go/` live (HTTP 200) and the first
     `docs` run pushed `gh-pages` fine under the org's token policy (2026-09-10).
  2. Fate of `acn-ericlaw/agent-memory` and its site: redirection notices added 2026-09-10 at the
     top of its `README.md` and `docs/index.md` (pending Eric's push); remaining — archive the
     repository on GitHub once pushed. The commit transfer left stars/issues/PR history behind
     (PR links in older logs resolve there).
  3. ~~`LICENSE` copyright line~~ — done 2026-09-10 on Eric's directive: "Copyright 2026 Accenture"
     (README License section and whitepaper Status line carry it too).
  4. ~~Repo metadata~~ — description + homepage set 2026-09-10 via `gh repo edit` (needed the
     `acn-ericlaw` account; the EMU account got a 404). The stale `dev` branch (a React
     flow-editor prototype) deleted by Eric 2026-09-10 — `main` + `gh-pages` are the only
     branches. (Contribution workflow is settled: PR required — Eric, 2026-09-10; recorded in
     `github-origin-mercury-go`.)
  5. ~~Attribution locators in the engines' white papers~~ — landed as PRs
     Accenture/mercury-composable#350 and Accenture/mercury#253 (2026-09-10): closing note
     "part of the Mercury family (github.com/Accenture/mercury-go)" + References #20 → the
     agent-memory whitepaper at the official site; the Java repo's thread is closed.
  6. ~~Dependabot Accenture/mercury-go#1~~ (org-level Dependabot; the repo ships no
     `.github/dependabot.yml`): `mkdocs-material` 9.7.6 → 9.7.7 — merged by Eric 2026-09-10
     together with #2 (branding / license / "Part of the Mercury family" wording); the strict
     `docs` build passed on the merged `main` and the live site shows the new footer and the
     family page. **Only item 2 remains open.**
  <!-- id: ot-graduation-followups | created: 2026-09-10 | last_used: 2026-09-10 | uses: 1 | tier: working | origin: 2026-09-10-152543 -->
