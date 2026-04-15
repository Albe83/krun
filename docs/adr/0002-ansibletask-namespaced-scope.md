# ADR 0002: AnsibleTask is namespaced

- Status: Accepted
- Date: 2026-04-15

## Context

The operator will be used in Kubernetes environments where isolation between teams/environments is required.
The `AnsibleTask` CRD needs a clear tenancy boundary.

## Decision

`AnsibleTask` is defined with `spec.scope: Namespaced`.

## Consequences

- Task definitions are isolated per namespace.
- RBAC and operational ownership can align with namespace boundaries.
- Future composition resources can reference tasks within their namespace by default.

## Alternatives Considered

- Cluster-scoped `AnsibleTask`: rejected because it weakens namespace isolation and increases governance complexity.
