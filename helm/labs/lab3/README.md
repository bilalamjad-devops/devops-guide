
Good — this is the **exact step** where you move from “learning Helm” → “thinking like DevOps engineer”.

I’ll keep it **very simple + practical**.

---

# 🧪 Lab 2.1: Dev vs Prod using Helm (Real World)

## 🎯 Goal

👉 Run **same app** in:

* Dev (1 pod)
* Prod (3 pods)

---

## 🧠 Idea (very simple)

Instead of changing one `values.yaml` again and again:

👉 we create:

* `values-dev.yaml`
* `values-prod.yaml`

---

## 🚀 Step 1: Go to Your Chart

```bash
cd my-app
```

---

## 🚀 Step 2: Create Dev File

```bash
vi values-dev.yaml
```

Paste:

```yaml
replicaCount: 1

service:
  type: NodePort
```

---

## 🚀 Step 3: Create Prod File

```bash
vi values-prod.yaml
```

Paste:

```yaml
replicaCount: 3

service:
  type: LoadBalancer
```

---

## 🚀 Step 4: Deploy DEV

```bash
helm install my-app-dev . -f values-dev.yaml
```

Check:

```bash
kubectl get pods
```

👉 You will see **1 pod**

---

## 🚀 Step 5: Deploy PROD

```bash
helm install my-app-prod . -f values-prod.yaml
```

Check:

```bash
kubectl get pods
```

👉 You will see **3 pods**

---

## 🚀 Step 6: Verify Both

```bash
helm list
```

👉 Output:

```
my-app-dev
my-app-prod
```

---

## 🧠 What You Did (IMPORTANT)

* Same code
* Same chart
* Different environments

👉 Only config changed

---

## 🔥 Real Industry Mapping

| Environment | Pods | Service      |
| ----------- | ---- | ------------ |
| Dev         | 1    | NodePort     |
| Prod        | 3    | LoadBalancer |

---

## ⚠️ Important Concept

👉 NEVER do this:

```bash
edit values.yaml again and again ❌
```

👉 ALWAYS do this:

```bash
use separate values files ✅
```

---

## 🚀 Bonus (Very Important Command)

Upgrade DEV:

```bash
helm upgrade my-app-dev . -f values-dev.yaml
```

Upgrade PROD:

```bash
helm upgrade my-app-prod . -f values-prod.yaml
```

---

## 🧹 Cleanup

```bash
helm uninstall my-app-dev
helm uninstall my-app-prod
```

---

## 🧠 Final Understanding

👉 Helm =
“Same app → different configs → different environments”

---

If you understand this, you are now:

✅ Not beginner anymore
✅ Moving into intermediate

---

Next (very powerful, optional):

👉 Helm + CI/CD (Jenkins)
👉 Helm + ArgoCD (GitOps — used in real companies)

Just tell me 👍
