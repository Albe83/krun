# ADR 0007: Extend AnsibleRole entries to reference either AnsibleTask or AnsibleBlock

- Status: Accepted
- Date: 2026-04-15

## Context

`AnsibleBlock` now exists and groups tasks into `block/rescue/always` sections.
To demonstrate composition `task -> block -> role`, `AnsibleRole` must reference blocks directly.

## Decision

Keep `roles.krun.io/v1alpha1` and extend role phase entries (`preTasks`, `tasks`, `postTasks`, `handlers`) to use union items:
- `{id, task}` or `{id, block}`
- exactly one between `task` and `block` must be set.

Other rules:
- `spec.tasks` remains required (`minItems: 1`) for backward compatibility.
- `id` remains unique per phase.
- `task` and `block` references are namespaced and resolved in the same namespace.

Reconcile status behavior:
- `TaskReferenceNotFound` for missing task refs,
- `BlockReferenceNotFound` for missing block refs,
- `BlockReferenceNotReady` for block refs not yet `Ready=True`.

## Consequences

- Existing task-only role specs remain valid.
- New role specs can compose reusable blocks.
- Nested role composition and runtime execution remain out of scope.
