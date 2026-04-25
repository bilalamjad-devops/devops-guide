

### Lab: Bind Mounts:

In this lab, we create:
- directory `mkdir`
- `run` container and `bind` directory
- `exec` container
- create file
- see changes in host machine's `directory`


*Make a directory*
```bash
mkdir testingmount
```


*create container and mount a directory*
```bash
docker run -it -d -p 80:80 -v /home/devopsmolvi/testtingmount:/opt --name container1 nginx:latest
```

`sourcedirectory:destinationdirectory`

*Exec the container*

```bash
docker exec -it 12344321 sh 
```

```bash
cd /opt
```

*create file*

```bash
touch abc.txt
```
```bash
exit
```


*see changes in host machine's `directory`*

```bash
/home/devopsmolvi/testingmount/
ls -l
cat abc.txt
```


---

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
