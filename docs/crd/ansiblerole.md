# AnsibleRole CRD Reference

## Purpose and scope

`AnsibleRole` (`roles.krun.io/v1alpha1`) defines a reusable role composition as ordered references to `AnsibleTask` resources.

This CRD is semantic-only in v1:
- it models role phases (`preTasks`, `tasks`, `postTasks`, `handlers`),
- it validates structure and same-namespace task references,
- it does not execute hosts or inventories.

## API identity

- API group: `roles.krun.io`
- Version: `v1alpha1`
- Kind: `AnsibleRole`
- Plural: `ansibleroles`
- Singular: `ansiblerole`
- Short name: `arole`
- Scope: `Namespaced`

## Required and optional fields

### Required
- `spec.tasks`

### Optional
- `spec.preTasks`
- `spec.postTasks`
- `spec.handlers`

Each list item uses `{id, task}`:
- `id`: unique identifier within that list.
- `task`: referenced `AnsibleTask.metadata.name` in the same namespace.

## `spec` field reference

| Field | Type | Required | Purpose |
| --- | --- | --- | --- |
| `spec.preTasks` | `array[RoleTaskRef]` | No | Ordered tasks executed before main tasks. |
| `spec.tasks` | `array[RoleTaskRef]` | Yes | Ordered main role tasks (`minItems: 1`). |
| `spec.postTasks` | `array[RoleTaskRef]` | No | Ordered tasks executed after main tasks. |
| `spec.handlers` | `array[RoleTaskRef]` | No | Ordered handler task references. |

`RoleTaskRef` schema:

| Field | Type | Required | Purpose |
| --- | --- | --- | --- |
| `id` | `string` | Yes | Step identifier (unique per list). |
| `task` | `string` | Yes | Referenced `AnsibleTask` name in same namespace. |

## `status` field reference

| Field | Type | Purpose |
| --- | --- | --- |
| `status.observedGeneration` | `integer (int64)` | Last `metadata.generation` processed by operator. |
| `status.message` | `string` | Human-readable reconciliation message. |
| `status.conditions` | `array` | Standard condition list for state transitions. |

Common `Ready` reasons:
- `SpecAccepted`
- `SpecInvalid`
- `TaskReferenceNotFound`

## Examples

- Base sample: [`config/samples/roles_v1alpha1_ansiblerole.yaml`](../../config/samples/roles_v1alpha1_ansiblerole.yaml)
- Progressive examples: [`docs/examples/ansiblerole`](../examples/ansiblerole/README.md)
