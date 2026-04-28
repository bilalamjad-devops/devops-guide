Got it — you don’t need more theory, you need **clear + simple + step-by-step**.

I’ll simplify Lab 2 so it feels like **doing, not thinking**.

---

# 🧪 Lab 2 (Simple Version): Change App using Helm

## 🎯 Goal (in one line)

👉 Change number of pods using Helm (like real DevOps)

---

## 🚀 Step 1: Create Chart

```bash
helm create my-app
cd my-app
```

👉 Done. Don’t overthink structure.

---

## 🚀 Step 2: Run First Time

```bash
helm install my-app .
```

Check:

```bash
kubectl get pods
```

👉 You will see **1 pod running**

---

## 🚀 Step 3: Change Pods (IMPORTANT)

Open file:

```bash
vi values.yaml
```

Find:

```yaml
replicaCount: 1
```

Change to:

```yaml
replicaCount: 3
```

Save file.

---

## 🚀 Step 4: Apply Change

```bash
helm upgrade my-app .
```

Now check:

```bash
kubectl get pods
```

👉 You will see **3 pods**

✅ This is the **main concept of Helm**

---

## 🚀 Step 5: Change Service Type

In `values.yaml`:

```yaml
service:
  type: ClusterIP
```

Change to:

```yaml
service:
  type: NodePort
```

Apply again:

```bash
helm upgrade my-app .
```

Check:

```bash
kubectl get svc
```

---

## 🚀 Step 6: Break + Fix (Rollback)

Now break something (for learning):

```bash
helm upgrade my-app wrong-folder/
```

(It will fail)

Now rollback:

```bash
helm history my-app
helm rollback my-app 1
```

👉 Back to working state

---

## 🧠 What Just Happened (Simple)

* You did NOT edit YAML manually
* You only changed `values.yaml`
* Helm updated everything

👉 This is why companies use Helm

---

## 🔥 Real Meaning (Very Important)

Without Helm:

* Edit 10 YAML files 😓

With Helm:

* Change 1 value 😎

---

## 🧹 Cleanup

```bash
helm uninstall my-app
```

---

## 🧠 One Line Summary

👉 Helm = “Change config → Run upgrade → Done”

---

If you want, next I can make it even more real:

👉 Lab 2.1 (very powerful):

* Create `values-dev.yaml` and `values-prod.yaml`
* Run same app in **2 environments**

This is where you start thinking like **intermediate DevOps engineer**.
