# Overview Diagram
```text
gitops-vm
  ├─ VS Code / code-server
  ├─ YAML authoring
  └─ Git push
        │
        ▼
GitHub repository
        │
        ▼
Argo CD on k3s-lab
  ├─ monitors repo
  ├─ syncs manifests
  └─ self-heals drift
        │
        ▼
k3s cluster
  ├─ kube-system
  ├─ argocd
  ├─ headlamp
  └─ whoami
´´´

