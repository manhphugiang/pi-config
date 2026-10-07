# Ansible Configuration for Raspberry Pi Cluster

This folder contains Ansible playbooks and inventory to provision and manage the physical Raspberry Pi nodes.

## Inventory
Configured in `hosts.ini`:
- `master` (`192.168.2.44`) - K3s server control plane
- `worker1` (`192.168.2.11`) - K3s agent node
- `worker2` (`192.168.2.22`) - K3s agent node
- `worker3` (`192.168.2.33`) - Spare node

## Playbooks
1. **`site.yml`**:
   - Base node setup: install packages (`python3-apt`, `iptables`, `curl`), disable swap, configure `/boot/firmware/cmdline.txt` for cgroups.
   - Installs K3s control plane on `master` bound to `eth0`.
   - Joins `worker1` and `worker2` to the K3s cluster.
2. **`ollama.yml`**: Installs Ollama runtime on the nodes.
3. **`pullModel.yml`**: Pulls LLM models into Ollama.

## Usage
Run from inside the `ansible/` directory:
```bash
cd ansible
ansible-playbook site.yml --ask-become-pass
```
