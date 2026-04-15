# Repository Guidelines

## Contribution Policy Source of Truth
For contribution governance (human developers + AI agents), follow [`CONTRIBUTING.md`](./CONTRIBUTING.md).
If this file and `CONTRIBUTING.md` diverge, `CONTRIBUTING.md` takes precedence.

## Project Structure & Module Organization
This repository is currently a minimal scaffold:
- `README.md`: top-level project description.
- `LICENSE`: project license terms.

When adding implementation code, keep a predictable layout:
- `src/` for application/runtime code.
- `tests/` for automated tests, mirroring `src/` paths.
- `docs/` for design notes and usage examples.
- `assets/` for static files (images, sample data) when needed.

Example: `src/runner/task.py` should have tests in `tests/runner/test_task.py`.

## Build, Test, and Development Commands
No build/test toolchain is configured yet. Until one is added, use lightweight checks:
- `git status` to verify intended file changes.
- `git diff --staged` to review staged content before commit.

If you introduce a language ecosystem, document and standardize commands in `README.md` (for example, `make test`, `npm test`, or `pytest`). Prefer one canonical command per activity (build, test, lint).

## Coding Style & Naming Conventions
Adopt consistent naming from the start:
- Directories/files: lowercase with separators (`kebab-case` or `snake_case`, choose one per language).
- Tests: `test_*.ext` naming.
- Keep modules focused and small; avoid mixing unrelated concerns.

Use the language-standard formatter/linter when added (for example, Prettier/ESLint for JS/TS, Ruff/Black for Python) and run it before opening a PR.

## Testing Guidelines
There is no test framework configured yet. For any non-trivial feature:
- add an automated test in `tests/`;
- cover normal flow and at least one edge case;
- document manual verification steps in the PR when automation is not yet available.

## Commit & Pull Request Guidelines
Git history currently starts with `Initial commit`; use clear, imperative commit subjects:
- `Add task runner skeleton`
- `Create CI workflow for unit tests`

PRs should include:
- a concise summary of changes,
- linked issue/reference when applicable,
- test evidence (command output or explanation),
- screenshots only for UI/visual changes.
