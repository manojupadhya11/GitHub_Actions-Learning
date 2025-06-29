# 🚀 GitHub Actions: First Sample Workflow

This repository demonstrates a basic **GitHub Actions** workflow and explains key CI/CD concepts like workflows, runners, jobs, events, and actions.

---

## 🧠 What is GitHub Actions?

GitHub Actions is a **CI/CD (Continuous Integration and Continuous Deployment)** platform that allows you to **automate tasks** within your software development lifecycle, directly inside GitHub repositories.

---

## 📘 Key Concepts in GitHub Actions

### 🔹 Workflow
A **workflow** is an automated process defined in a YAML file. It is triggered by events (e.g., code pushes, pull requests) and consists of one or more jobs.

> 🗂️ Location: `.github/workflows/sample.yml`

---

### 🔹 Runner
A **runner** is a server that runs your workflows. It can be:
- **GitHub-hosted** (e.g., `ubuntu-latest`, `windows-latest`)
- **Self-hosted** (your own machine)

---

### 🔹 Job
A **job** is a group of steps that are executed on the same runner. Jobs can run in **parallel or sequentially** depending on dependencies.

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
