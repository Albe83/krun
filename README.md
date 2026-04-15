# krun

[![Build](https://img.shields.io/github/actions/workflow/status/Albe83/krun/build.yml?branch=main&style=flat-square)](https://github.com/Albe83/krun/actions/workflows/build.yml)
[![GHCR](https://img.shields.io/badge/ghcr-ghcr.io%2FAlbe83%2Fkrun-blue?style=flat-square&logo=github)](https://github.com/users/Albe83/packages/container/package/krun)
[![License](https://img.shields.io/github/license/Albe83/krun?style=flat-square)](./LICENSE)

Kubernetes operator (Ansible-based) built with `operator-sdk`.

## Contributing

Contribution rules for both humans and AI agents are documented in [`CONTRIBUTING.md`](./CONTRIBUTING.md).

## Current milestone

Current CRDs:

- `AnsibleTask` (`tasks.krun.io/v1alpha1`): semantic definition of a single Ansible task.
  - required: `spec.action`
  - optional: `spec.args`, `when`, `tags`, `become`, `register`, `ignoreErrors`
  - additional controls: `changedWhen`, `failedWhen`, `loop`, `loopControl`, `until`, `retries`, `delay`, `checkMode`, `notify`
- `AnsibleRole` (`roles.krun.io/v1alpha1`): semantic composition of task/block references across role phases.
  - required: `spec.tasks` (`{id, task}` or `{id, block}` items)
  - optional: `spec.preTasks`, `spec.postTasks`, `spec.handlers`
- `AnsibleBlock` (`blocks.krun.io/v1alpha1`): semantic composition of `AnsibleTask` references across block phases.
  - required: `spec.block` (`{id, task}` items)
  - optional: `spec.rescue`, `spec.always`

This milestone models semantics only. It does not execute remote hosts or inventories yet.

## Architecture Decision Records

Key technical decisions are documented as ADRs in [`docs/adr`](./docs/adr/README.md).

## CRD Reference

Detailed references:
- [`docs/crd/ansibletask.md`](./docs/crd/ansibletask.md)
- [`docs/crd/ansiblerole.md`](./docs/crd/ansiblerole.md)
- [`docs/crd/ansibleblock.md`](./docs/crd/ansibleblock.md)

## CI

GitHub Actions build sanity workflow:
- [`build.yml`](./.github/workflows/build.yml)

It validates:
- `kubectl kustomize` rendering for `config/crd`, `config/samples`, and `config/default`
- YAML sanity for `AnsibleTask`, `AnsibleRole`, and `AnsibleBlock` samples/examples
- Docker image build for the operator runtime image

## Artifact

The CI publishes an executable operator image to GHCR:
- image: `ghcr.io/<owner>/krun`
- tags:
  - `sha-<commit>` (immutable)
  - `latest` (updated on `main`)
- publish policy:
  - pull requests: build only (no push)
  - `main`: build + push

## Examples

Progressive `AnsibleTask` examples are available in [`docs/examples/ansibletask`](./docs/examples/ansibletask/README.md).
Progressive `AnsibleRole` examples are available in [`docs/examples/ansiblerole`](./docs/examples/ansiblerole/README.md).
Progressive `AnsibleBlock` examples are available in [`docs/examples/ansibleblock`](./docs/examples/ansibleblock/README.md).
End-to-end composition examples (`task -> block -> role`) are available in [`docs/examples/composition`](./docs/examples/composition/README.md).

## Quickstart

```bash
make install
kubectl apply -f config/samples/tasks_v1alpha1_ansibletask.yaml
kubectl apply -f config/samples/blocks_v1alpha1_ansibleblock.yaml
kubectl apply -f config/samples/roles_v1alpha1_ansiblerole.yaml
```

Run the operator locally:

```bash
make run
```

Inspect resource schema:

```bash
kubectl explain ansibletasks.spec
kubectl explain ansibleblocks.spec
kubectl explain ansibleroles.spec
```
