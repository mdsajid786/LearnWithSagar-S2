What are the key differences between GitHub Actions and Jenkins?

GitHub Actions and Jenkins are both popular tools for CI/CD (Continuous Integration and Continuous Deployment), but they differ in a few key areas. Here's a breakdown of the main differences:

### Summary Table:
---------------------------------------------------------------------------------------------------------
| Feature               | GitHub Actions                        | Jenkins                               |
|-----------------------|----------------------------------------|--------------------------------------|
| Hosting               | Cloud-native                          | Self-hosted                           |
| Setup                 | No setup required                     | Requires setup and maintenance        |
| Configuration         | YAML                                  | Groovy (Jenkinsfile)                  |
| Plugin Ecosystem      | Marketplace with limited actions      | Very large and mature plugin ecosystem|
| GitHub Integration    | Built-in                              | Requires plugins                      |
| Cost                  | Free with limits                      | Free, but infrastructure costs        |
| Flexibility           | Easy to use, less flexible            | Highly customizable                   |
---------------------------------------------------------------------------------------------------------


## Describe the general structure of a GitHub Actions workflow.

A **GitHub Actions workflow** is defined using a YAML file located in your repository under the `.github/workflows/` directory. The general structure includes several key components that define **when** the workflow runs, **what it does**, and **how it's executed**.

---

### 🔧 **General Structure**

```yaml
name: <Workflow Name>

on:
  <Event(s)>:        # Triggers like push, pull_request, schedule, workflow_dispatch, etc.

jobs:
  <job_id>:
    name: <Job Name>
    runs-on: <runner>  # e.g., ubuntu-latest, windows-latest, macos-latest
    steps:
      - name: <Step Name>
        uses: <action>           # Optional: Use a predefined action
        run: <shell command>     # Optional: Run custom commands
        with:                    # Optional: Input parameters for actions
          key: value
        env:                     # Optional: Environment variables
          VAR_NAME: value
```

---

### 🧩 **Key Components Explained**

#### **1. `name` (Optional)**
- A human-readable name for your workflow.

#### **2. `on`**
- Specifies the events that trigger the workflow.
```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [develop]
  schedule:
    - cron: '0 0 * * *'  # runs daily at midnight UTC
  workflow_dispatch:     # allows manual trigger
```

#### **3. `jobs`**
- A workflow can have multiple jobs that run either in parallel or sequentially.
```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test
```

#### **4. `steps`**
- Each job contains multiple steps that run sequentially.
- Steps can:
  - Use actions (`uses`)
  - Run shell commands (`run`)
  - Set environment variables (`env`)
  - Reference outputs from other steps

---

### 🧠 **Example Use Case**

```yaml
name: CI Pipeline

on:
  push:
    branches: [main]

jobs:
  test-and-build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout repo
        uses: actions/checkout@v3

      - name: Install Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Install dependencies
        run: pip install -r requirements.txt

      - name: Run tests
        run: pytest
```


How to manage variables and secrets in GitHub Actions?

Managing variables and secrets in GitHub Actions is crucial for securely handling sensitive information and making workflows more dynamic and reusable. Here's how to manage both:

---

## 🔐 **Secrets in GitHub Actions**

### **1. Repository-Level Secrets**
- Go to your repo on GitHub → **Settings** → **Secrets and variables** → **Actions** → **Secrets**.
- Click **"New repository secret"** and add your secret (e.g., `AWS_ACCESS_KEY`).

### **2. Using Secrets in Workflows**
```yaml
env:
  AWS_KEY: ${{ secrets.AWS_ACCESS_KEY }}
```

Or directly in a step:
```yaml
- name: Deploy to AWS
  run: aws deploy ...
  env:
    AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY }}
```

> 🔒 Secrets are encrypted and not exposed in logs. They can’t be accessed from pull requests from forks.

---

## 🧮 **Variables in GitHub Actions**

### **1. Repository-Level Variables**
- Go to **Settings** → **Secrets and variables** → **Actions** → **Variables**.
- Add variables like `ENVIRONMENT=production`.

### **2. Using Variables in Workflows**
```yaml
env:
  ENVIRONMENT: ${{ vars.ENVIRONMENT }}
```

Or inside a step:
```yaml
- name: Echo environment
  run: echo "Running in $ENVIRONMENT"
  env:
    ENVIRONMENT: ${{ vars.ENVIRONMENT }}
```

---

## 🎯 **Other Ways to Set Variables**

### **1. Job/Workflow-Level `env`**
Set environment variables for the whole job or workflow:
```yaml
env:
  GLOBAL_VAR: 'value'
```

### **2. Step-Level Output/Set Variable Dynamically**
```yaml
- name: Set custom variable
  id: set_var
  run: echo "MY_VAR=123" >> $GITHUB_ENV

- name: Use custom variable
  run: echo "My var is $MY_VAR"
```

---

## 🧩 **Best Practices**
- ✅ Use **secrets** for anything sensitive: API keys, tokens, passwords.
- ✅ Use **variables** for configuration values: environment names, file paths, versions.
- ❌ Avoid hardcoding secrets or config values directly in the workflow file.
- ✅ Use organization-level secrets/variables if sharing across repos.

---

Let me know if you want a quick demo workflow using secrets + variables!

