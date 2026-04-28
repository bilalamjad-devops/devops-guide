

# ☸️ Helm: The Kubernetes Package Manager

### 1. What is Helm?
Think of Helm as the **APT** or **YUM** for Kubernetes. 

* **APT** manages software packages (`.deb`) on Linux.
* **Helm** manages application packages (**Charts**) on Kubernetes.

| Action | Linux (APT) | Kubernetes (Helm) |
| :--- | :--- | :--- |
| **Search** | `apt search nginx` | `helm search repo nginx` |
| **Install** | `sudo apt install nginx` | `helm install my-web bitnami/nginx` |
| **Upgrade** | `sudo apt upgrade nginx` | `helm upgrade my-web bitnami/nginx` |
| **Remove** | `sudo apt remove nginx` | `helm uninstall my-web` |

---

### 2. The "Big Question": Why Helm?
You might ask: *"I can already use `kubectl apply -f` to install NGINX. Why do I need Helm?"*

**The Problem with `kubectl`:**
Imagine you have to install **ArgoCD**. It requires 20+ different YAML files (Deployments, RBAC, Services, CRDs). 
* If you use `kubectl`, you have to manage 20 files manually. 
* If you need to change the port or the replica count, you have to find that specific line in 20 files. 
* **Dependencies:** Just like a Linux package needs certain libraries, a K8s app might need a specific database version. Helm handles these "sub-charts" automatically.

**The Helm Solution (Templating):**
Helm allows you to use **Variables**. You write one template, and then you use a `values.yaml` file to inject different settings for `Dev`, `Staging`, and `Production`.



---

### 3. Core Components

#### **A. Helm Charts**
A "Chart" is a bundle of YAML templates. It’s the "Package" itself.

#### **B. Helm Repositories**
A place where charts are stored and shared (like Docker Hub, but for Kubernetes YAMLs).
* **Add Repo:** `helm repo add bitnami https://charts.bitnami.com/bitnami`
* **Update Repo:** `helm repo update`

#### **C. Helm Releases**
A **Release** is a running instance of a Chart. 
* *Example:* You can install the "NGINX Chart" three times in the same cluster. Each one will have a different **Release Name** (e.g., `web-prod`, `web-staging`, `web-test`).

---

### 4. Release Management Commands

| Task | Command |
| :--- | :--- |
| **List Releases** | `helm list` |
| **Check History** | `helm history <release-name>` |
| **Rollback** | `helm rollback <release-name> <revision-number>` |
| **Status** | `helm status <release-name>` |

> **💡 Senior DevOps Tip:** The `rollback` command is the "Magic Button." If you upgrade an app and it crashes, `helm rollback` restores the previous working version in seconds. `kubectl apply` cannot do this easily.

---

### 🧪 Lab: Managing NGINX with Helm

**Prerequisites:**
* A running Kubernetes cluster (Minikube or Kind).
* Helm installed (`helm version`).

#### **Step 1: Setup Repository**
```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

#### **Step 2: Deploy NGINX**
We will install NGINX and name our release `my-nginx`.
```bash
helm install my-nginx bitnami/nginx
```

#### **Step 3: Verify the Deployment**
```bash
# See the Helm release
helm list

# See the actual K8s resources created by Helm
kubectl get pods,svc
```

#### **Step 4: Cleanup**
```bash
helm uninstall my-nginx
```

---

### 📂 How to organize this in your Repo
Since you are organizing your repos, put this under:
`devops-documentation/kubernetes/03-helm-notes.md`

**Would you like to see how a `values.yaml` file works? This is the "secret sauce" that allows you to change a whole deployment by editing just one line.**

Commit Date: 28-April-2026
