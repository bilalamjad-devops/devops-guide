

### 🚀 Production-Ready Multi-Stage Dockerfile (Node.js/React)

```dockerfile
# ==========================================
# STAGE 1: Build Stage (The "Factory")
# ==========================================
# We use 'as build' to create a reference name for this stage.
# 'alpine' versions are used to keep the base image small.
FROM node:23-alpine AS build

# Set the working directory inside the container
WORKDIR /app

# Copy dependency files first. 
# This is a DevOps best practice called "Layer Caching."
# If package.json hasn't changed, Docker skips 'npm install' in the next build.
COPY package*.json ./

# Install dependencies
RUN npm install

# Copy the rest of the application source code
COPY . .

# Build the application (converts code into static files in the /dist folder)
RUN npm run build


# ==========================================
# STAGE 2: Production Stage (The "Store")
# ==========================================
# We move to a tiny Nginx server. 
# We no longer need Node.js or node_modules here!
FROM nginx:stable-alpine

# Remove the default Nginx static files to keep it clean
RUN rm -rf /usr/share/nginx/html/*

# THE MAGIC LINE: 
# We reach back into the 'build' stage and grab ONLY the finished product.
# This keeps our final image size very small (~20MB vs ~900MB).
COPY --from=build /app/dist /usr/share/nginx/html

# Expose port 80 for web traffic
EXPOSE 80

# Start Nginx in the foreground so the container doesn't exit
CMD ["nginx", "-g", "daemon off;"]
```

---

### 📘 Key Concepts to remember for your Labs:

1.  **Layer Caching:** By copying `package.json` and running `npm install` **before** copying the rest of the code, your builds will be much faster. If you only change a line of text in your code, Docker doesn't need to re-download all your dependencies.
    
2.  **`AS build`**: Think of this as a "Save Point" in a video game. You are telling Docker, "Remember everything I did here and call it 'build'."
3.  **`--from=build`**: This is like a "Teleport." You are teleporting the clean files from the first container into the second container.
4.  **Alpine Linux:** Notice we use `node:23-alpine` and `nginx:stable-alpine`. Alpine is a very lightweight Linux distribution (only 5MB). In DevOps, we **always** prefer Alpine to keep images small and secure.
    

### ❓ Question for your GitHub Lab:
In your `labs/lab2/README.md`, you should ask the reader:
> *"What happens to the `node_modules` folder after the build is finished?"*

**The Answer:** It is deleted! It stays in Stage 1, and since Stage 1 is not part of the final image, the `node_modules` never reach the production server. This makes your app much more secure.

**Should we move on to the Python Multi-Stage Dockerfile next? It uses a "Virtual Environment" which is a slightly different concept!**

Commit Date: 25-April-2026
