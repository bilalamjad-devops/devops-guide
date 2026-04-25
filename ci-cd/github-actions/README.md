

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



Yes, we can definitely improve this! While your original list is a great foundation, a **Senior DevOps Engineer** looks for a few more "advanced" keywords that handle **Security**, **Organization**, and **Dependencies** between tasks.

To make this a truly "Excellent" resource for your portfolio, we should add the concepts of **Secrets**, **Permissions**, and **Context**.

---

### 🚀 The "Pro" DevOps Grammar (Improved)

Think of the workflow not just as a recipe, but as a **Secure Factory Pipeline**.

| Keyword | What it is | Why it's "Pro" | Real-world Example |
| :--- | :--- | :--- | :--- |
| **`env`** | Variables | Keeps your scripts clean and reusable. | `NODE_ENV: production` |
| **`secrets`** | Encrypted Data | **CRITICAL.** Never leak your AWS or Docker keys. | `${{ secrets.AWS_KEY }}` |
| **`needs`** | Dependency | Tells Job B to wait until Job A finishes successfully. | `needs: [build-job]` |
| **`permissions`** | Security Gate | Limits what the GitHub token can do (Least Privilege). | `contents: read` |
| **`with`** | Input | Passes specific settings to a `uses` action. | `push: true` |
| **`github` (Context)** | Metadata | Accesses data about the run (branch name, run number). | `${{ github.ref_name }}` |

---

### 📂 How to Visualize the Hierarchy
In DevOps, the structure of the YAML file is just as important as the keywords. You can explain it to your readers like this:



1.  **Workflow (`name`):** The whole project.
2.  **Triggers (`on`):** The event that starts the engine.
3.  **Jobs (`jobs`):** High-level goals (e.g., "Scan Code", "Build Image"). These run on separate servers unless you tell them otherwise.
4.  **Steps (`steps`):** The individual commands inside one job.
5.  **Actions (`uses` / `run`):** The specific code being executed.



Commit Date: 21-April-2026

Commit Date: 25-April-2026
