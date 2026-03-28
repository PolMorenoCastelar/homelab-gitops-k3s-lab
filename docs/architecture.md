# Architecture

## Goal
This lab was designed to build a small but realistic **GitOps workflow** on top of Kubernetes. 

The setup enforces a strict separation between:
- **Manifest authoring** (Development)
- **Git** (Source of Truth)
- **Cluster Runtime** (Production-like environment)
- **Visualization and Troubleshooting** (Observability)

---

## Main Components

### 1. Editing Workstation VM
A dedicated VM used to:
* Edit Kubernetes YAML manifests.
* Manage Git repositories.
* Document changes.
* Prepare application definitions for Argo CD.
* *Note: This VM is intentionally isolated from the Kubernetes runtime.*

### 2. Git Repository
GitHub acts as the **Source of Truth** for:
* Kubernetes application manifests.
* Argo CD application definitions.
* Lab documentation.
* Sanitized examples of deployed workloads.

### 3. k3s Cluster VM
A dedicated VM running a single-node Kubernetes lab using **k3s**. This node hosts:
* System components required by k3s.
* Argo CD and Headlamp.
* Demo workloads (e.g., `whoami`).

### 4. Argo CD
Argo CD is responsible for:
* Reading the Git repository.
* Detecting configuration changes.
* Synchronizing the cluster with the repository state.
* Reverting manual drift through **self-healing**.

### 5. Headlamp
Headlamp provides a visual interface for monitoring:
* Namespaces, Pods, and Deployments.
* Services and networking.
* Cluster exploration and troubleshooting.

---

## High-level Flow

```text
Editing VM
   │
   │ edit YAML / commit / push
   ▼
GitHub Repository
   │
   │ watched by Argo CD
   ▼
Argo CD
   │
   │ reconciles desired state
   ▼
k3s Cluster
   │
   ├── System Components
   ├── Argo CD
   ├── Headlamp
   └── Demo Applications
```

### Block 3: Namespaces and Design Decisions

## Current Namespaces
The cluster currently includes the following relevant namespaces:

| Namespace | Content |
| :--- | :--- |
| **kube-system** | CoreDNS, Traefik, metrics-server, local-path-provisioner. |
| **argocd** | Server, repo-server, application-controller, dex, redis. |
| **headlamp** | Headlamp UI deployment and service. |
| **whoami** | Demo application deployed through GitOps. |
| **default** | Standard Kubernetes default resources. |

---

## Design Decisions

### Why k3s?
Selected for being lightweight, simple to install, and perfectly suited for a homelab learning environment.

### Why Argo CD?
Chosen to demonstrate:
* Automated synchronization.
* Reconciliation against Git.
* **Self-healing** capabilities.
* Declarative application delivery.

### Why Headlamp?
Selected as a modern, extensible web UI for Kubernetes visualization and daily cluster inspection.

### Why separate editing from runtime?
This reinforces the **GitOps model**:
1. Edit in one place (Workstation).
2. Push to Git.
3. Reconciliation happens automatically in the cluster.

---

## Demo Workload
The repository includes a demo application called **whoami** to validate:
* Deployment in its own namespace.
* Basic Kubernetes manifest structure.
* Argo CD application management.
* Sync and self-heal validation.