Perfect — now you’re entering **real industry level (GitOps)**.
I’ll keep it **simple + clear + no confusion**.

---

# 🧪 Lab 4: Helm + ArgoCD (GitOps — Real Industry)

## 🎯 Goal

👉 Automatically deploy app using **Git only**

No manual:

* ❌ `kubectl apply`
* ❌ `helm install`

Only:
👉 **Git push → deployment happens**

---

## 🧠 Idea (Very Simple)

Earlier:

```
You → run helm command → deploy
```

Now (GitOps):

```
You → push code → ArgoCD deploys automatically
```

---

## 🏗️ Architecture

```
GitHub Repo → ArgoCD → Kubernetes
```

---

## 📋 Prerequisites

* Kubernetes cluster (Minikube / EKS)
* Helm chart ready (`my-app`)
* ArgoCD installed

---

## 🚀 Step 1: Install ArgoCD

```bash
kubectl create namespace argocd
```

```bash
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

Wait:

```bash
kubectl get pods -n argocd
```

---

## 🚀 Step 2: Access ArgoCD UI

Port forward:

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

Open:

```
https://localhost:8080
```

---

### Get Password

```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

Login:

* Username: `admin`
* Password: (above command output)

---

## 🚀 Step 3: Push Helm Chart to GitHub

Structure:

```
repo/
  my-app/
    Chart.yaml
    values.yaml
    templates/
```

Push:

```bash
git add .
git commit -m "helm chart"
git push
```

---

## 🚀 Step 4: Create ArgoCD Application

👉 In UI:

1. Click **New App**
2. Fill:

* Application Name: `my-app`
* Project: `default`

---

### Source (IMPORTANT)

* Repo URL: your GitHub repo
* Path: `my-app`
* Revision: `main`

---

### Destination

* Cluster: `https://kubernetes.default.svc`
* Namespace: `default`

---

### Sync Policy

👉 Select:

✅ **Automatic**

---

Click **Create**

---

## 🚀 Step 5: Deploy Automatically

👉 ArgoCD will:

* Read your Helm chart
* Deploy to Kubernetes

Check:

```bash
kubectl get pods
```

---

## 🚀 Step 6: Make Change (Magic Part)

Edit:

```bash
vi values.yaml
```

Change:

```yaml
replicaCount: 1 → 3
```

Push:

```bash
git commit -am "scale app"
git push
```

---

## ✅ Result

👉 WITHOUT running anything:

* ArgoCD detects change
* Automatically deploys
* Pods increase

Check:

```bash
kubectl get pods
```

---

## 🧠 What Just Happened

👉 This is **GitOps**

* Git = source of truth
* ArgoCD = deploy engine

---

## 🔥 Real Industry Flow

```
Developer → Git Push
          ↓
ArgoCD detects change
          ↓
Auto deploy to Kubernetes
```

---

## ⚠️ Important Rules

* Never deploy manually
* Always push to Git
* Git is your “control panel”

---

## 🔐 Best Practices

* Use separate values files:

```
values-dev.yaml
values-prod.yaml
```

* Use separate ArgoCD apps for:

  * dev
  * staging
  * prod

---

## 🧹 Cleanup

```bash
kubectl delete ns argocd
helm uninstall my-app
```

---

## 🔚 What You Achieved

Now you can:

✅ Use GitOps
✅ Automate deployments
✅ Work like real DevOps engineer
✅ Use ArgoCD + Helm together

---

## 🧠 Final Simple Understanding

👉 CI/CD way:

```
Pipeline → deploy
```

👉 GitOps way:

```
Git → deploy
```

---

If you want next (very powerful):

👉 ArgoCD + EKS + LoadBalancer + Domain (full production setup)

That will make your profile **very strong for jobs**.
