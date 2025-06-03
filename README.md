# 🧭 DevOps Portfolio Project Plan: E2E GitOps with CI/CD, EKS, Terraform, ArgoCD

> ⚙️ Project Goal: Deploy a microservices app (like Robot Shop) with full CI/CD, GitOps, observability, and infrastructure automation, in phases on weekends.

---

## 📅 Phase-wise Plan (Weekend-by-Weekend)

---

### ✅ Week 1: Project Initialization & Repo Setup

**Objective**: Prepare project structure, repos, and base environments.

**Tasks**:
- [ ] Create three GitLab repos:
  - `app-services` – app source code
  - `infra-terraform` – infra IaC code
  - `helm-charts` – Helm manifests
- [ ] Set up local Git remotes
- [ ] Draft `README.md` in each repo with purpose and tech stack
- [ ] Install essential CLIs:
  - AWS CLI, Terraform, kubectl, Helm, Vault CLI, Trivy, Checkov, gitleaks
- [ ] Create GitLab groups, runners (self-hosted or shared)

**Deliverables**:
- Clean project structure
- Base README in all repos
- Git remotes and runners ready

---

### ✅ Week 2: Terraform Infra Setup (EKS + VPC + DB)

**Objective**: Use Terraform to create foundational infra on AWS.

**Tasks**:
- [ ] Write Terraform modules for:
  - VPC, Subnets
  - EKS Cluster + Worker Nodes
  - RDS/Aurora DB (Postgres preferred)
- [ ] Enable S3 + DynamoDB for state backend
- [ ] Use `checkov` to scan Terraform for best practices
- [ ] Push infrastructure code to `infra-terraform` repo

**Commands**:
```bash
terraform init
terraform validate
terraform plan
terraform apply
checkov -d .
```

**Deliverables**:
- EKS + VPC + DB on AWS
- Modular, reusable Terraform
- GitLab CI for Terraform (with plan/apply stages)

---

### ✅ Week 3: Helm Chart & ArgoCD Setup

**Objective**: Prepare Helm templates and GitOps CD pipeline.

**Tasks**:
- [ ] Install ArgoCD on EKS via Helm
- [ ] Create basic Helm chart for 1 microservice (e.g., cart)
- [ ] Set up `helm-charts` repo with folders like:
  ```
  charts/
    cart/
    user/
    frontend/
  values/
    dev.yaml
    prod.yaml
  ```
- [ ] Configure ArgoCD to track `helm-charts` repo
- [ ] Setup ArgoCD application for `cart` service

**Deliverables**:
- Helm structure in place
- ArgoCD synced to Git repo
- One service auto-deployed via GitOps

---

### ✅ Week 4: CI Setup – Frontend Pipeline

**Objective**: Set up GitLab CI pipeline for frontend services

**Pipeline Steps**:
- Init
- Gitleaks
- Lint (ESLint)
- Build
- OWASP Dependency Check
- Unit tests (if any)
- Docker build
- Trivy image scan
- Push to ECR

**.gitlab-ci.yml Sample**:
```yaml
stages:
  - lint
  - test
  - build
  - scan
  - deploy
...
```

**Tasks**:
- [ ] Write GitLab CI pipeline
- [ ] Configure GitLab registry or AWS ECR
- [ ] Add badges & pipeline status to README

**Deliverables**:
- Full CI pipeline for frontend services
- Secure image pushed to ECR

---

### ✅ Week 5: CI for Backend with SonarQube

**Objective**: Backend CI pipeline with quality gates

**Pipeline Extras**:
- Post-unit SonarQube scan
- Trivy for image
- ECR push

**Tasks**:
- [ ] Install local SonarQube or use hosted version
- [ ] Add SonarQube step in backend `.gitlab-ci.yml`
- [ ] Validate test coverage + quality gates

**Deliverables**:
- CI pipeline for backend services
- SonarQube analysis results
- Artifacts in ECR

---

### ✅ Week 6: Vault Integration & Secret Management

**Objective**: Manage secrets securely

**Tasks**:
- [ ] Deploy Vault to EKS
- [ ] Enable Kubernetes auth method
- [ ] Use Vault Agent Sidecar or External Secrets
- [ ] Store secrets: DB credentials, JWT keys, etc.

**Deliverables**:
- Vault setup and accessible
- ArgoCD and apps pulling secrets securely

---

### ✅ Week 7: Monitoring – Prometheus, Grafana, ELK

**Objective**: Implement observability stack

**Tasks**:
- [ ] Install Prometheus + Grafana via Helm
- [ ] Connect EKS metrics + app metrics
- [ ] Setup ELK stack:
  - Filebeat or Fluentbit → Logstash → Elasticsearch
- [ ] Dashboards for key services

**Deliverables**:
- Monitoring & alerting dashboards
- Logs searchable in Kibana

---

### ✅ Week 8: CD & Canary Deployments (Argo Rollouts)

**Objective**: Add controlled deployment strategies

**Tasks**:
- [ ] Install Argo Rollouts
- [ ] Add rollout strategy to Helm templates
- [ ] Connect Argo Rollouts to ArgoCD
- [ ] Add health checks & metric-based promotion

**Deliverables**:
- Canary deployments
- Rollback safety
- ArgoCD dashboard integration

---

## 🧪 Bonus Enhancements (Optional)

| Feature                 | Tools                    |
|------------------------|--------------------------|
| Policy as Code         | OPA/Gatekeeper           |
| Sentry Integration     | Sentry.io                |
| Kubernetes Cost Report | Kubecost                 |
| Multi-region DR        | Route 53, cross-region S3|

---

## 📁 Suggested Repo Structure

```
robot-shop-devops/
├── app-services/            # All microservices
├── infra-terraform/         # EKS, RDS, VPC, etc.
├── helm-charts/             # All Helm templates
└── docs/                    # README, diagrams, guides
```

---

## 🧠 Notes

- Tag commits by feature or phase (`v1-infra`, `v2-ci`, etc.)
- Record demo videos for CI/CD + ArgoCD + Observability
- Write technical blogs on each phase

---

## ✅ Completion Outcome

You’ll have:
- AWS EKS setup via Terraform
- GitLab CI for frontend/backend (secure, scan-enabled)
- Helm + ArgoCD GitOps CD
- Vault secret management
- Monitoring + Logging dashboards
- Real-world showcase-level DevOps pipeline
