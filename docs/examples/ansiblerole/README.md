# AnsibleRole Examples

This directory contains progressive `AnsibleRole` examples for `roles.krun.io/v1alpha1`.

## Prerequisites

Apply referenced resources first:

```bash
make install
kubectl apply -f config/samples/tasks_v1alpha1_ansibletask.yaml
kubectl apply -f config/samples/blocks_v1alpha1_ansibleblock.yaml
```

## Apply examples

```bash
kubectl apply -f docs/examples/ansiblerole/01-minimal.yaml
kubectl apply -f docs/examples/ansiblerole/02-with-phases.yaml
kubectl apply -f docs/examples/ansiblerole/03-missing-reference.yaml
kubectl apply -f docs/examples/ansiblerole/04-with-blocks.yaml
kubectl apply -f docs/examples/ansiblerole/05-mixed-task-block.yaml
kubectl apply -f docs/examples/ansiblerole/06-missing-block-reference.yaml
```

## Delete examples

```bash
kubectl delete -f docs/examples/ansiblerole/
```

## Example Index

| File | Focus |
| --- | --- |
| `01-minimal.yaml` | Minimal role with required `tasks` only (`task` reference) |
| `02-with-phases.yaml` | Full task-only composition across phases |
| `03-missing-reference.yaml` | Negative example: missing task reference (`Ready=False`) |
| `04-with-blocks.yaml` | Role composition using block references |
| `05-mixed-task-block.yaml` | Mixed task+block composition in same phase |
| `06-missing-block-reference.yaml` | Negative example: missing block reference (`Ready=False`) |
