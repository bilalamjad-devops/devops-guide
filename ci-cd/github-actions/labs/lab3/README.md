


### 🚢 Lab 3: The "Production Flow" (Build & Push)
**Goal:** Understand `secrets` and multi-step jobs.
* **Task:** Build your multi-stage Dockerfile and push it to Docker Hub automatically.

```yaml
name: Build-and-Push-Image
on:
  push:
    branches: [ "main" ]

jobs:
  docker-job:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Login to Docker Hub
        uses: docker/login-action@v3
        with:
          username: ${{ secrets.DOCKER_USERNAME }} # Using Secrets!
          password: ${{ secrets.DOCKER_PASSWORD }}

      - name: Build & Push
        run: |
          docker build -t ${{ secrets.DOCKER_USERNAME }}/my-app:latest .
          docker push ${{ secrets.DOCKER_USERNAME }}/my-app:latest
```


Commit Date: 25-April-2026
