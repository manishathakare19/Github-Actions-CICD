# 🚀 GitHub Actions CI/CD Pipeline – Basics and Setup

## 🧩 Project Overview
This project demonstrates the **basics of GitHub Actions** — GitHub’s built-in CI/CD tool that automates workflows like building, testing, and deploying your code.  
It’s similar to Jenkins, but **GitHub manages the runners**, so you don’t need to maintain servers or install plugins.

---
<img width="1919" height="781" alt="Screenshot 2025-08-30 075803" src="https://github.com/user-attachments/assets/5f60e566-3b23-4666-b363-b219a25f2ddd" />
<img width="1919" height="763" alt="Screenshot 2025-08-30 075845" src="https://github.com/user-attachments/assets/b556ecfc-0af3-4ffc-b900-e7085a7cfaa6" />
<img width="1888" height="870" alt="Screenshot 2025-08-30 075821" src="https://github.com/user-attachments/assets/12ec9053-999f-49e7-aa63-aadc51318349" />


## ⚙️ Workflow Overview
- Folder: `.github/workflows/first-actions.yml`
- Trigger: Runs automatically on every `git push`
- Platform: `ubuntu-latest` (GitHub-hosted runner)

### 🧠 Example Workflow:
```yaml
name: My First GitHub Actions
on: [push]

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        python-version: [3.8, 3.9]

    steps:
      - uses: actions/checkout@v3
      - name: Set up Python
        uses: actions/setup-python@v2
        with:
          python-version: ${{ matrix.python-version }}
      - name: Install dependencies
        run: |
          python -m pip install --upgrade pip
          pip install pytest
      - name: Run tests
        run: |
          cd src
          python -m pytest addition.py
Every time code is pushed, this workflow:

Checks out the repository

Sets up Python (multiple versions)

Installs dependencies

Runs automated tests

🆚 Jenkins vs GitHub Actions
Feature	Jenkins	GitHub Actions
Server	Self-managed	Cloud-hosted by GitHub
Pipeline File	Jenkinsfile (Groovy)	.yml (YAML)
Secrets	Jenkins Credentials Store	GitHub Secrets
Maintenance	Manual setup	Auto-managed
Cost	Free (self-hosted)	Free for public repos

Analogy:

Jenkins = Your own kitchen 🍳
GitHub Actions = A restaurant kitchen with chefs ready to serve 👩‍🍳

🖥️ Runner Types
1️⃣ GitHub-Hosted Runner
Runs on GitHub’s servers (default).

Use: runs-on: ubuntu-latest

Simple setup for public projects.

2️⃣ Self-Hosted Runner
Run jobs on your own machine (EC2, VM, or on-prem).

Use: runs-on: self-hosted

Offers more control and power.

🔐 Secrets Management in CI/CD
Each platform secures credentials differently:

Jenkins → Credentials Store

GitHub Actions → Settings → Secrets and Variables

GitLab CI → Project Variables

Kubernetes → Kubeconfig / SealedSecrets

🧭 When to Use What
Scenario	Recommended Tool
Public / Open-source Project	GitHub Actions
Private or Sensitive Project	Jenkins or Self-hosted Runner
Heavy Compute Workloads	Self-hosted GitHub Runner or Jenkins Agent

✅ Final Takeaway
“If your code is public, let GitHub handle CI/CD.
If your code is private and sensitive, take control with Jenkins or self-hosted runners.”
