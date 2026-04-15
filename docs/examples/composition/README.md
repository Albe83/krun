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
```

## Cleanup

```bash
kubectl delete -f docs/examples/composition/
```
