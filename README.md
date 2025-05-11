# selfhosted-automation-lab
selfhosted-automation-lab A portable HomeLab blueprint showcasing self-hosted applications and automation with Docker Compose, Kubernetes (k3s) and Ansible. Deploy and install Gitea, Nextcloud, Home Assistant, Portainer, Uptime Kuma, it-tools, ttydBridge and Netdata in minutes.



[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#license)  
[![Kubernetes](https://img.shields.io/badge/k3s-Ready-green.svg)](#kubernetes)  
[![Docker Compose](https://img.shields.io/badge/Docker–Compose-Quickstart-blue.svg)](#quickstart)  

> **A blueprint for your self-hosted homelab:**  
> Deploy Gitea, Nextcloud, Home Assistant, it-tools, Uptime Kuma, Portainer, ttydBridge & Netdata  
> from Docker Compose → k3s Kubernetes → (soon) Ansible.

---

## 🚀 Features

- **Core Apps**: Gitea · Nextcloud · Home Assistant · it-tools  
- **Utilities**: Portainer · ttydBridge · Uptime Kuma  
- **Observability**: Netdata (DaemonSet)  
- **Infra as Code**: Docker Compose + kustomize + (coming) Ansible  
- **CI/CD**: GitHub Actions templates (lint, kubeval)  (planned) 
- **Backup**: Restic CronJob (planned)  
- **Networking**: NodePort now, Ingress + TLS in future  (planned)

---

## 📁 Repository Structure

ı will add :)


## k3s Kubernetes

 1. Create a local cluster (k3d example)
```bash
k3d cluster create lab --config k8s/cluster/k3d-cluster.yaml
```

 2. Deploy everything in one go:
```bash
kubectl apply -k k8s/
```

## 🔗 Access Your Services

| App               | URL / SSH                                                 |
|-------------------|-----------------------------------------------------------|
| **Gitea**         | `http://localhost:30002`<br>`ssh -p 30222 git@<HOST>`        |
| **Nextcloud**     | `http://localhost:30003`                                     |
| **Home Assistant**| `http://localhost:30004`                                     |
| **it-tools**      | `http://localhost:30005`                                     |
| **Uptime Kuma**   | `http://localhost:30006`                                     |
| **Portainer**     | `http://localhost:30007` _(to be added)_                     |
| **ttydBridge**    | `http://localhost:30008` _(to be added)_                     |
| **Netdata**       | `http://localhost:19999` _(to be added)_                     |


