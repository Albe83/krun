Role: ansibletask
=================

This role reconciles the `tasks.krun.io/v1alpha1` `AnsibleTask` custom resource.

Current scope (v1)
------------------

- Validate and normalize task semantics from `spec`.
- Publish a `Ready=True` condition when the semantic definition is accepted.
- Do **not** orchestrate host targeting, inventories, credentials, or remote execution yet.

Supported `spec` fields
-----------------------

- `action` (required): task action (typically a fully qualified Ansible module name).
- `args` (optional): free-form action arguments object.
- `name`, `when`, `tags`, `become`, `register`, `ignoreErrors` (optional).
- `changedWhen`, `failedWhen`, `loop`, `loopControl`, `until`, `retries`, `delay`, `checkMode`, `notify` (optional).

Status fields written by the role
---------------------------------

- `status.observedGeneration`
- `status.message`
- `status.conditions` (includes `type=Ready`, `reason=SpecAccepted`)
