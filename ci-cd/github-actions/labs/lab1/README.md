



### 🏗️ Lab 1: The "Hello World" (Basic Trigger)
**Goal:** Understand how `on` and `run` work together.
* **Task:** Create a workflow that simply prints "Checking my DevOps progress" every time you push code.

```yaml
name: Hello-DevOps
on: [push]  # Trigger

jobs:
  say-hello:
    runs-on: ubuntu-latest
    steps:
      - name: Print Message
        run: echo "I am learning GitHub Actions in 2026!"
```



Commit Date: 25-April-2026
