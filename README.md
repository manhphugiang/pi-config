# Raspberry Pi Cluster (`pi-cluster`)

A home-lab Raspberry Pi cluster running K3s, AI workloads with Kagent & Ollama, and GitOps with ArgoCD.

---

## 📸 Cluster Setup

![Cluster Photo 1](img/2.jpg)
![Cluster Photo 2](img/3.jpg)

---

## 🗂️ Repository Structure

* **[`ansible/`](ansible/)**: Bare-metal configuration, OS provisioning, network settings, cgroups, and K3s cluster initialization (`master`, `worker1`, `worker2`).
* **[`k8s/`](k8s/)**: Kubernetes manifests, base namespaces, and Kustomize configurations for workloads.
* **[`kagent/`](kagent/)**: [Kagent](https://github.com/kagent-dev/kagent) CNCF Sandbox agentic AI framework quickstart, Helm values, and custom Agent manifests.
* **[`argocd/`](argocd/)**: ArgoCD GitOps application manifests and setup instructions.
* **[`.github/workflows/`](.github/workflows/)**: GitHub Actions CI workflow for linting YAML files and validating Kubernetes manifests.

---

## 🚀 Quick Navigation

1. **Bare-metal / K3s setup**: See [ansible/README.md](ansible/README.md)
2. **Kagent Agentic AI setup**: See [kagent/README.md](kagent/README.md)
3. **ArgoCD GitOps setup**: See [argocd/README.md](argocd/README.md)
4. **Kubernetes manifests**: See [k8s/README.md](k8s/README.md)
