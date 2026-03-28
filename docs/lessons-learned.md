# Lessons Learned

### 1. Separate Editing from Runtime
Using a dedicated VM for editing makes the GitOps workflow much clearer. It prevents treating the cluster as the place where configuration is authored.

### 2. Start with a Simple Demo App
Using a tiny app like `whoami` is enough to prove the model (desired state, sync, self-healing) without adding unnecessary complexity.

### 3. Namespace Isolation
Moving the demo app into its own namespace made the cluster easier to understand, separating system components from workloads.

### 4. Manual Changes Are Not the Truth
Direct changes in Kubernetes are temporary. When Git is authoritative, Argo CD ensures the cluster always returns to the intended state.

### 5. Visualization Matters
Kubernetes is easier to reason about when using **Headlamp** alongside **Argo CD**. It answers: Which pods belong where? Is the app healthy?

### 6. Start Small
A single-node `k3s` cluster is sufficient to learn key concepts like manifests, services, and reconciliation.

### 7. Curate Public Content
A public repo should show architecture and engineering decisions without exposing sensitive data.
* **Include:** Sanitized manifests, diagrams, and documentation.
* **Exclude:** Secrets, kubeconfigs, and private keys.

### 8. Intentional Tooling
`k3s`, `Argo CD`, and `Headlamp` were chosen not for complexity, but to build a coherent, realistic platform for learning.

### 9. GitOps Beyond Deployment
This model improves documentation quality, change discipline, and confidence in rollbacks.

### 10. Document Your Work
Technical work's value increases significantly when turned into a reproducible repository with clean documentation and clear learning outcomes.