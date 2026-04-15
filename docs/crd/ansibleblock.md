# AnsibleBlock CRD Reference

## Purpose and scope

`AnsibleBlock` (`blocks.krun.io/v1alpha1`) defines a reusable block composition as ordered references to `AnsibleTask` resources.

This CRD is semantic-only in v1:
- it models block phases (`block`, `rescue`, `always`),
- it validates structure and same-namespace task references,
- it does not execute hosts or inventories.

## API identity

- API group: `blocks.krun.io`
- Version: `v1alpha1`
- Kind: `AnsibleBlock`
- Plural: `ansibleblocks`
- Singular: `ansibleblock`
- Short name: `ablock`
- Scope: `Namespaced`

## Required and optional fields

### Required
- `spec.block`

### Optional
- `spec.rescue`
- `spec.always`

Each list item uses `{id, task}`:
- `id`: unique identifier within that list.
- `task`: referenced `AnsibleTask.metadata.name` in the same namespace.

## `spec` field reference

| Field | Type | Required | Purpose |
| --- | --- | --- | --- |
| `spec.block` | `array[BlockTaskRef]` | Yes | Ordered tasks in main block section (`minItems: 1`). |
| `spec.rescue` | `array[BlockTaskRef]` | No | Ordered tasks for rescue section. |
| `spec.always` | `array[BlockTaskRef]` | No | Ordered tasks for always section. |

`BlockTaskRef` schema:

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

- Base sample: [`config/samples/blocks_v1alpha1_ansibleblock.yaml`](../../config/samples/blocks_v1alpha1_ansibleblock.yaml)
- Progressive examples: [`docs/examples/ansibleblock`](../examples/ansibleblock/README.md)
