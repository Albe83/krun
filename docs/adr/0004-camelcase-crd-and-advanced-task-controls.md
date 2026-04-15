# ADR 0004: Keep camelCase CRD API and map to Ansible keywords

- Status: Accepted
- Date: 2026-04-15

## Context

The CRD API uses camelCase field names (`ignoreErrors`, etc.).
We also need to expose additional task controls that map to standard Ansible task keywords.

## Decision

Keep camelCase as the public CRD style and map internally to Ansible snake_case where needed.
Added task controls in `spec`:

- `changedWhen` -> `changed_when`
- `failedWhen` -> `failed_when`
- `loop`
- `loopControl` -> `loop_control`
- `until`
- `retries`
- `delay`
- `checkMode` -> `check_mode`
- `notify`

## Consequences

- CRD remains stylistically consistent for API consumers.
- Reconciler/role performs deterministic name mapping to Ansible semantics.
- More task-level logic is expressible without expanding runtime orchestration scope.

## Alternatives Considered

- Expose snake_case directly in CRD: rejected for API style inconsistency.
- Support both camelCase and snake_case in CRD: rejected to avoid duplicate fields and validation ambiguity.
