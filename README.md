# Awesome Flux2 CRDs repository

This repository contains CRDs from popular operators for Kubernetes installed via Flux2. All CRDs are moved to this repository, since Flux2 cannot install a product and custom resource if the CRD is not yet available.

## Prerequisites

You will need a Kubernetes cluster version 1.21 or newer with installed Flux

## Import current repository

Create GitRepository and Flux Kustomization in you main repository:

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

The Git repository contains the following top directories:

- **crds** dir contains CRDs folder with various installation method depends on product
- **bundles** (optionally) you can create bundles folder with bundle specific set of CRDs for EKS/AKS/etc

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

# NB: All CRDs pointed to latest version available in upstream, use it carefully or clone example and use pinned specific versions.
