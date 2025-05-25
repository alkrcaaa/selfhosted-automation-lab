# selfhosted-automation-lab

***⚠️ Project Status: This project is in its early stages and may contain bugs.If you encounter any issues or need help, please open an issue or contact me directly!*** 

selfhosted-automation-lab is a portable HomeLab blueprint showcasing self-hosted applications and full automation with Docker Compose, Kubernetes (k3s), and Ansible. Deploy Gitea, Nextcloud, Home Assistant, Portainer, Uptime Kuma, it-tools, ttydBridge, and Netdata in minutes.

> **A blueprint for your self-hosted homelab:**
> **→ Ansible → k3s Kubernetes**

---

## 🚀 Features

* **Core Apps:** Gitea · Nextcloud · Home Assistant · it-tools
* **Utilities:** Portainer · ttydBridge · Uptime Kuma
* **Observability:** Netdata (DaemonSet)
* **Infra as Code:** Docker Compose · Kustomize · Ansible
* **CI/CD:** GitHub Actions templates (lint, kubeval) *(planned)*
* **Backup:** Restic CronJob *(planned)*
* **Networking:** NodePort now · Ingress + TLS *(planned)*

---

## 📁 Repository Structure

```text
selfhosted-automation-lab/
├── ansible/           # Ansible playbooks and roles (install.yml, uninstall.yml, roles/...)
├── docs/              # Architecture & design documentation
├── k8s/               # Kubernetes manifests (Kustomize)
├── install.yml        # One-shot install playbook (Ansible)
├── uninstall.yml      # Cleanup playbook (Ansible)
├── README.md          # This file
└── .github/           # CI/CD workflows and templates
```

---

## 🔧 Automation with Ansible

We use Ansible to fully automate the bootstrap and deployment process:

| Playbook                                                                        | Purpose                                                |
| ------------------------------------------------------------------------------- | ------------------------------------------------------ |
| `install.yml`                                                                   | Setup OS, install k3s, and deploy Kubernetes workloads |
| `uninstall.yml`                                                                 | Tear down everything provisioned by install.yml        |
| **Detailed docs:** [docs/architecture/ansible.md](docs/architecture/ansible.md) |                                                        |

```bash
# Bootstrap and deploy everything
ansible-playbook install.yml

# Clean up Kubernetes resources
ansible-playbook uninstall.yml
```

---

## ⚙️ k3s Kubernetes Quickstart

1. **Create cluster (k3d example):**

```bash
k3d cluster create lab --config k8s/cluster/k3d-cluster.yaml
```

2. **Deploy manifests:**

```bash
kubectl apply -k k8s/
```

---

## 🔗 Access Your Services

| App                | URL / SSH                                             |
| ------------------ | ----------------------------------------------------- |
| **Gitea**          | `http://localhost:30002`<br>`ssh -p 30222 git@<HOST>` |
| **Nextcloud**      | `http://localhost:30003`                              |
| **Home Assistant** | `http://localhost:30004`                              |
| **it-tools**       | `http://localhost:30005`                              |
| **Uptime Kuma**    | `http://localhost:30006`                              |
| **Portainer**      | `http://localhost:30007` *(to be added)*              |
| **ttydBridge**     | `http://localhost:30008` *(to be added)*              |
| **Netdata**        | `http://localhost:19999` *(to be added)*              |

---

*Enjoy your automated homelab!*
