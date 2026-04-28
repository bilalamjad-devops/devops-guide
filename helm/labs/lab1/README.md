
## 🧪 Lab: Deploy NGINX using Helm

### 🎯 Objective

Deploy and manage NGINX using Helm.

---

### 📋 Prerequisites

* Kubernetes cluster (Minikube / Kind / EKS)
* Helm installed
* kubectl configured

---

### 🚀 Step 1: Add Repository

```bash
helm repo add bitnami https://charts.bitnami.com/bitnami
helm repo update
```

---

### 🚀 Step 2: Install NGINX

```bash
helm install my-nginx bitnami/nginx
```

---

### 🚀 Step 3: Verify

```bash
helm list
kubectl get pods
kubectl get svc
```

---

### 🚀 Step 4: Access Application

```bash
kubectl port-forward svc/my-nginx 8080:80
```

Open browser:

```
http://localhost:8080
```

---

### 🚀 Step 5: Uninstall

```bash
helm uninstall my-nginx
```
Commit Date: 28-April-2026
