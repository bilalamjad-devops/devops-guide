# devops-guide
21-April-2026

It is not a trap; it is actually the **smartest way** to learn. Starting with a massive project like a "3-Tier DevSecOps Pipeline on EKS" can be overwhelming because when something breaks, you won't know if it's a Docker issue, a Jenkins issue, or a Kubernetes networking issue.

By doing **Micro-Projects**, you master one "brick" at a time before building the whole house.

### 1. Why "Small" is Better (The Lego Strategy)
If you can't run a simple Python script in a container locally, you shouldn't try to deploy it to a multi-node Kubernetes cluster. Small projects build the **muscle memory** you need.



### 2. The "No-Cost" Roadmap for 2026

* **Linux/Docker:** Use **WSL2** (Windows Subsystem for Linux) or **Killercoda** (Free interactive browser labs).
* **Kubernetes:** Use **Minikube** or **Kind** on your own laptop. It costs $0.
* **CI/CD:** Use **GitHub Actions**. It has a generous free tier for public repositories.
* **Cloud:** Stick to the **AWS Free Tier** or **Oracle Cloud "Always Free"** (which gives you very generous ARM VMs for free).

---

### 3. Recommended Small Projects (Do these in order)

| Project Level | Project Goal | Key Learning |
| :--- | :--- | :--- |
| **Project 1** | **Static Website on Nginx** | Learn Linux, SSH, and Nginx configuration. |
| **Project 2** | **Dockerize a "Hello World" App** | Learn `Dockerfile`, `.dockerignore`, and port mapping. |
| **Project 3** | **GitHub Actions to Docker Hub** | Learn CI/CD basics: secrets, triggers, and automated pushing. |
| **Project 4** | **Docker Compose 2-Tier App** | Learn how a Flask/Node API talks to a Redis/Postgres DB. |
| **Project 5** | **Terraform a Single EC2** | Learn Infrastructure as Code (IaC) without complex networking. |

---

Commit Date: 25-April-2026
