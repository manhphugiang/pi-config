# ArgoCD GitOps Configurations

This directory is reserved for ArgoCD manifests, root applications (App of Apps), and application sets.

## Planned Structure
```text
argocd/
├── install/               # ArgoCD installation manifests / kustomization
├── applications/          # Root ArgoCD Application definitions
│   ├── kagent.yaml        # Deploys kagent via GitOps
│   └── apps.yaml          # Other cluster applications
└── README.md
```

## Quick Installation on K3s
To install ArgoCD manually into the cluster when ready:
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Access the ArgoCD Web UI:
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Initial admin password:
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d; echo
```
