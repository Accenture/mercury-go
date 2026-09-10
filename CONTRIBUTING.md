# Contributing to agent-memory

Thanks for taking the time to contribute!

The following is a set of guidelines for contributing to agent-memory — part of the Mercury
family of advanced software foundations for human–AI collaboration, hosted in the
[Accenture Organization](https://github.com/accenture) on GitHub. These are mostly
guidelines, not rules. Use your best judgment, and feel free to propose changes to this document
in a pull request.

## Code of Conduct

This project and everyone participating in it is governed by our
[Code of Conduct](CODE_OF_CONDUCT.md). By participating, you are expected to uphold this code.
Please report unacceptable behavior to Eric Law, who is the current project maintainer.
Our [Inclusive Language Guidebook](INCLUSIVITY.md) describes the language we use.

## What should I know before I get started?

We follow the [standard GitHub workflow](https://guides.github.com/introduction/flow/): every
change lands through a pull request. Before submitting a Pull Request:

- Please write tests. agent-memory is markdown-first, but its helpers are tested: the shell
  suites under `tests/` and the per-skill script tests under `agent-skills/*/scripts/` run in CI.
- Make sure you run all tests and check for warnings.
- Think about whether it makes sense to document the change in some way. For smaller, internal
  changes, inline documentation might be sufficient, while more visible ones might warrant a
  change to the docs site (`docs/`) or the [README](./README.md).
- Update `CHANGELOG.md` under the version being prepared with a short description of what the
  change is all about and a link to the issue or pull request. Version, `CHANGELOG.md`,
  `UPGRADE.md` and `MANIFEST.md` move in lockstep — see `UPGRADE.md` for the version ladder.
- Start your session from `AGENTS.md` if you work with an AI agent: this repository carries its
  own shared memory (`memory/`), and a session log is part of a complete change.

### Design Decisions

When we make a significant decision in how to write code, or how to maintain the project and
what we can or cannot support, we will document it using
[Architecture Decision Records (ADR)](http://thinkrelevance.com/blog/2011/11/15/documenting-architecture-decisions).
Take a look at the [ADR ledger](docs/arch-decisions/ADR.md) for existing ADRs.
If you have a question around how we do things, check to see if it is documented
there. If it is *not* documented there, please ask us - chances are you're not the only one
wondering. Of course, also feel free to challenge the decisions by opening a discussion or an
issue.
