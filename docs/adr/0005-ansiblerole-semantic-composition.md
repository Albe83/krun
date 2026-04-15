# ADR 0005: Introduce AnsibleRole as semantic composition of AnsibleTask references

- Status: Accepted
- Date: 2026-04-15

## Context

`AnsibleTask` already models one task semantic block.
We need a first role-level resource that composes tasks into role phases without introducing execution concerns.

## Decision

Add `AnsibleRole` (`roles.krun.io/v1alpha1`, namespaced) with:
- required `spec.tasks` (`minItems: 1`),
- optional `spec.preTasks`, `spec.postTasks`, `spec.handlers`,
- list item schema `{id, task}` where:
  - `id` is unique per list,
  - `task` references `AnsibleTask.metadata.name` in the same namespace.

Reconciliation validates:
- structural correctness,
- per-list duplicate `id`,
- existence of referenced `AnsibleTask` resources.

Status model:
- `Ready=True`, `reason=SpecAccepted` when valid,
- `Ready=False`, `reason=SpecInvalid` for malformed/duplicate IDs,
- `Ready=False`, `reason=TaskReferenceNotFound` when references are missing.

`watches.yaml` configures periodic reconciliation (`60s`) for eventual consistency.

## Consequences

- Establishes a reusable role abstraction without coupling to runtime execution.
- Keeps compatibility with current semantic-only milestone.
- Defers cross-namespace references and notify/handler binding validation to future iterations.
