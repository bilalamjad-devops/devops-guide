

These are 6 "Boss Commands" you need to master. If you understand these, you can containerize almost any application in the world.

Let's break them down like a professional DevOps engineer.

---

### 1. `FROM` (The Foundation)
Every stage starts with `FROM`. It tells Docker which base image to use.
* **Pro Tip:** Always use specific versions (like `node:23-alpine`) instead of `latest` to keep your builds "idempotent" (meaning they don't change unexpectedly).
* **The `AS` keyword:** This is critical for multi-stage. It gives the stage a name so you can refer to it later.
    > `FROM golang:1.21-alpine AS builder`

### 2. `WORKDIR` (The Home Base)
Think of this as `mkdir` + `cd`. It creates a folder inside the container and moves you into it.
* **Why use it?** If you don't use `WORKDIR`, Docker puts everything in the root directory (`/`), which is messy and can cause security issues.
    > `WORKDIR /app`

### 3. `COPY` (The Bridge)
This moves files from your **Laptop (Host)** into the **Container**.
* **Syntax:** `COPY <source_on_laptop> <destination_in_container>`
* **In Multi-Stage:** This command gets a superpower: `--from`.
    > `COPY --from=builder /app/main .` (This grabs the finished file from the builder stage).

### 4. `RUN` (The Builder)
This executes commands **during the build process**. Use this to install dependencies or compile your code.
* **Common uses:** `npm install`, `pip install`, `go build`, or `apt-get install`.
    > `RUN npm run build`

### 5. `EXPOSE` (The Window)
This is mostly for documentation. It tells the person running the container which port the app listens on (e.g., 80 for Nginx, 3000 for React).
* **Note:** It doesn't actually open the port; you still need to use `-p` when you run the container.
    > `EXPOSE 80`

### 6. `CMD` (The Ignition)
This is the **final command** that runs when the container actually starts.
* **Difference from `RUN`:** `RUN` happens while building the image; `CMD` happens when you start the container.
* **Format:** Always use the "exec" form (square brackets).
    > `CMD ["node", "server.js"]`

---

### 🏗️ Putting it all together: The "Cheat Sheet"

| Command | Purpose | When it happens |
| :--- | :--- | :--- |
| **FROM** | Sets the base OS/Language | Build Time |
| **WORKDIR** | Sets the active directory | Build Time |
| **COPY** | Moves files into the image | Build Time |
| **RUN** | Installs/Compiles things | Build Time |
| **EXPOSE** | Tells us the port | Documentation |
| **CMD** | Starts the application | **Run Time** |

---

### 🎓 Your First "Small Lab" Assignment
To prove you've mastered these, try to create a file named `Dockerfile` in a folder with a simple `index.html` file. Use this structure:

1.  **FROM** `nginx:alpine`
2.  **WORKDIR** `/usr/share/nginx/html`
3.  **COPY** `index.html .`
4.  **EXPOSE** `80`
5.  **CMD** `["nginx", "-g", "daemon off;"]`






Commit Date: 21-April-2026

Commit Date: 25-April-2026
