


---

### 🛡️ Lab 2: The "Security First" (Trivy Scan)
**Goal:** Understand `uses` (pre-made tools) and how to protect your code.
* **Task:** Scan your repository for security vulnerabilities before you even think about building an image.

```yaml
name: Security-Scan
on: [push]

jobs:
  scan-code:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v4  # Uses a pre-made action

      - name: Run Trivy FS Scan
        uses: aquasecurity/trivy-action@master  # Uses a specialized security tool
        with:
          scan-type: 'fs'
          format: 'table'
```



Commit Date: 25-April-2026
