Role: ansiblerole
=================

This role reconciles the `roles.krun.io/v1alpha1` `AnsibleRole` custom resource.

Current scope (v1)
------------------

- Validate role structure (`preTasks`, `tasks`, `postTasks`, `handlers`) where each entry is `{id, task}`.
- Validate per-list `id` uniqueness.
- Validate that all referenced `AnsibleTask` resources exist in the same namespace.
- Publish a `Ready` condition:
  - `Ready=True`, `reason=SpecAccepted` when structure and references are valid;
  - `Ready=False`, `reason=SpecInvalid` for malformed sections/ids;
  - `Ready=False`, `reason=TaskReferenceNotFound` when references are missing.

Non-goals in this version
-------------------------

- No remote execution/inventory orchestration.
- No `notify` to `handlers` binding validation.
