# Awesome Flux2 CRDs repository

This repository contains CRDs from popular operators for Kubernetes installed via Flux2. All CRDs are moved to this repository because Flux2 cannot install a product and custom resource if the CRD is not yet available.

## Support Project
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/N4N011QV6F)

## Prerequisites

- Kubernetes cluster version 1.24 or newer
- Flux version 2.3.0 or newer bootstrapped to the [Head repository (example)](https://github.com/brainfair/awesome-flux-head)

## Import current repository

Create a GitRepository and a Flux Kustomization in your main repository.

```yaml
---
apiVersion: source.toolkit.fluxcd.io/v1
kind: GitRepository
metadata:
  name: fluxcd-gitops-crds
  namespace: flux-system
spec:
  interval: 10m
  ref:
    branch: main
  secretRef:
    name: flux-system
  url: https://github.com/brainfair/awesome-flux-crds.git
  ignore: |
    # exclude README.md
    /README.md
---
apiVersion: kustomize.toolkit.fluxcd.io/v1
kind: Kustomization
metadata:
  name: fluxcd-gitops-crds
  namespace: flux-system
spec:
  interval: 10m
  path: ./
  prune: true
  sourceRef:
    kind: GitRepository
    name: fluxcd-gitops-crds
```

[Check head repository example](https://github.com/brainfair/awesome-flux-head/blob/main/clusters/homelab/00-crds.yaml)

## Repository structure

The Git repository contains the following top-level directories:

- **crds** Contains the CRDs folder with various installation methods, depending on the product.
- **bundles** (optionally) You can create a bundles folder with a specific set of CRDs for EKS, AKS, etc.

```
├── crds
│   ├── cert-manager
│   ├── istio
│   ├── Prometheus
|   ├── ...
│   └── VictoriaMetrics
└── bundles
    ├── eks
    └── aks
```

## CRDs list

The next CRDs available in the example are:

* cert-manager
* cloudnative-pg
* elastic-eck
* external-secrets
* istio
* k8ssandra-operator
* metallb
* Prometheus
* strimzi
* VictoriaMetrics

# NB: All CRDs point to the latest version available upstream. Use them carefully, or clone the example and use a pinned, specific version.
