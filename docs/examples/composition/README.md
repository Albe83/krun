# Task -> Block -> Role Composition Examples

This directory shows end-to-end semantic composition:
1. define reusable tasks,
2. group tasks into blocks,
3. compose roles from blocks.

## Apply in order

```bash
make install
kubectl apply -f docs/examples/composition/01-tasks.yaml
kubectl apply -f docs/examples/composition/02-blocks.yaml
kubectl apply -f docs/examples/composition/03-role-from-blocks.yaml
kubectl apply -f docs/examples/composition/04-role-mixed.yaml
kubectl apply -f docs/examples/composition/05-real-nginx-tasks.yaml
kubectl apply -f docs/examples/composition/06-real-nginx-blocks.yaml
kubectl apply -f docs/examples/composition/07-real-nginx-role.yaml
```

## Cleanup

```bash
kubectl delete -f docs/examples/composition/
```

## Realistic Nginx scenario

The `05/06/07` files model a realistic install-and-configure flow while staying semantic-only:

- `05-real-nginx-tasks.yaml`: reusable task semantics for package install, config deployment, validation, service management, assertions, and handler actions.
- `06-real-nginx-blocks.yaml`: grouped rollout logic with:
  - main configure path,
  - `rescue` rollback path,
  - `always` summary/assert path.
- `07-real-nginx-role.yaml`: role composition using blocks and direct tasks together (`task` + `block` references in the same role).

Even though this project currently validates semantics (not remote execution), this set demonstrates how real operations can be modeled with combined `AnsibleTask`, `AnsibleBlock`, and `AnsibleRole` resources.
