Role: ansiblerole
=================

This role reconciles the `roles.krun.io/v1alpha1` `AnsibleRole` custom resource.

Current scope (v1)
------------------

- Validate role structure (`preTasks`, `tasks`, `postTasks`, `handlers`) where each entry is `{id, task}` or `{id, block}`.
- Validate per-list `id` uniqueness.
- Validate that all referenced `AnsibleTask` and `AnsibleBlock` resources exist in the same namespace.
- Validate that referenced `AnsibleBlock` resources are `Ready=True`.
- Publish a `Ready` condition:
  - `Ready=True`, `reason=SpecAccepted` when structure and references are valid;
  - `Ready=False`, `reason=SpecInvalid` for malformed sections/items;
  - `Ready=False`, `reason=TaskReferenceNotFound` for missing task refs;
  - `Ready=False`, `reason=BlockReferenceNotFound` for missing block refs;
  - `Ready=False`, `reason=BlockReferenceNotReady` for block refs not yet ready.

Non-goals in this version
-------------------------

- No remote execution/inventory orchestration.
- No nested role composition.
