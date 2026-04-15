# Architecture Decision Records

This directory contains the Architecture Decision Records (ADRs) for `krun`.

## Conventions

- Numbering: `000N` (incremental, immutable once published).
- Status values: `Proposed`, `Accepted`, `Superseded`.
- File name format: `000N-short-kebab-title.md`.

## Index

| ID | Title | Status | Date |
| --- | --- | --- | --- |
| [0001](./0001-ansibletask-semantic-not-execution.md) | AnsibleTask models task semantics, not runtime execution | Accepted | 2026-04-15 |
| [0002](./0002-ansibletask-namespaced-scope.md) | AnsibleTask is namespaced | Accepted | 2026-04-15 |
| [0003](./0003-use-action-instead-of-module.md) | Use `spec.action` instead of `spec.module` | Accepted | 2026-04-15 |
| [0004](./0004-camelcase-crd-and-advanced-task-controls.md) | Keep camelCase CRD API and map to Ansible keywords | Accepted | 2026-04-15 |
| [0005](./0005-ansiblerole-semantic-composition.md) | Introduce `AnsibleRole` as semantic composition of task references | Accepted | 2026-04-15 |
| [0006](./0006-ansibleblock-semantic-composition.md) | Introduce `AnsibleBlock` as semantic composition of task references | Accepted | 2026-04-15 |
