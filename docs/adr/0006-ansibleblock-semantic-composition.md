# ADR 0006: Introduce AnsibleBlock as semantic composition of task references

- Status: Accepted
- Date: 2026-04-15

## Context

`AnsibleTask` models a single task and `AnsibleRole` models role phases.
We need a dedicated resource for Ansible `block` semantics (`block/rescue/always`) without adding execution concerns.

## Decision

Add `AnsibleBlock` (`blocks.krun.io/v1alpha1`, namespaced) with:
- required `spec.block` (`minItems: 1`),
- optional `spec.rescue`, `spec.always`,
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

- Adds a reusable semantic block abstraction aligned with Ansible taxonomy.
- Keeps compatibility with current semantic-only milestone.
- Defers nested block composition and runtime execution semantics to future iterations.
