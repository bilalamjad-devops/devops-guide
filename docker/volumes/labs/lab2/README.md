
# Named Volume Lab (Companion to Your Bind Mount Lab)

You did **Bind Mount** (host directory → container).  
Now **Named Volume** (Docker-managed storage → container).

Same structure, but no host path — Docker handles the location.

---

## Named Volume Lab

**What makes it different:**
- Bind mount = you choose the host path (`/home/devopsmolvi/testingmount`)
- Named volume = Docker chooses the host path; you just give it a **name**

---

### Step 1: Create a named volume

```bash
docker volume create myvol
```

Verify it exists:
```bash
docker volume ls
```

Output:
```
DRIVER    VOLUME NAME
local     myvol
```

---

### Step 2: Run container and mount the volume

```bash
docker run -it -d -p 8080:80 -v myvol:/opt --name container2 nginx:latest
```

**Compare with your bind mount:**
| Your bind mount | This named volume |
|----------------|-------------------|
| `-v /home/devopsmolvi/testingmount:/opt` | `-v myvol:/opt` |
| You gave full host path | You gave only a name |

---

### Step 3: Exec into container

```bash
docker exec -it container2 sh
```

```bash
cd /opt
```

---

### Step 4: Create a file inside container

```bash
echo "This data is in a named volume" > mydata.txt
cat mydata.txt
```

```bash
exit
```

---

### Step 5: See that data survives container deletion

```bash
# Stop and remove the container
docker stop container2
docker rm container2

# Create a NEW container using the SAME volume
docker run --rm -v myvol:/opt alpine cat /opt/mydata.txt
```

Output:
```
This data is in a named volume
```

**Data survived** — even though the original container is gone.

---

### Step 6: Find where Docker stores the volume (on your host)

```bash
docker volume inspect myvol
```

Look for `"Mountpoint"` in the output:
```json
[
    {
        "Name": "myvol",
        "Mountpoint": "/var/lib/docker/volumes/myvol/_data"
    }
]
```

Now check it directly on your host:
```bash
sudo ls -l /var/lib/docker/volumes/myvol/_data
sudo cat /var/lib/docker/volumes/myvol/_data/mydata.txt
```

---

### Step 7: Clean up

```bash
docker volume rm myvol
```

---

## Side-by-Side Comparison (Your Lab vs This Lab)

| Step | Bind Mount (your lab) | Named Volume (this lab) |
|------|----------------------|-------------------------|
| **Create storage** | `mkdir testingmount` | `docker volume create myvol` |
| **Run container** | `-v /home/.../testingmount:/opt` | `-v myvol:/opt` |
| **Docker knows path?** | No — you told Docker | Yes — Docker manages it |
| **See file on host** | In `~/testingmount/` | In `/var/lib/docker/volumes/myvol/_data` |
| **Data survives `rm container`?** | ✅ Yes (files still on host) | ✅ Yes (Docker keeps volume) |
| **Delete storage** | `rm -rf ~/testingmount` | `docker volume rm myvol` |

---

## When to Use Which (Cheat Sheet)

| Use case | Choose |
|----------|--------|
| Development (edit code, see live changes) | **Bind Mount** |
| Need to share files from a specific host folder | **Bind Mount** |
| Production database (PostgreSQL, MySQL) | **Named Volume** |
| Data that must survive container deletion | **Named Volume** |
| You don't care where data lives on host | **Named Volume** |
| Backup/restore data easily | **Named Volume** (`docker run --volumes-from`) |

---

## Quick Memory Trick

```
Bind Mount   = You tell Docker WHERE (full path)
Named Volume = You tell Docker WHAT (name) — Docker decides WHERE
```

---

## Bonus: Multiple Containers Sharing Same Volume

```bash
# Create volume
docker volume create shared-data

# Container 1 writes data
docker run --rm -v shared-data:/data alpine sh -c 'echo "Hello from container1" > /data/message.txt'

# Container 2 reads the same data
docker run --rm -v shared-data:/data alpine cat /data/message.txt
```

Output:
```
Hello from container1
```

---

Do you want me to add both labs (bind mount + named volume) as a single `README.md` file for your `docker-guide/volumes/` folder?
