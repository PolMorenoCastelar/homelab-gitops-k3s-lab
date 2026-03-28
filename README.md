# Homelab GitOps k3s Lab

A hands-on homelab GitOps lab built with **k3s**, **Argo CD**, and **Headlamp**, showcasing declarative app deployment, self-healing, namespace isolation, and Kubernetes observability.

## Overview

This project documents a small Kubernetes lab designed to learn and demonstrate GitOps workflows in a practical way.

The setup is based on:
- **k3s**: Lightweight Kubernetes distribution.
- **Argo CD**: GitOps reconciliation tool.
- **Headlamp**: Kubernetes visualization and cluster exploration.
- **Dedicated Workstation**: A separate VM used for Git/YAML editing.

## Architecture

High-level flow:
1. Kubernetes manifests are edited in a dedicated workstation VM.
2. Changes are committed and pushed to GitHub.
3. Argo CD detects repository changes.
4. Argo CD reconciles the Kubernetes cluster automatically.
5. Manual drift in the cluster is reverted through self-healing.

> See more details in: [`docs/architecture.md`](docs/architecture.md) | [`docs/gitops-flow.md`](docs/gitops-flow.md)

## Repository Structure

```text
.
├── docs/               # Documentation & Screenshots
├── diagrams/           # Architecture diagrams
├── kubernetes/
│   ├── apps/           # Application manifests (whoami)
│   └── argocd/         # Argo CD Application definitions
├── .gitignore
└── README.md

```
### 3. Características y Demo

## Features Demonstrated

* **Declarative Deployments**: All infrastructure state is defined in code.
* **Namespace Isolation**: Applications are segmented for security and order.
* **Argo CD Automated Sync**: Real-time synchronization between Git and the cluster.
* **Self-healing**: Automatic restoration if manual changes occur in the cluster.
* **Observability**: Clean UI for cluster exploration via Headlamp.

## Demo Workflow

1. Update a manifest in Git.
2. Push changes to the repository.
3. Watch **Argo CD** sync the cluster automatically.
4. Manually change a resource in Kubernetes (e.g., scale a deployment).
5. Watch Argo CD restore the **desired state**.

## Screenshots

### Argo CD Dashboard
*Shows the GitOps application in a healthy and synchronized state.*
![Argo CD App](docs/screenshots/argocd-app.png)

### Resource Tree
*Relationship between Argo CD and the managed Kubernetes resources.*
![Resource Tree](docs/screenshots/resource-tree.png)

### Headlamp View
*Observability of namespaces and the `whoami` application.*
![Headlamp](docs/screenshots/headlamp-view.png)

---

## Security Note
This public repository contains only **sanitized manifests**. It does **not** include:
- Real secrets or operational credentials.
- Private SSH keys or kubeconfig files.
- Sensitive internal topology details.

## Next Steps
- [ ] Expose applications through Ingress.
- [ ] Setup internal hostnames for Argo CD and Headlamp.
- [ ] Add more example applications (e.g., Nginx, Redis).