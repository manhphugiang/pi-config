# Kubernetes Manifests

This directory contains declarative Kubernetes manifests deployed across the cluster.

## Structure
```text
k8s/
├── base/
│   ├── namespaces.yaml        # Standard cluster namespaces
│   └── kustomization.yaml
└── README.md
```

## Quick Apply
```bash
kubectl apply -k k8s/base/
```
