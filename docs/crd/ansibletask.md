# AnsibleTask CRD Reference

## Purpose and scope

`AnsibleTask` (`tasks.krun.io/v1alpha1`) defines the semantics of one Ansible task as a reusable Kubernetes resource.

This CRD is a semantic building block, not a runtime execution job:
- it stores task intent (`action`, arguments, conditions, loop/retry logic, etc.),
- it is designed to be composed by higher-level resources,
- it does not model host inventory or execution history in this version.

## API identity

- API group: `tasks.krun.io`
- Version: `v1alpha1`
- Kind: `AnsibleTask`
- Plural: `ansibletasks`
- Singular: `ansibletask`
- Short name: `atask`
- Scope: `Namespaced`

## Required and optional fields

### Required
- `spec.action`

### Optional
- `spec.args`
- `spec.when`
- `spec.tags`
- `spec.become`
- `spec.register`
- `spec.ignoreErrors`
- `spec.changedWhen`
- `spec.failedWhen`
- `spec.loop`
- `spec.loopControl`
- `spec.until`
- `spec.retries`
- `spec.delay`
- `spec.checkMode`
- `spec.notify`

## `spec` field reference

| Field | Type | Required | Purpose | Ansible mapping | Official docs |
| --- | --- | --- | --- | --- | --- |
| `spec.action` | `string` | Yes | Task action to execute (usually module FQCN). | `action` / module invocation | [Playbook Keywords](https://docs.ansible.com/projects/ansible/latest/reference_appendices/playbooks_keywords.html), [Module Index](https://docs.ansible.com/projects/ansible/latest/collections/index_module.html) |
| `spec.args` | `object` | No | Parameters for the selected action/module. | module/action arguments | [Module Index](https://docs.ansible.com/projects/ansible/latest/collections/index_module.html) |
| `spec.when` | `string` | No | Conditional expression for task execution. | `when` | [Conditionals](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_conditionals.html) |
| `spec.tags` | `array[string]` | No | Tag list for selective execution. | `tags` | [Tags](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_tags.html) |
| `spec.become` | `boolean` | No | Enable/disable privilege escalation. | `become` | [Privilege Escalation](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_privilege_escalation.html) |
| `spec.register` | `string` | No | Store task result in a variable name. | `register` | [Registering variables](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_variables.html#registering-variables) |
| `spec.ignoreErrors` | `boolean` | No | Continue execution if task fails. | `ignore_errors` | [Error handling](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_error_handling.html) |
| `spec.changedWhen` | `string` | No | Override changed-state evaluation. | `changed_when` | [Error handling](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_error_handling.html) |
| `spec.failedWhen` | `string` | No | Override failure-state evaluation. | `failed_when` | [Error handling](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_error_handling.html) |
| `spec.loop` | `array[string]` | No | Items processed by task loop. | `loop` | [Loops](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_loops.html) |
| `spec.loopControl` | `object` | No | Loop behavior controls (for example `loopVar`). | `loop_control` | [Loops](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_loops.html) |
| `spec.until` | `string` | No | Retry-until condition. | `until` | [Loops](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_loops.html) |
| `spec.retries` | `integer` | No | Max retries for `until`. | `retries` | [Loops](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_loops.html) |
| `spec.delay` | `integer` | No | Delay in seconds between retries. | `delay` | [Loops](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_loops.html) |
| `spec.checkMode` | `boolean` | No | Force or disable check-mode behavior for task. | `check_mode` | [Check mode](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_checkmode.html) |
| `spec.notify` | `array[string]` | No | Notify handlers when task reports changed. | `notify` | [Handlers](https://docs.ansible.com/projects/ansible/latest/playbook_guide/playbooks_handlers.html) |

## `status` field reference

`status` is populated by the operator reconciliation logic and reports acceptance/observed state of the CR.

| Field | Type | Purpose |
| --- | --- | --- |
| `status.observedGeneration` | `integer (int64)` | Last `metadata.generation` processed by the operator. |
| `status.message` | `string` | Human-readable reconciliation message. |
| `status.conditions` | `array` | Standard condition list for state transitions. |
| `status.conditions[].type` | `string` | Condition type (for example `Ready`). |
| `status.conditions[].status` | `string` | Condition status: `True`, `False`, or `Unknown`. |
| `status.conditions[].reason` | `string` | Short machine-oriented reason. |
| `status.conditions[].message` | `string` | Human-oriented explanation. |
| `status.conditions[].lastTransitionTime` | `string (date-time)` | Timestamp of last status transition. |
| `status.conditions[].observedGeneration` | `integer (int64)` | Generation observed when condition was set. |

## Examples

- Base sample managed with operator scaffold: [`config/samples/tasks_v1alpha1_ansibletask.yaml`](../../config/samples/tasks_v1alpha1_ansibletask.yaml)
- Progressive examples: [`docs/examples/ansibletask`](../examples/ansibletask/README.md)

## Notes

- API style is camelCase in CRD fields, with internal mapping to Ansible snake_case keywords where applicable.
- Canonical action field is `spec.action` (`spec.module` is not part of the current API contract).
- Task name is derived from `metadata.name`; `spec.name` is not part of the current API contract.
