# 🔧 GitHub Actions Variables - Complete Guide

This document explains **all types of variables** used in GitHub Actions. It includes how they work, how to define them, where they are used, and examples for each.

---

##  Workflow Inputs (`on.workflow_dispatch.inputs`)

These variables are passed when manually triggering a workflow. You define them under `workflow_dispatch`.
  run: echo "Hello, ${{ inputs.name }}"


### 🔹 How to define:
```yaml
on:
  workflow_dispatch:
    inputs:
      name:
        description: "Your name"
        required: true
        default: "John"
```

## Environment Variables (env)
Environment variables can be declared at the workflow, job, or step level.

🔹 Workflow-level env:
```yaml
  env:
  GLOBAL_ENV: "I am global"
```
🔹 job-level env:
```yaml
  jobs:
  example:
    env:
      JOB_ENV: "I am job level"
```
        
🔹 Step-level env:
```yaml
  - name: Print step variable
  env:
    STEP_ENV: "I am step level"
  run: echo "Step: $STEP_ENV"
```
## 3️⃣ GitHub Context Variables (github, env, runner, etc.)
These are built-in variables provided by GitHub Actions. You access them using ${{ }}.
    github.actor
    github.repository
    runner.os

## 4️⃣ Step Outputs (GITHUB_OUTPUT)
Used to pass data from one step to another in the same job.

🔹 Set an output:
```yaml
- name: Set output
  id: example
  run: echo "message=Hello" >> $GITHUB_OUTPUT
 ```
🔹 Access output:
```yaml
  - name: Use output
  run: echo "${{ steps.example.outputs.message }}"
```
## 5️⃣ Job Outputs (outputs & needs)
Used to pass data between jobs.

🔹 Producing job:
```yaml
jobs:
  producer:
    runs-on: ubuntu-latest
    outputs:
      my_output: ${{ steps.set.outputs.message }}
    steps:
      - id: set
        run: echo "message=42" >> $GITHUB_OUTPUT
          ```
🔹 Consuming job:
```yaml
  consumer:
    needs: producer
    runs-on: ubuntu-latest
    steps:
      - run: echo "Message: ${{ needs.producer.outputs.my_output }}"
```
## 6️⃣ Secrets (secrets)
Used to store sensitive values such as API keys, tokens, passwords.

🔹 Define:
Go to Repository > Settings > Secrets and create MY_SECRET.

🔹 Use:
```yaml
run: echo "${{ secrets.MY_SECRET }}"
Note: GitHub masks secrets in logs to protect sensitive data.
```

## 🔹 Input Variables in GitHub Actions
Input variables allow you to manually pass data into a workflow when it's triggered using the workflow_dispatch event. These are useful for dynamic workflows like deployments, testing with parameters, or triggering conditional logic.


✅ How to Define Input Variables
Define them under the on.workflow_dispatch.inputs section:

```yaml
on:
  workflow_dispatch:
    inputs:
      environment:
        description: 'Environment to deploy to'
        required: true
        default: 'dev'
      version:
        description: 'App version'
        required: false
        default: 'latest'
```
```yaml
| Property      | Description                         |
| ------------- | ----------------------------------- |
| `description` | A short explanation shown in the UI |
| `required`    | Whether this input must be provided |
| `default`     | Default value used if not provided  |

```

## 🚀 How to Use Inputs in Workflow Steps
```
jobs:
  example:
    runs-on: ubuntu-latest
    steps:
      - name: Print inputs
        run: |
          echo "Environment: ${{ inputs.environment }}"
          echo "Version: ${{ inputs.version }}"
```

Inputs are accessed via ${{ inputs.input_name }} and are always strings.
