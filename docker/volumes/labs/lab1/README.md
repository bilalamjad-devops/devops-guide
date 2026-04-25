



### Lab 1: The Persistence Test (Named Volumes)
**Goal:** Prove that data survives even after the container is destroyed.

1.  **Create the volume:**
    ```bash
    docker volume create my_database_data
    ```
2.  **Start a container and write a file to the volume:**
    ```bash
    docker run -it --name temp_container -v my_database_data:/app/data alpine sh
    # Inside the container:
    echo "Portfolio Data 2026" > /app/data/save.txt
    exit
    ```
3.  **Delete the container:**
    ```bash
    docker rm temp_container
    ```
4.  **Start a NEW container and read the file:**
    ```bash
    docker run --rm -v my_database_data:/app/data alpine cat /app/data/save.txt
    ```
    *Result: You should see "Portfolio Data 2026".*




Commit Date: 25-April-2026
