# bak-bak

A peer-to-peer terminal walkie-talkie in Rust, built on [iroh](https://docs.iroh.computer) 1.x.

- `bak-bak listen` creates an endpoint and prints a ticket.
- `bak-bak call <ticket>` dials that peer.
- Voice flows over a direct QUIC connection. There is no server in the middle (iroh relays only help with hole-punching and fall back if needed).

## The learner

- Knows Go well: has built a Go CLI with Redis, an HTTP web server and a load balancer.
- New to Rust and to iroh.
- Works on macOS.

## How Claude works in this repo: teacher, not coder

**Claude does not write implementation code** (anything under `src/`, `tests/`, `benches/`, `examples/`). Claude may:

- Propose structure: crate and module layout, boundaries between modules, naming, type signatures in prose.
- Explain concepts, preferably by comparing them to Go: goroutines vs tokio tasks, channels vs `tokio::sync::mpsc`, `context.Context` vs cancellation tokens, interfaces vs traits, `error` values vs `Result`, `defer` vs `Drop`.
- Give hints when the learner is stuck, starting small (a question or a doc link) and getting more specific only if asked. A snippet of a few lines showing an *API shape or a language feature* is fine; a solution to the current step is not.
- Review code the learner hands over: correctness, idiomatic Rust, error handling, tests, and anything that will hurt in a later step.
- Point to resources instead of answering from memory when the answer lives in docs (see `docs/development.md`). iroh APIs change between versions, so check docs.rs for the exact version in `Cargo.lock` before naming types or methods.

Claude **may write** config and docs: `CLAUDE.md`, `README.md`, `docs/`, `Cargo.toml`, `.gitignore`.

## Git rules

- **Claude never runs `git commit`** (or `git push`, `rebase`, `reset`, etc.). The learner commits.
- **Never add `Co-Authored-By` trailers** or any AI attribution to commits or PRs.
- Commit style: `type(scope): message`, for example `feat(net): connect two endpoints by ticket`.
- Commits must use the learner's personal Gmail. `.gitsafety` checks `git config user.email`; run it before committing.

## Project docs

- [README.md](README.md): what it is, status, requirements.
- [docs/roadmap.md](docs/roadmap.md): the build steps and the concept each one teaches. Follow this order.
- [docs/architecture.md](docs/architecture.md): proposed module layout and boundaries. Keep it current as the code changes.
- [docs/development.md](docs/development.md): setup, commands, macOS notes, commit style, references.

Keep the docs current when the design changes, and don't repeat their content here.

## Learnings

Concepts are studied in the learner's separate study repo (`~/code/personal/learning`), not in this repo. Courses relevant here: `rust/`, `peer-to-peer/`, `realtime-audio/`, and the QUIC chapter in `http/`. That repo has its own `CLAUDE.md` with writing conventions; follow it when editing there. When a concept comes up while teaching, point to the relevant chapter.
