
Go (Golang) is the **superstar** of multi-stage builds. Because Go compiles into a single, standalone binary file, we can use a special image called `scratch`.

`scratch` is an **empty** image. It has 0MB size. This means your final image will only be the size of your application (usually 10MB to 15MB).

### 🚀 Production-Ready Multi-Stage Dockerfile (Go)

```dockerfile
# ==========================================
# STAGE 1: The Builder (The "Heavy Lifting")
# ==========================================
FROM golang:1.22-alpine AS builder

# Set the working directory
WORKDIR /app

# Copy go.mod and go.sum to download dependencies first (Caching)
COPY go.mod go.sum ./
RUN go mod download

# Copy the source code
COPY . .

# Build the application
# CGO_ENABLED=0 makes the binary "static" (so it doesn't need any Linux libraries)
# GOOS=linux ensures it is built for Linux containers
RUN CGO_ENABLED=0 GOOS=linux go build -o myapp .


# ==========================================
# STAGE 2: The Final Image (The "Empty Box")
# ==========================================
# 'scratch' is the smallest possible image in Docker (0MB)
FROM scratch

# Set working directory
WORKDIR /

# THE MAGIC LINE: 
# Grab only the single binary file from the builder stage
COPY --from=builder /app/myapp .

# Run the binary
ENTRYPOINT ["./myapp"]
```

---

### 🔍 Why Go is different from Node and Python

1.  **No Interpreter needed:** Python needs the `python` engine. Node needs the `node` engine. Go becomes a "Binary," which is like an `.exe` file on Windows. It runs by itself!
2.  **The `scratch` Image:** Since the binary is "Static" (thanks to `CGO_ENABLED=0`), it doesn't even need a Linux OS (like Ubuntu or Alpine) to run.
3.  **Maximum Security:** Because the final image is empty (no shell, no `ls`, no `cd`, no `apt`), a hacker has **nothing** to use if they somehow get inside. It is the most secure way to run an app.



---

### 📘 Comparison for your GitHub Lab

| Language | Final Base Image | Final Image Size (Approx) |
| :--- | :--- | :--- |
| **Node.js** | `nginx:alpine` | ~25 MB |
| **Python** | `python:slim` | ~120 MB |
| **Go** | `scratch` | **~12 MB** |

### 💡 Pro-Tip for your Portfolio
When you write this in your `docker-guide`, explain that **Go is the best choice for Microservices** because the images are so small that they start up in milliseconds. 

**This is the last famous language we covered! You now have React, Python, and Go for your repository. Which part of the repo do you want to work on next? Maybe the "Tag & Push" section?**

Commit Date: 25-April-2026
