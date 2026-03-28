# GitOps Flow

## Objective
The purpose of this lab is to validate a basic GitOps workflow end-to-end. 

The desired model is:
1. **Define state in Git.**
2. **Let Argo CD reconcile the cluster.**
3. **Avoid manual configuration drift.**
4. **Keep deployed resources aligned with the repository.**

---

## Workflow

### Step 1: Edit Manifests
Kubernetes manifests are edited on a dedicated workstation VM. Typical changes include:
* Changing replica count.
* Moving an app to a new namespace.
* Adding a Service or updating a container image.
* Adding a new application definition.

### Step 2: Commit and Push
Changes are committed and pushed to GitHub.
Example:
```bash
git add .
git commit -m "Scale whoami to 2 replicas"
git push
```
### Block 2: Sync, Self-Healing, and Benefits
```markdown
### Step 4: Automatic Synchronization
Since the application uses automated sync, Argo CD applies changes automatically. The current demo uses:
* `automated`
* `prune: true`
* `selfHeal: true`

### Step 5: Workload Updated in Cluster
Once synchronized, the cluster reflects the desired configuration:
* Deployments are scaled.
* Services are created or removed.
* Namespaces are populated.
* Outdated resources are pruned.

---

## Self-Healing Behavior
A key validation in this lab is **Self-healing**:
1. `whoami` is defined in Git with `replicas: 2`.
2. Someone manually changes it in Kubernetes to `replicas: 1`.
3. Argo CD detects the drift.
4. Argo CD automatically restores `replicas: 2`.

**Prune behavior:** Ensures that resources removed from Git are also deleted from the cluster, avoiding "configuration leftovers."

---

## Benefits of this Model
* **Reproducibility & Traceability.**
* **Cleaner change history.**
* **Lower risk of manual drift.**
* **Easier troubleshooting and better documentation.**