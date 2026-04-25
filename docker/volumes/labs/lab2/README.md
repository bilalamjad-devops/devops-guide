

### Lab 2: Hot-Reloading (Bind Mounts)
**Goal:** See code changes instantly without rebuilding the image.

1.  **Create a simple HTML file on your laptop:**
    ```bash
    echo "<h1>Old Version</h1>" > index.html
    ```
2.  **Run Nginx and "Bind" your local file to the container:**
    *(Use `${PWD}` to represent your current folder path)*
    ```bash
    docker run -d -p 8080:80 -v ${PWD}/index.html:/usr/share/nginx/html/index.html nginx
    ```
3.  **Change the file on your laptop:**
    ```bash
    echo "<h1>New Version Updated!</h1>" > index.html
    ```
4.  **Refresh your browser at `localhost:8080`.**
    *Result: The text updates instantly!*


Commit Date: 25-April-2026
