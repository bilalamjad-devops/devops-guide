

### 1. `workflow_dispatch` (The Manual Trigger)
* **What it is:** Instead of running every time you `push` code, this workflow only runs when **you** click the "Run workflow" button in the GitHub Actions tab.
* **Why Seniors use it:** In production, you might not want to deploy to AWS every single time you fix a typo in the README. This gives you **control**.

### 2. `defaults: run:` (The "Don't Repeat Yourself" Rule)
* **What it is:** It tells GitHub: "For every step in this job, assume I am working inside the `/frontend` (or `/backend`) folder."
* **DevOps Benefit:** You don't have to write `cd frontend && ...` in every single step. It keeps the code clean.

### 3. `${{ github.run_number }}` (Dynamic Tagging)
* **What it is:** A built-in GitHub variable that counts how many times the workflow has run (e.g., 1, 2, 3...).
* **DevOps Benefit:** Instead of always using `:latest`, this tags your image as `:1`, `:2`, etc. This is called **Immutable Tagging**. If version 5 breaks, you can easily roll back to version 4.

---

### 🚀 The Commented "Senior" Workflow

I have added comments explaining the advanced parts:

```yaml
name: Frontend Build & Push

on:
  workflow_dispatch: # Allows manual triggering from the GitHub UI

jobs:
  build-push:
    runs-on: ubuntu-latest

    # Least privilege principle: only allow the runner to read the code
    permissions:
      contents: read

    # Global setting for this job so we don't have to 'cd' everywhere
    defaults:
      run:
        shell: bash
        working-directory: frontend

    steps:
      - name: Checkout Code
        uses: actions/checkout@v4 # Note: v4 is current standard; v6 is likely a typo/future-proof in your source

      # Connects GitHub to your AWS Account securely
      - name: Configure AWS
        uses: aws-actions/configure-aws-credentials@v4
        with:
          aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
          aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          aws-region: us-east-1

      # Authenticates Docker to talk to AWS ECR (Elastic Container Registry)
      - name: Login to ECR
        uses: aws-actions/amazon-ecr-login@v2

      # This is the "Industry Standard" way to build Docker images in CI/CD
      - name: Build and Push
        uses: docker/build-push-action@v5
        with:
          context: frontend  # The folder where the code is
          file: frontend/Dockerfile # Path to the Dockerfile
          push: true
          # Uses the AWS account ID and run number for a unique image tag
          tags: 615299766984.dkr.ecr.us-east-1.amazonaws.com/dev/frontend:${{ github.run_number }}
          # Injects secrets into the REACT build (like your API URL)
          build-args: |
            REACT_APP_API_BASE_URL=${{ secrets.API_BASE_URL }}
```



---

### 🔍 Differences to Learn:

1.  **ECR vs Docker Hub:** This developer is using **AWS ECR**. In professional jobs, companies usually keep their images inside their cloud provider (AWS/Azure/GCP) rather than public Docker Hub for better security and speed.
2.  **`build-args`**: This is a powerful feature. It allows you to pass variables (like your API URL) into the Docker image **while it is building**. This is how you connect your Frontend to your Backend.
3.  **Permissions**: Adding `permissions: contents: read` is a security "Best Practice." It ensures that if the GitHub runner is hacked, it can't write or delete code in your repo; it can only read it.



Commit Date: 25-April-2026
