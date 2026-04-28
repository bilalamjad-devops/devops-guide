
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



Commit Date: 28-April-2026
