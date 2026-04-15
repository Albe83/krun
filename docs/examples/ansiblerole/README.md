# AnsibleRole Examples

This directory contains progressive `AnsibleRole` examples for `roles.krun.io/v1alpha1`.

## Prerequisites

Apply a referenced `AnsibleTask` first:

```bash
make install
kubectl apply -f config/samples/tasks_v1alpha1_ansibletask.yaml
```

## Apply examples

```bash
kubectl apply -f docs/examples/ansiblerole/01-minimal.yaml
kubectl apply -f docs/examples/ansiblerole/02-with-phases.yaml
kubectl apply -f docs/examples/ansiblerole/03-missing-reference.yaml
```

## Delete examples

```bash
kubectl delete -f docs/examples/ansiblerole/
```

## Example Index

| File | Focus |
| --- | --- |
| `01-minimal.yaml` | Minimal role with required `tasks` only |
| `02-with-phases.yaml` | Full composition across `preTasks`, `tasks`, `postTasks`, `handlers` |
| `03-missing-reference.yaml` | Negative example: missing task reference (`Ready=False`) |
