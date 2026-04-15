# AnsibleTask Examples

This directory contains progressive `AnsibleTask` examples for `tasks.krun.io/v1alpha1`.

## Prerequisites

```bash
make install
```

## Apply examples

```bash
kubectl apply -f docs/examples/ansibletask/01-minimal.yaml
kubectl apply -f docs/examples/ansibletask/02-conditions.yaml
kubectl apply -f docs/examples/ansibletask/03-loop-retry.yaml
kubectl apply -f docs/examples/ansibletask/04-notify-checkmode.yaml
```

## Delete examples

```bash
kubectl delete -f docs/examples/ansibletask/
```

## Example Index

| File | Focus |
| --- | --- |
| `01-minimal.yaml` | Minimal task definition with required `action` and basic `args` |
| `02-conditions.yaml` | Task-level conditions with `when`, `changedWhen`, `failedWhen` |
| `03-loop-retry.yaml` | Iteration and retry controls: `loop`, `loopControl`, `until`, `retries`, `delay` |
| `04-notify-checkmode.yaml` | `checkMode`, `notify`, plus common fields (`tags`, `register`, `ignoreErrors`) |
