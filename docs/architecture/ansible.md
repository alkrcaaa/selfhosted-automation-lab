Homelab Automation with Ansible

This document outlines how we use Ansible to automate and manage our homelab infrastructure in the selfhosted-automation-lab project.

1. Why Ansible?

Single Source of Truth: All infrastructure steps (OS updates, package installs, k3s setup) are defined in YAML playbooks.

Idempotent: Running the same playbook multiple times only applies necessary changes, preventing unintended side effects.

Portability: Easily replicate your environment on a new machine or Raspberry Pi with a single command.

Documentation: Playbooks serve as living documentation—no separate HOWTO guides needed.

2. Directory Structure

selfhosted-automation-lab/
├── ansible/
│   ├── ansible.cfg            # Ansible configuration and defaults
│   ├── inventory.yml          # Defines localhost connection
│   ├── playbooks/
│   │   ├── site.yml           # Bootstrap OS & k3s
│   │   └── k8s-deploy.yml     # Deploy Kubernetes manifests
│   └── roles/
│       ├── common/            # Install base packages (git, curl, etc.)
│       ├── k3s/               # Install and configure k3s cluster
│       ├── k8s-deploy/        # Apply k8s manifests from k8s/ directory
│       └── flux/              # (Optional) GitOps bootstrap with Flux
├── k8s/                       # Kustomize manifest files
├── install.yml                # Top-level playbook to install everything
├── uninstall.yml              # Top-level playbook to clean up Kubernetes resources
└── README.md                  # Project overview and quickstart

3. Key Playbooks

3.1 site.yml

Bootstraps the homelab environment:

Runs the common role to update apt cache and install essential packages.

Runs the k3s role to install a lightweight Kubernetes cluster.

cd ansible
ansible-playbook playbooks/site.yml

3.2 k8s-deploy.yml

Deploys all Kubernetes resources from the k8s/ directory using Kustomize:

cd ansible
ansible-playbook playbooks/k8s-deploy.yml

3.3 install.yml

Single command to set up both the infrastructure and applications:

cd selfhosted-automation-lab
ansible-playbook install.yml

Imports site.yml for OS and cluster setup.

Applies Kustomize manifests in k8s/.

3.4 uninstall.yml

Cleans up all Kubernetes resources (namespaces, pods, deployments, CRDs) without touching OS packages:

cd selfhosted-automation-lab
ansible-playbook uninstall.yml

4. Roles

common: Installs and updates base packages (git, curl, apt-transport-https).

k3s: Uses the official install script to set up k3s and enables the systemd service.

k8s-deploy: Runs kubectl apply -k against the k8s/ directory.

flux: (Optional) Installs Flux CLI and bootstraps GitOps workflows.

5. Usage Workflow

Cleanup (optional):

ansible-playbook uninstall.yml

Setup:

ansible-playbook install.yml

Verify:

sudo KUBECONFIG=/etc/rancher/k3s/k3s.yaml kubectl get nodes
sudo KUBECONFIG=/etc/rancher/k3s/k3s.yaml kubectl get pods --all-namespaces

6. Future Plans

GitOps Integration: Automate manifest sync with Flux or ArgoCD.

Multi-Node k3s: Expand cluster across multiple machines.

Ansible Vault: Secure management of secrets and credentials.

Additional Service Roles: Add roles for Portainer, Gitea, Nextcloud, etc.

End of Ansible Architecture Document