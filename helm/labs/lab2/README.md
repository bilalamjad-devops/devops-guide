Good — this is where your level actually starts moving from **beginner → intermediate**.

Lab 1 was just “install nginx”.
👉 Lab 2 = **REAL DevOps skill (what companies expect)**

---

# 🧪 Lab 2: Create and Customize Your Own Helm Chart

## 🎯 Objective

* Create your own Helm chart
* Use `values.yaml`
* Deploy same app with different configs (dev / prod mindset)

---

## 🧠 What You Will Learn

* How Helm charts are structured
* How templating works
* How to avoid hardcoding values
* How real teams manage environments

---

## 📋 Prerequisites

* Kubernetes cluster (Minikube / Kind / EKS)
* Helm installed
* kubectl configured

---

## 🚀 Step 1: Create Helm Chart

```bash
helm create my-app
cd my-app
```

This creates structure like:

```
my-app/
  Chart.yaml
  values.yaml
  templates/
    deployment.yaml
    service.yaml
```

---

## 🚀 Step 2: Understand Important Files

### values.yaml

This is where you define variables:

```yaml
replicaCount: 1

image:
  repository: nginx
  tag: latest

service:
  type: ClusterIP
  port: 80
```

---

### templates/deployment.yaml

You will see something like:

```yaml
replicas: {{ .Values.replicaCount }}
```

👉 This means:
Helm will replace value from `values.yaml`

---

## 🚀 Step 3: Deploy Chart

```bash
helm install my-release ./my-app
```

Verify:

```bash
helm list
kubectl get pods
```

---

## 🚀 Step 4: Change Configuration (VERY IMPORTANT)

Now simulate **production change**

Edit `values.yaml`:

```yaml
replicaCount: 3

service:
  type: LoadBalancer
```

---

## 🚀 Step 5: Upgrade Release

```bash
helm upgrade my-release ./my-app
```

Check:

```bash
kubectl get pods
kubectl get svc
```

👉 You will see:

* Pods increased (scaling)
* Service type changed

---

## 🚀 Step 6: Rollback (REAL INDUSTRY SCENARIO)

If something breaks:

```bash
helm history my-release
```

Rollback:

```bash
helm rollback my-release 1
```

---

## 🧠 Real-World Use Case

In companies:

* `values-dev.yaml`
* `values-staging.yaml`
* `values-prod.yaml`

Example:

```bash
helm install my-app -f values-dev.yaml
helm install my-app -f values-prod.yaml
```

👉 Same chart, different environments

---

## 🔐 Best Practices

* Never hardcode values in YAML
* Always use `values.yaml`
* Use separate files for environments
* Use Helm rollback in CI/CD pipelines

---

## 🧹 Cleanup

```bash
helm uninstall my-release
```

---

## 🔚 What You Achieved

After this lab, you can:

* Create Helm charts
* Customize deployments
* Handle real production changes
* Rollback safely

---

