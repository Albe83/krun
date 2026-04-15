# AnsibleBlock Examples

This directory contains progressive `AnsibleBlock` examples for `blocks.krun.io/v1alpha1`.

## Prerequisites

Apply a referenced `AnsibleTask` first:

```bash
make install
kubectl apply -f config/samples/tasks_v1alpha1_ansibletask.yaml
```

## Apply examples

```bash
kubectl apply -f docs/examples/ansibleblock/01-minimal.yaml
kubectl apply -f docs/examples/ansibleblock/02-with-rescue-always.yaml
kubectl apply -f docs/examples/ansibleblock/03-missing-reference.yaml
```

## Delete examples

```bash
kubectl delete -f docs/examples/ansibleblock/
```

## Example Index

| File | Focus |
| --- | --- |
| `01-minimal.yaml` | Minimal block with required `block` section only |
| `02-with-rescue-always.yaml` | Full block composition with `rescue` and `always` |
| `03-missing-reference.yaml` | Negative example: missing task reference (`Ready=False`) |
