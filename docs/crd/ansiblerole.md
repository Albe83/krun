# AnsibleRole CRD Reference

## Purpose and scope

`AnsibleRole` (`roles.krun.io/v1alpha1`) defines a reusable role composition as ordered references to `AnsibleTask` and `AnsibleBlock` resources.

This CRD is semantic-only in v1:
- it models role phases (`preTasks`, `tasks`, `postTasks`, `handlers`),
- it validates structure and same-namespace references,
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

Each list item uses union `{id, task}` or `{id, block}`:
- `id`: unique identifier within that list.
- `task`: referenced `AnsibleTask.metadata.name` in the same namespace.
- `block`: referenced `AnsibleBlock.metadata.name` in the same namespace.

Exactly one of `task` or `block` must be set for each item.

## `spec` field reference

| Field | Type | Required | Purpose |
| --- | --- | --- | --- |
| `spec.preTasks` | `array[RoleEntryRef]` | No | Ordered entries executed before main phase. |
| `spec.tasks` | `array[RoleEntryRef]` | Yes | Ordered main role entries (`minItems: 1`). |
| `spec.postTasks` | `array[RoleEntryRef]` | No | Ordered entries executed after main phase. |
| `spec.handlers` | `array[RoleEntryRef]` | No | Ordered handler entries. |

`RoleEntryRef` schema:

| Field | Type | Required | Purpose |
| --- | --- | --- | --- |
| `id` | `string` | Yes | Step identifier (unique per list). |
| `task` | `string` | Conditionally | Referenced `AnsibleTask` name in same namespace. |
| `block` | `string` | Conditionally | Referenced `AnsibleBlock` name in same namespace. |

Condition: exactly one of `task` or `block` is required.

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
- `BlockReferenceNotFound`
- `BlockReferenceNotReady`

## Examples

- Base sample: [`config/samples/roles_v1alpha1_ansiblerole.yaml`](../../config/samples/roles_v1alpha1_ansiblerole.yaml)
- Progressive examples: [`docs/examples/ansiblerole`](../examples/ansiblerole/README.md)
- Cross-resource composition examples: [`docs/examples/composition`](../examples/composition/README.md)
- Domain class diagram: [`docs/crd/model.md`](./model.md)
