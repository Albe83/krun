# ADR 0003: Use `spec.action` instead of `spec.module`

- Status: Accepted
- Date: 2026-04-15

## Context

In Ansible task taxonomy, `action` is the canonical task keyword, while module name is commonly used as shorthand syntax.
The CRD originally used `spec.module`.

## Decision

Adopt `spec.action` as the required field and remove `spec.module` from the API contract.
This is an explicit breaking change within `v1alpha1`.

## Consequences

- API terminology is aligned with Ansible's task model.
- Existing manifests using `spec.module` must migrate to `spec.action`.
- Validation and reconciliation logic remain simple (single canonical field).

## Alternatives Considered

- Keep `module` forever: rejected due to terminology drift.
- Support both `action` and `module`: rejected to avoid ambiguity and dual-path behavior.
