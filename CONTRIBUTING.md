# Contributing to krun

This policy applies to both human contributors and AI agents.

## Purpose

Keep contributions small, reviewable, and reproducible while preserving operator quality and safety.

## Development Workflow

1. Branch from `main`.
2. Keep each change focused on one intent (`feat`, `fix`, `docs`, `ci`, etc.).
3. Update docs/examples when CRD behavior or user-facing semantics change.
4. Open a PR with clear evidence of what was validated.

Useful commands:

- `make help`: list available development targets.
- `make install`: install CRDs in the current cluster.
- `make run`: run the Ansible operator locally.
- `make docker-build IMG=<image:tag>`: build operator image.

## Commit Convention

Use imperative and concise subjects. Preferred format:

- `<type>: <summary>`

Examples:

- `feat: add ansibletask retry controls`
- `docs: document checkMode and notify semantics`
- `ci: validate ansibletask examples in workflow`

## Pull Request Requirements

Each PR must include:

- concise summary and motivation;
- linked issue or ADR when applicable;
- validation evidence (commands executed and result);
- impact note for risky changes (rollback or mitigation).

## AI Agent Policy (Human-in-the-loop)

AI can assist with analysis, code, and documentation, but accountability stays with a human maintainer.

- AI-generated changes must be reviewed and approved by a human before merge.
- PRs must disclose AI assistance (what was generated vs. reviewed/edited by human).
- AI contributors must not push directly to protected branches.
- Never include secrets, tokens, or sensitive data in prompts, commits, or logs.
- Avoid destructive git operations on shared branches/history.

## Review and Merge Gate

Merge only when:

- CI checks pass;
- at least one human reviewer approves;
- PR description is complete and traceable.
