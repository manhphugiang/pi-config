# Kagent Quickstart & Testing

[Kagent](https://github.com/kagent-dev/kagent) is an open-source, CNCF Sandbox project designed to deploy and orchestrate AI agents natively inside Kubernetes using Custom Resource Definitions (CRDs).

---

## Prerequisites

1. Running Kubernetes cluster (Your K3s cluster on `master`, `worker1`, and `worker2`).
2. `kubectl` configured with cluster access.
3. LLM API Key (OpenAI, Anthropic, or a local provider like Ollama running on your cluster).
4. `helm` v3+ or the `kagent` CLI.

---

## Installation Options

### Method A: Using the `kagent` CLI (Recommended for Development)

1. **Install CLI**:
   ```bash
   # On macOS
   brew install kagent
   # Or via curl
   curl -fsSL https://raw.githubusercontent.com/kagent-dev/kagent/refs/heads/main/scripts/get-kagent | bash
   ```

2. **Deploy into K3s**:
   ```bash
   export OPENAI_API_KEY="sk-..."
   # Demo profile includes sample agents and tools
   kagent install --profile demo
   ```
   *(For a clean installation without sample agents, use `--profile minimal`)*

3. **Open Kagent Dashboard**:
   ```bash
   kagent dashboard
   ```
   This port-forwards the UI to `http://localhost:8082`.

---

### Method B: Using Helm (OCI Registry)

Kagent distributes its Helm charts via OCI in GitHub Container Registry (`ghcr.io`):

1. **Install CRDs**:
   ```bash
   helm install kagent-crds oci://ghcr.io/kagent-dev/kagent/helm/kagent-crds \
     --namespace kagent \
     --create-namespace
   ```

2. **Create Secret for Provider API Key**:
   ```bash
   kubectl create secret generic kagent-api-keys \
     --namespace kagent \
     --from-literal=OPENAI_API_KEY="sk-..."
   ```

3. **Install Kagent Controller & Dashboard**:
   ```bash
   helm install kagent oci://ghcr.io/kagent-dev/kagent/helm/kagent \
     --namespace kagent \
     --values helm/values.yaml
   ```

---

## Directory Structure

```text
kagent/
├── README.md                  # This quickstart guide
├── helm/
│   └── values.yaml            # Custom Helm values for K3s deployment
└── examples/
    ├── secret.yaml.example    # Example credentials secret template
    └── sample-agent.yaml      # Declarative Agent resource definition
```

---

## Testing Declarative Agents

Once CRDs are installed, you can create and manage agents declaratively via `kubectl`:

```bash
kubectl apply -f examples/sample-agent.yaml
kubectl get agents -n kagent
```
