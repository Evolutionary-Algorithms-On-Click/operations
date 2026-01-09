# 🤖 Automated Deployment with Ansible

This directory contains the automation logic to provision target servers from scratch, configure a multi-node Kubernetes cluster, and deploy all EvOC infrastructure components.

## 🛠 Prerequisites

- **Ansible 2.10+** installed locally.
- **Ubuntu 22.04 / 24.04** on target servers (Recommended).
- **SSH access** with sudo privileges on all nodes.

---

## ⚙️ Configuration

### 1. Inventory Setup
Edit `inventory.ini` to define your cluster topology.

```ini
[nodes]
master-node  ansible_host=1.2.3.4
worker-node1 ansible_host=1.2.3.5
worker-node2 ansible_host=1.2.3.6

[master]
master-node

[workers]
worker-node1
worker-node2

[all:vars]
ansible_user=ubuntu
```

### 2. Variable Configuration
Create the following secret files in `ansible/vars/` (these are ignored by Git):

#### `ansible/vars/crdb_secrets.yml`
```yaml
crdb_enterprise_license_key: "YOUR_LICENSE_KEY_HERE"
```

#### `ansible/vars/minio_secrets.yml`
```yaml
minio_root_user: "admin"
minio_root_password: "a-very-secure-password"
```

---

## 🚀 Execution

Run the deployment from the root or `ansible` directory:

```bash
ansible-playbook -i inventory.ini playbook.yaml -kK
```

### What This Playbook Does:
1.  **System Preparation**: Disables swap, configures kernel modules (`overlay`, `br_netfilter`), and sets sysctl parameters.
2.  **Container Runtime**: Installs Docker and the `cri-dockerd` (v0.3.21) bridge to enable Kubernetes-Docker compatibility.
3.  **Kubernetes Stack**: Installs `kubeadm`, `kubelet`, and `kubectl` (v1.31).
4.  **Cluster Lifecycle**:
    - Initializes the Master node.
    - Generates and shares join tokens dynamically with Workers.
    - Installs **Flannel CNI** for cross-node networking.
5.  **Infrastructure**: Provisions **CockroachDB** (Multi-node), **MinIO**, and **RabbitMQ**.
6.  **Application**: Automatically copies and applies all manifests from the `/kubernetes` directory.

---

## 🧩 Advanced Features

### 🔌 CRI-Dockerd Integration
As Kubernetes has deprecated direct Docker support, this playbook integrates **`cri-dockerd`**. This shim allows you to continue using the Docker Engine as the container runtime while maintaining full compatibility with the Kubernetes CRI.

### 💻 Multi-Architecture Support
The playbook automatically detects the processor architecture of your nodes. Whether you are running on **x86_64 (Intel/AMD)** or **aarch64 (ARM/Apple Silicon)**, the correct binaries (Docker, CRDB, MinIO) will be downloaded and installed.

---

## 🔍 Troubleshooting

- **CRI Socket**: If `kubelet` fails to start, verify the socket exists: `ls /var/run/cri-dockerd.sock`.
- **Node Status**: Check cluster health: `kubectl get nodes`.
- **Logs**: View service logs on nodes: `journalctl -u cri-docker`.
