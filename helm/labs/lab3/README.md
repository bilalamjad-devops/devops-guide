Perfect — this is where your profile becomes **job-ready**.

Lab 3 is not just learning — this is **what real companies do**.

---

# 🧪 Lab 3: Deploy Helm Chart using CI/CD (GitHub Actions)

## 🎯 Objective

* Automate Helm deployment
* Use CI/CD pipeline
* Deploy app to Kubernetes automatically

👉 This is **real DevOps workflow**

---

## 🧠 What You Will Learn

* CI/CD with GitHub Actions
* Automating Helm deployments
* Real production flow
* Git → Pipeline → Kubernetes

---

## 📋 Prerequisites

* Kubernetes cluster (Minikube / EKS / Kind)
* Helm installed
* GitHub repo
* kubectl working locally

---

## 🏗️ Architecture

```
GitHub Push → GitHub Actions → Helm → Kubernetes
```

---

## 🚀 Step 1: Push Your Helm Chart to GitHub

Your repo structure:

```
repo/
  my-app/
    Chart.yaml
    values.yaml
    templates/
```

Push it:

```bash
git add .
git commit -m "added helm chart"
git push
```

---

## 🚀 Step 2: Create GitHub Actions Workflow

Create file:

```
.github/workflows/deploy.yml
```

---

## 🚀 Step 3: Add Pipeline Code

```yaml
name: Deploy Helm App

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout Code
        uses: actions/checkout@v3

      - name: Setup Kubectl
        uses: azure/setup-kubectl@v3

      - name: Setup Helm
        uses: azure/setup-helm@v3

      - name: Configure Kubeconfig
        run: |
          mkdir -p $HOME/.kube
          echo "${{ secrets.KUBECONFIG }}" > $HOME/.kube/config

      - name: Deploy using Helm
        run: |
          helm upgrade --install my-app ./my-app
```

---

## 🔐 Step 4: Add GitHub Secret

Go to:

👉 GitHub → Settings → Secrets → Actions

Add:

```
Name: KUBECONFIG
Value: (paste your kubeconfig file content)
```

Get kubeconfig:

```bash
cat ~/.kube/config
```

---

## 🚀 Step 5: Trigger Pipeline

Now push any change:

```bash
git commit -m "trigger deploy"
git push
```

---

## ✅ Expected Output

* GitHub Actions runs pipeline
* Helm deploys app automatically
* Kubernetes gets updated

Check:

```bash
kubectl get pods
kubectl get svc
```

---

## 🧠 Real Industry Flow

In companies:

```
Developer → Git Push  
        ↓
CI Pipeline (test + scan)
        ↓
CD Pipeline (Helm deploy)
        ↓
Kubernetes Cluster
```

---

## 🔥 Bonus (VERY IMPORTANT)

Instead of plain deploy:

```bash
helm upgrade --install my-app ./my-app -f values-prod.yaml
```

👉 Different environments

---

## ⚠️ Common Mistakes

* Not storing kubeconfig in secrets
* Hardcoding values
* Not using Helm upgrade (using install again)
* No rollback strategy

---

## 🔐 Best Practice

Always use:

```bash
helm upgrade --install
```

👉 Safe deployment (create or update)

---

## 🧹 Cleanup

```bash
helm uninstall my-app
```

---

## 🔚 What You Achieved

Now you can:

* Automate deployments
* Use Helm in CI/CD
* Work like real DevOps engineer

---

