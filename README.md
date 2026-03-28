# 🏗️ Homelab GitOps k3s Lab

A hands-on **GitOps** lab built with **k3s**, **Argo CD**, and **Headlamp**. Designed to showcase declarative app deployment, self-healing, namespace isolation, and Kubernetes observability.

---

## 📋 Project Overview
This project documents a controlled Kubernetes environment designed to learn and demonstrate GitOps workflows in a practical and realistic way.

### 🛠️ Tech Stack
| Component | Tool | Function |
| :--- | :--- | :--- |
| **Orchestrator** | k3s | Lightweight Kubernetes distribution. |
| **GitOps** | Argo CD | Reconciliation of desired vs. actual state. |
| **Dashboard** | Headlamp | Cluster visualization and exploration. |
| **Dev Environment** | Workstation VM | Dedicated VM for YAML editing and Git operations. |

---

## 📐 System Architecture

The workflow follows the **Continuous Delivery** standard:

1. **Editing:** Manifests are modified in the dedicated workstation VM.
2. **Push:** Changes are pushed to the GitHub repository.
3. **Detection:** Argo CD identifies repository changes.
4. **Synchronization:** Argo CD automatically reconciles the cluster.
5. **Resilience:** Manual cluster modifications are reverted by the self-healing system.

---

## 🚀 Current Demo Application
The lab currently manages the **whoami** application:
* **Isolation:** Deployed in its own dedicated namespace.
* **Management:** 100% declarative through Git.
* **Automation:** Automatically synchronized by Argo CD.

---

## 📂 Repository Structure

```text
.
├── docs/                   # Detailed documentation
│   ├── architecture.md
│   ├── gitops-flow.md
│   ├── lessons-learned.md
│   └── screenshots/        # Lab screenshots
├── diagrams/               # Infrastructure diagrams
├── kubernetes/             # K8s manifests
│   ├── apps/               # Application definitions
│   │   └── whoami/
│   │       ├── namespace.yaml
│   │       ├── deployment.yaml
│   │       ├── service.yaml
│   │       └── kustomization.yaml
│   └── argocd/             # Argo CD App configurations
│       └── whoami-app.yaml
└── README.md
```
---

### Block 3: Features, Workflow, Security, and Roadmap

```markdown
---

## ✨ Demonstrated Features
* ✅ Declarative Kubernetes deployments.
* ✅ Namespace isolation.
* ✅ Automated sync with Argo CD.
* ✅ **Self-healing:** Automatic recovery from configuration drift.
* ✅ Strict separation between **Source of Truth** (Git) and **Runtime** (Cluster).
* ✅ Basic observability via the Headlamp dashboard.

---

## 🔄 Typical Workflow
1. **Update** a manifest in Git.
2. **Push** changes to the repository.
3. **Watch** Argo CD update the cluster instantly.
4. **Simulate failure:** Manually change a resource in K8s (via CLI).
5. **Verify** how Argo CD automatically restores the desired state.

---

## 🔒 Security Notes
> **Note:** This is a public repository containing only sanitized manifests and documentation.

**Does NOT include:**
* Real secrets (Seals/Vaults).
* `kubeconfig` files.
* Private SSH keys.
* Operational credentials or sensitive internal topologies.

---

## 🛠️ Next Steps (Roadmap)
* [ ] Expose applications via **Ingress**.
* [ ] Publish Argo CD and Headlamp with internal hostnames.
* [ ] Add more complex example applications.
* [ ] Document architecture with visual diagrams.
* [ ] Expand GitOps workflow with multiple environments and namespaces.