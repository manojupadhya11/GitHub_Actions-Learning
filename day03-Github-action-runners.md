# 🚀 GitHub Actions Runners

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
