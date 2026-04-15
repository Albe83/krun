# ADR 0001: AnsibleTask models task semantics, not runtime execution

- Status: Accepted
- Date: 2026-04-15

## Context

The first resource in this operator is `AnsibleTask` (`tasks.krun.io/v1alpha1`).
We need a reusable unit to compose future higher-level resources (for example an `AnsibleRole` CR), without coupling this first step to runtime orchestration concerns.

## Decision

`AnsibleTask` represents the semantic definition of one Ansible task (action + options).
It is not treated as a runtime execution job.
The operator validates and normalizes the task definition and sets status conditions for acceptance.

## Consequences

- The CRD remains reusable as a building block for future composition.
- Runtime concerns (inventory, credentials, host targeting, execution history) are deferred.
- Status communicates resource acceptance, not execution outcomes on target systems.

## Alternatives Considered

- Model `AnsibleTask` as a one-shot execution CR: rejected to avoid mixing definition and execution concerns in v1.
- Model `AnsibleTask` as continuous desired-state execution: rejected for same reason and higher complexity.
