

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

Commit Date: 21-April-2026

Commit Date: 25-April-2026
