
# OWASP Juice Shop – DevSecOps CI/CD Pipeline

This project implements a full **DevSecOps GitLab CI/CD pipeline** for the [OWASP Juice Shop](https://owasp.org/www-project-juice-shop/) vulnerable web application.  
The pipeline integrates **security testing, compliance checks, automated deployments, GitOps, and real-time Slack notifications**.

---

## 🚀 Features

- **CI/CD Pipeline on GitLab** with the following stages:
  - `cache` – Dependency caching with Yarn.
  - `test` – Security scans (SAST, dependency scans, IaC scanning).
  - `build` – Docker image build and push to **AWS ECR** and **Docker Hub**.
  - `deploy-test` – Deploys Juice Shop to a remote test server via SSH.
  - `cd-gitops` – Updates GitOps repository with the new deployment manifest.
- **Security integrations**:
  - 🔎 **SAST** – Semgrep, njsscan, Bandit.  
  - 🧩 **Dependency Scanning** – Retire.js, Gitleaks.  
  - ☁️ **IaC Security** – Checkov for Terraform, YAML, and cloud templates.  
  - 🐳 **Container Security** – Trivy, Syft + Grype.  
  - 🛡️ **DAST** – OWASP ZAP baseline scan against deployed instance.  
  - 📦 **SBOM Generation** – Automated Software Bill of Materials.  
- **Slack Notifications**:
  - Real-time job updates: stage, status, commit, and user.
- **DefectDojo Integration**:
  - Centralized vulnerability management with automated report uploads.
- **OWASP Top 10 Mitigation**:
  - Addressed multiple critical Juice Shop vulnerabilities at the source-code level.

---

## 🛠️ Tools & Technologies

- **CI/CD**: GitLab CI/CD  
- **Languages/Frameworks**: Node.js (Juice Shop), Python (scripts)  
- **Security**: Semgrep, njsscan, Retire.js, Bandit, Checkov, Gitleaks, Trivy, Syft, Grype, OWASP ZAP  
- **Cloud & Container**: Docker, AWS ECR, Docker Hub  
- **Vulnerability Management**: DefectDojo  
- **Messaging**: Slack Webhooks  
- **GitOps**: Kubernetes manifests stored in a dedicated repo  

---

## 📂 Pipeline Overview

```mermaid
flowchart TD
    A[Code Commit] --> B[Cache Dependencies]
    B --> C[SAST & Dependency Scans]
    C --> D[Build Docker Image]
    D --> E[Container & SBOM Scans]
    D --> F[Push to AWS ECR & Docker Hub]
    F --> G[Deploy to Test Server via SSH]
    G --> H[DAST - OWASP ZAP Scan]
    G --> I[CD - Update GitOps Repo]
    C --> J[Upload Security Reports to DefectDojo]
````

---

## 🔧 Setup Instructions

### 1. Clone the repository

```bash
git clone https://gitlab.com/<your-namespace>/juice-shop-devsecops.git
cd juice-shop-devsecops
```

### 2. Configure CI/CD variables in GitLab

Add the following variables under **Settings > CI/CD > Variables**:

* `DOCKER_USER` / `DOCKER_PASS`
* `AWS_ACCESS_KEY_ID` / `AWS_SECRET_ACCESS_KEY` / `AWS_ACCOUNT_ID` / `AWS_DEFAULT_REGION`
* `SERVER_IP` / `SERVER_USER` / `SSH_PRIVATE_KEY`
* `SEMGREP_APP_TOKEN`
* `SLACK_WEBHOOK`
* `GIT_USER` / `GIT_PASS` / `GITOPS_REPO`
* `REGISTRY`

### 3. Run the pipeline

Push a commit to trigger the pipeline:

```bash
git commit --allow-empty -m "Trigger pipeline"
git push origin main
```

### 4. Monitor

* Slack for pipeline job notifications 📩
* GitLab for detailed logs 📝
* DefectDojo for vulnerability tracking 🔐

---

## 📊 Security Reports Collected

* `gitleaks.json` – Hardcoded secrets detection
* `njsscan.sarif` – Node.js SAST
* `semgrep.json` – General static analysis
* `bandit.json` – Python SAST
* `retire.json` – JS dependency vulnerabilities
* `trivy.json` – Container vulnerability scan
* `grype_output.json` – SBOM + vuln scan results
* `baseline.xml` – OWASP ZAP DAST report

---

## 🏆 Achievements

* Built a **comprehensive DevSecOps CI/CD pipeline** integrating **SAST, DAST, dependency, IaC scanning, and SBOM**.
* Automated vulnerability handling via **DefectDojo**, ensuring compliance and centralized management.
* Eliminated multiple **OWASP Top 10 vulnerabilities** at the source-code level.
* Enhanced security posture while maintaining **fast and automated deployments**.

---

## 📜 License

This project is for **educational and research purposes** only.
OWASP Juice Shop is licensed under [GNU AGPL v3.0](https://github.com/juice-shop/juice-shop/blob/master/LICENSE).

