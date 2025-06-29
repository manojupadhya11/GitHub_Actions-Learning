### 🚀 GitHub Actions Runners

GitHub Actions **runners** are the servers that execute your workflows. This README explains what runners are, types of runners, how they work, and how to use or customize them in your GitHub Actions workflows.

---

## 🧠 What is a Runner?

A **runner** is a server (virtual machine or container) that GitHub Actions uses to execute jobs in a workflow. Each job in your workflow runs in its own runner.

---

## 🏁 Types of Runners

### 1️⃣ GitHub-Hosted Runners (Managed by GitHub)
These are temporary VMs created by GitHub. They come with pre-installed tools and are free for public repos.

#### 🔹 Available OS Options:
```yaml
runs-on: ubuntu-latest   # Linux
runs-on: windows-latest  # Windows
runs-on: macos-latest    # macOS
```
```yaml
jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - run: echo "Running on Linux"
```
#### 2️⃣ Self-Hosted Runners (Managed by You)
You can host your own runners on any machine (cloud or on-premise) for more control or specific tooling.

🔹 Setup:
Register your self-hosted runner via Settings > Actions > Runners

Download and configure the runner on your system
🔹 Use in workflow:
```yaml
jobs:
  build:
    runs-on: self-hosted
```
🔹 Optional Labels:
You can label self-hosted runners (e.g. self-hosted, linux, x64):

```
runs-on: [self-hosted, linux, arm64]
```

### 🔄 How Runners Work
A workflow is triggered (e.g., push, PR, or manual).

GitHub finds a suitable runner (runs-on).

A fresh runner environment is provisioned (if GitHub-hosted).

Steps are executed on the runner.

The runner is destroyed (if GitHub-hosted) after the job completes.

### ⚙️ Runners Context
You can access runner details using the runner context:
```| Context             | Description             |
| ------------------- | ----------------------- |
| `runner.os`         | The OS of the runner    |
| `runner.arch`       | The system architecture |
| `runner.name`       | Name of the runner      |
| `runner.temp`       | Path to temp dir        |
| `runner.tool_cache` | Path to tool cache dir  |
```

```- run: echo "Running on ${{ runner.os }} with architecture ${{ runner.arch }}"
```
### 🧹 Ephemeral Nature of GitHub Runners
GitHub-hosted runners are ephemeral: they reset after each job.

No data persists between jobs unless stored using artifacts, caches, or external storage.
