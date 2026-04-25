Since you are a DevOps student, learning **GitHub Actions** is like learning how to give your code a "brain." Instead of you manually building and pushing Docker images, GitHub Actions does it for you every time you push code.

In GitHub Actions, we don't just use "commands"—we use **Keywords** in a YAML file (located at `.github/workflows/main.yml`).

---

### 1. The Core Keywords (The "Grammar")

Think of a workflow like a **Recipe**:

| Keyword | What it is | Real-world Example |
| :--- | :--- | :--- |
| **`name`** | The title | "Build and Push Docker Image" |
| **`on`** | The trigger (The "When") | `push` or `pull_request` |
| **`jobs`** | The big tasks | "Build-App", "Deploy-App" |
| **`runs-on`** | The server type | `ubuntu-latest` |
| **`steps`** | The small actions | 1. Checkout code, 2. Login, 3. Build |
| **`uses`** | A pre-made tool | `actions/checkout@v4` (Someone else wrote this for you) |
| **`run`** | Your custom command | `docker build -t my-app .` |

---

### 2. A Professional Docker Workflow (The Lab)

Here is a script you can put in your `03-registry-ops` or `05-ci-cd` folder. This script automatically builds your **Multi-stage Dockerfile** and pushes it to Docker Hub.

```yaml
name: Docker Build and Push

# 1. When should this run?
on:
  push:
    branches: [ "main" ]  # Runs every time you push to the 'main' branch

jobs:
  build-and-push:
    # 2. What kind of machine do we need?
    runs-on: ubuntu-latest

    steps:
      # 3. Pull the code from GitHub onto the Ubuntu runner
      - name: Checkout Code
        uses: actions/checkout@v4

      # 4. Login to Docker Hub (Uses Secrets for safety!)
      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }}
          password: ${{ secrets.DOCKER_PASSWORD }}

      # 5. Build the image and Push it
      - name: Build and Push
        run: |
          docker build -t ${{ secrets.DOCKER_USERNAME }}/my-app:latest .
          docker push ${{ secrets.DOCKER_USERNAME }}/my-app:latest
```



---

### 3. The "Secret" Command: `${{ secrets.X }}`

In DevOps, we **NEVER** write passwords or usernames directly in the code. 
* **The Trap:** If you write your Docker password in the YAML file, everyone on GitHub can see it.
* **The Fix:** You go to **GitHub Repo > Settings > Secrets and Variables > Actions** and add your credentials there. GitHub Actions then "injects" them safely using the `${{ secrets.NAME }}` syntax.

---

### 4. Why this is "DevOps Mastery"

When you add this to your GitHub repo, you aren't just a "Docker guy" anymore. You are an **Automation Engineer**. 

* **Without Actions:** You: Build -> Tag -> Push (3 manual steps).
* **With Actions:** You: `git push` (1 step). The server does the rest.



### 💡 Pro-Tip for your GitHub Lab
In your `labs/lab_github_actions.md`, explain that `ubuntu-latest` is actually a **temporary VM** that GitHub gives you for free. Once the job is done, the VM is destroyed. This is called **Ephemeral Infrastructure**.

**Does this YAML structure make sense to you? Would you like to try a lab where we add a "Trivy Scan" command inside GitHub Actions to check for security before we push?**

Commit Date: 21-April-2026

Commit Date: 25-April-2026
