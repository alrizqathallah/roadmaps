# ⚙️ DevOps Learning Roadmap: Beginner to Advanced
### Industry-Focused · Practical · Implementable

> **How to use this roadmap:** Follow phases sequentially. DevOps is a *culture and practice* as much as a toolset — understanding the *why* behind each tool is as important as the *how*. Every phase requires hands-on work in real environments. Estimated durations assume 1.5–2 hours of focused daily practice.

---

## 📍 Phase 0 — Foundations & Mindset
**Duration:** 1–2 weeks | **Goal:** Understand what DevOps is, set up your environment, and build the foundational knowledge everything else rests on

### What DevOps Actually Is
- DevOps is **not** a job title, a tool, or a team — it is a set of practices that unify software development and operations to shorten delivery cycles and increase reliability
- The Three Ways: Flow (fast left-to-right delivery), Feedback (fast right-to-left learning), Continual Learning & Experimentation
- CALMS framework: Culture, Automation, Lean, Measurement, Sharing
- DevOps vs SRE (Site Reliability Engineering) vs Platform Engineering — how they relate
- The cost of slow feedback loops: why 10-minute deploys beat 10-week release cycles
- Key metrics: DORA metrics (Deployment Frequency, Lead Time, Change Failure Rate, Time to Restore)

### Prerequisites to Have Before Starting
| Skill | Minimum Level | Covered In |
|-------|--------------|------------|
| Linux CLI | Comfortable in the terminal | Linux Roadmap Phase 1–2 |
| Bash scripting | Can write basic scripts | Linux Roadmap Phase 2 |
| Networking basics | TCP/IP, DNS, HTTP, ports | Linux Roadmap Phase 3 |
| Git basics | commit, push, pull, branch | This phase |
| One programming language | Python preferred | Python Roadmap Phase 1–2 |

### Environment Setup
- A Linux environment (Ubuntu 24.04 LTS): WSL2, VirtualBox, or cloud VM
- Install: `git`, `curl`, `wget`, `jq`, `tree`, `make`, `python3`, `pip3`
- Create accounts: GitHub, DockerHub, AWS Free Tier (or GCP/Azure)
- Install VS Code with extensions: Docker, Kubernetes, GitLens, HashiCorp Terraform, YAML
- Set up a personal GitHub organization for all roadmap projects
- Configure SSH keys for GitHub: Ed25519, added to `~/.ssh/config`

### Git — Version Control Mastery
Git is the foundation of every DevOps practice. Master it before everything else.

- Repository lifecycle: `init`, `clone`, `add`, `commit`, `push`, `pull`, `fetch`
- Branching model: `branch`, `checkout`, `merge`, `rebase`
- Interactive rebase: `git rebase -i HEAD~n` — squash, reorder, edit commits
- `git stash` — save and restore work in progress
- `git cherry-pick` — apply specific commits
- `git bisect` — binary search for a regression-introducing commit
- `git log --oneline --graph --all` — visualizing branch history
- `.gitignore` — patterns, global ignore, language templates
- **Branching strategies:**
  - **GitFlow** — feature, develop, release, hotfix branches
  - **GitHub Flow** — simple: branch from main, PR, merge
  - **Trunk-Based Development** — the DevOps standard: short-lived branches, daily merges to main
- **Conventional Commits** — structured commit messages: `feat:`, `fix:`, `chore:`, `docs:`, `refactor:`
- `git tag` — semantic versioning tags (`v1.2.3`)
- Signing commits with GPG

### 📝 Exercises (Phase 0)
1. **Git History Rewrite** — clone a repo, make 5 commits with intentional mistakes, then use interactive rebase to squash, rename, and reorder them
2. **Conflict Resolution** — create two branches that modify the same lines; merge them and resolve the conflict manually
3. **Bisect Bug Hunt** — use `git bisect` to find which commit introduced a bug in a prepared repository
4. **Branching Model Setup** — initialize a repository and implement the GitHub Flow model with branch protection rules on GitHub (require PR review, passing CI)

---

## 🟢 Phase 1 — Containerization with Docker
**Duration:** 4–5 weeks | **Goal:** Package, run, and orchestrate applications in containers

### 1.1 Container Fundamentals
- Why containers? The "works on my machine" problem solved
- Containers vs virtual machines: namespaces, cgroups, overlay filesystems
- Docker architecture: daemon (`dockerd`), client (`docker`), registry
- **Core Docker workflow:**
  ```bash
  docker pull nginx:alpine
  docker run -d -p 8080:80 --name webserver nginx:alpine
  docker logs webserver
  docker exec -it webserver /bin/sh
  docker stop webserver && docker rm webserver
  ```
- Image layers and the union filesystem
- `docker ps`, `docker images`, `docker inspect`, `docker stats`
- Container lifecycle: created → running → paused → stopped → removed

### 1.2 Building Images — Dockerfile Mastery
- `FROM`, `RUN`, `COPY`, `ADD`, `WORKDIR`, `EXPOSE`, `ENV`, `ARG`, `CMD`, `ENTRYPOINT`
- `CMD` vs `ENTRYPOINT` — the critical distinction
- Layer caching — ordering instructions for maximum cache reuse
- Multi-stage builds — the key to small production images:
  ```dockerfile
  # Stage 1: Build
  FROM node:20-alpine AS builder
  WORKDIR /app
  COPY package*.json ./
  RUN npm ci --only=production
  COPY . .
  RUN npm run build

  # Stage 2: Production
  FROM nginx:alpine AS production
  COPY --from=builder /app/dist /usr/share/nginx/html
  EXPOSE 80
  CMD ["nginx", "-g", "daemon off;"]
  ```
- `.dockerignore` — never send unnecessary context to the daemon
- Image tagging strategy: `name:version`, `name:latest`, `name:sha256`
- **Dockerfile best practices:**
  - Run as non-root user (`USER appuser`)
  - Use specific base image versions, not `latest`
  - Combine `RUN` commands to minimize layers
  - Use `COPY` over `ADD` unless extracting archives
  - Pin dependency versions for reproducibility
  - Scan images: `docker scout`, `trivy`

### 1.3 Networking & Storage
- Docker network types: bridge, host, overlay, none
- User-defined bridge networks — containers communicate by name
- `docker network create`, `inspect`, `connect`, `disconnect`
- Port publishing: `-p hostPort:containerPort`
- **Volumes and bind mounts:**
  - Named volumes: `docker volume create`, managed by Docker
  - Bind mounts: `-v /host/path:/container/path` for development
  - `tmpfs` mounts: in-memory, never written to disk
- Volume backup and restore patterns

### 1.4 Docker Compose
- `docker-compose.yml` / `compose.yaml` structure
- Services, networks, volumes — declarative multi-container apps
- Environment variables: `.env` files, `environment:`, `env_file:`
- Health checks: `healthcheck:` with retry and interval
- Service dependencies: `depends_on:` with `condition: service_healthy`
- `docker compose up -d`, `down`, `logs -f`, `exec`, `ps`, `pull`
- Override files: `docker-compose.override.yml` for local dev customization
- Scaling services: `docker compose up --scale worker=4`
- Full example: web app + PostgreSQL + Redis + background worker

### 1.5 Image Registry & Security
- DockerHub: push/pull, public vs private repositories
- Private registries: AWS ECR, GCP Artifact Registry, GitHub Container Registry (`ghcr.io`), self-hosted Harbor
- `docker login`, `docker tag`, `docker push`, `docker pull`
- Image scanning for vulnerabilities: `trivy image <name>`
- Image signing: Docker Content Trust, `cosign`
- SBOM (Software Bill of Materials) — generating with `syft`
- Secrets in containers: **never** bake secrets into images; use environment variables, Docker secrets, or external vaults

### 📝 Exercises (Phase 1)
1. **Slim a Bloated Image** — take a naive Python app image (800MB+), apply multi-stage builds and Alpine base; get it under 100MB
2. **Compose Stack** — write a `compose.yaml` for a web app with PostgreSQL and Redis; include health checks so the app waits for DB readiness
3. **Image Security Scan** — pull 3 different images, run `trivy` on each, compare vulnerability counts, and find a version with fewer CVEs
4. **Layer Cache Optimization** — deliberately order Dockerfile instructions incorrectly, time a rebuild; then reorder correctly and compare cache hit rate
5. **Custom Network** — run three containers on a custom bridge network; verify they resolve each other by name; verify isolation from the default bridge

### 🔨 Mini-Project 1: Containerized Microservices Application
Design and containerize a multi-service application:
- **Services:** API server (Python/FastAPI), Frontend (Nginx serving React build), PostgreSQL, Redis cache, background worker
- Multi-stage Dockerfiles for every service
- `compose.yaml` with health checks and dependency ordering
- Named volumes for database persistence
- Separate `compose.override.yml` for dev (hot reload) vs prod (optimized)
- All images scanned and passing `trivy` with no CRITICAL CVEs
- Images pushed to GitHub Container Registry with semantic version tags
- `Makefile` with targets: `build`, `up`, `down`, `logs`, `test`, `push`

---

## 🟡 Phase 2 — CI/CD Pipelines
**Duration:** 5–6 weeks | **Goal:** Automate testing, building, and deploying software reliably

### 2.1 CI/CD Fundamentals
- Continuous Integration: merge code frequently, build and test automatically on every push
- Continuous Delivery: every passing build *can* be deployed
- Continuous Deployment: every passing build *is* deployed automatically
- Pipeline stages: Source → Build → Test → Security Scan → Package → Deploy
- Artifact management: what gets built, stored, and deployed
- Pipeline as Code — pipelines live in the repository alongside the code they build
- Idempotency in pipelines — running twice should produce the same result
- Feedback speed: why a 2-minute pipeline beats a 30-minute one

### 2.2 GitHub Actions (Primary)
The industry's most widely used CI/CD platform.

**Core concepts:**
- Workflows: YAML files in `.github/workflows/`
- Events: `push`, `pull_request`, `schedule`, `workflow_dispatch`, `release`
- Jobs: parallel or sequential units of work
- Steps: individual commands or actions within a job
- Runners: `ubuntu-latest`, `macos-latest`, `windows-latest`, self-hosted

**Workflow anatomy:**
```yaml
name: CI Pipeline

on:
  push:
    branches: [main, develop]
  pull_request:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-python@v5
        with:
          python-version: '3.12'
      - run: pip install -r requirements.txt
      - run: pytest --cov=app tests/
```

**Key features:**
- `secrets` — encrypted secrets at repo, environment, and org level
- `env` — environment variables at workflow, job, and step level
- Matrix builds: test across multiple versions/OS combinations
- Caching: `actions/cache` for dependencies (pip, npm, Maven, Go modules)
- Artifacts: `actions/upload-artifact` / `download-artifact`
- Reusable workflows: `workflow_call` — DRY pipelines
- Composite actions: package multiple steps as a reusable action
- Environments with protection rules: require approvals before deploying to production
- `concurrency` — cancel in-progress runs on new push
- OIDC authentication: keyless cloud authentication (no stored credentials)

### 2.3 GitLab CI/CD
- `.gitlab-ci.yml` structure: stages, jobs, scripts
- GitLab-specific features: merge request pipelines, environments, protected branches
- GitLab Container Registry integration
- Self-hosted GitLab Runner setup and registration
- Cache and artifacts in GitLab CI
- Comparison with GitHub Actions: when to choose each

### 2.4 Jenkins (Enterprise Context)
- Jenkins architecture: controller, agents, plugins
- `Jenkinsfile` — declarative vs scripted pipeline syntax
- Blue Ocean — modern Jenkins UI
- Shared libraries — reusable Groovy code for pipelines
- When Jenkins makes sense (large enterprises, complex legacy requirements)

### 2.5 Pipeline Patterns & Best Practices
- **Shift-left security:** run security scans early, not at the end
- **Fast feedback first:** lint and unit tests before slow integration tests
- **Pipeline stages in production order:**
  1. Lint & format check
  2. Unit tests
  3. Build artifact / Docker image
  4. Security scan (SAST, image scan)
  5. Integration tests
  6. Deploy to staging
  7. Smoke tests on staging
  8. Deploy to production (with approval gate if CD)
  9. Post-deploy health check
- **Dependency caching** — never download the same packages twice
- **Branch-based deployment rules:** feature branches → dev; main → staging; tags → production
- **Semantic versioning automation:** `semantic-release`, `release-please`
- **Rollback strategy:** always know how to undo a deployment

### 2.6 Testing in CI Pipelines
- Unit tests: fast, isolated, run on every commit
- Integration tests: test service boundaries, run after build
- End-to-end tests: full user flow, run against deployed environments
- **Test coverage gates:** fail the pipeline below a threshold
- Contract testing: `Pact` — verify API consumer/provider contracts
- Performance testing in CI: `k6`, `Locust` — catch regressions early
- Test result reporting: JUnit XML format, GitHub Actions test summaries

### 2.7 Artifact & Release Management
- Semantic Versioning (SemVer): `MAJOR.MINOR.PATCH`
- Automated changelog generation from conventional commits
- GitHub Releases and release assets
- Package registries: PyPI, npm, Maven Central, GitHub Packages
- Artifact retention policies — clean up old artifacts

### 📝 Exercises (Phase 2)
1. **First Pipeline** — create a GitHub Actions workflow that lints, tests, and builds a Docker image on every PR to `main`; fail the PR if any step fails
2. **Matrix Build** — test a Python package across Python 3.10, 3.11, and 3.12 on Ubuntu and macOS in parallel; display a test summary
3. **Dependency Cache** — add caching to a pipeline; measure and document the time saved on cache hits
4. **OIDC Cloud Auth** — configure GitHub Actions to authenticate to AWS using OIDC (no stored access keys); push an image to ECR
5. **Environment Protection** — set up `staging` and `production` GitHub environments; require a manual approval before the production deploy job runs

### 🔨 Mini-Project 2: Full CI/CD Pipeline for a Real Application
Build a complete, production-grade pipeline for the containerized app from Phase 1:
- **Trigger:** PR to `main` → full CI; merge to `main` → deploy to staging; Git tag → deploy to production
- **CI jobs (parallel):** lint, unit tests, security scan (Trivy + SAST with CodeQL)
- **Build:** multi-arch Docker image (`linux/amd64`, `linux/arm64`) via `docker buildx`
- **Staging deploy:** automated to a cloud VM via SSH + Docker Compose
- **Integration test job:** run against the staging environment
- **Production deploy:** manual approval gate, then deploy; post-deploy smoke test
- **Notifications:** Slack/email on failure and on successful production deploy
- **Release automation:** `release-please` generates changelog and bumps version on merge to `main`
- Zero stored cloud credentials (OIDC throughout)

---

## 🟠 Phase 3 — Infrastructure as Code
**Duration:** 5–6 weeks | **Goal:** Provision and manage all infrastructure through code, not consoles

### 3.1 IaC Philosophy
- Why IaC? Consistency, repeatability, auditability, speed
- Imperative vs declarative IaC: scripts vs desired-state tools
- Idempotency — the core requirement of good IaC
- IaC and Git: all infrastructure changes go through pull requests
- The IaC maturity model: manual → scripted → declarative → policy-enforced
- State management: why tracking what exists is hard and important
- Drift detection: what happens when someone changes infrastructure outside of IaC

### 3.2 Terraform (Primary)
The industry-standard tool for cloud infrastructure provisioning.

**Core concepts:**
```hcl
# Provider configuration
terraform {
  required_providers {
    aws = {
      source  = "hashicorp/aws"
      version = "~> 5.0"
    }
  }
  backend "s3" {
    bucket = "my-terraform-state"
    key    = "prod/terraform.tfstate"
    region = "us-east-1"
  }
}

# Resource definition
resource "aws_instance" "web" {
  ami           = data.aws_ami.ubuntu.id
  instance_type = "t3.micro"
  tags = {
    Name        = "web-server"
    Environment = var.environment
  }
}
```

**Terraform workflow:**
- `terraform init` — initialize providers and backend
- `terraform plan` — preview changes (always review before apply)
- `terraform apply` — apply changes
- `terraform destroy` — tear down infrastructure
- `terraform fmt` — format code
- `terraform validate` — validate configuration
- `terraform state` — inspect and manipulate state

**Key concepts to master:**
- Resources, data sources, variables, outputs, locals
- `terraform.tfvars` and `*.auto.tfvars` — variable files
- State backends: S3 + DynamoDB for remote state and locking
- Modules: reusable infrastructure components
  - Root module, child modules, published modules (Terraform Registry)
  - Module versioning and pinning
- `for_each` and `count` — creating multiple resources
- `dynamic` blocks — conditional nested blocks
- `lifecycle` rules: `prevent_destroy`, `create_before_destroy`, `ignore_changes`
- Data sources — query existing infrastructure
- Provisioners (avoid when possible): `local-exec`, `remote-exec`
- Workspaces — managing multiple environments (prefer separate state files)

**Terraform best practices:**
- One state file per environment per service
- Pin all provider versions
- Write modules for everything reused more than once
- Always run `plan` before `apply` — review every change
- Store state remotely, never locally
- Use `terraform-docs` to auto-generate module documentation
- Test with `terratest` (Go) or `checkov` for policy compliance

### 3.3 Ansible (Configuration Management)
Where Terraform provisions infrastructure, Ansible configures it.

**Core concepts:**
- Agentless: connects via SSH (Linux) or WinRM (Windows)
- Inventory: static files, dynamic inventory scripts, plugins
- Playbooks: YAML describing desired state
- Roles: reusable, structured collections of tasks
- Modules: the building blocks (`apt`, `service`, `copy`, `template`, `user`, `cron`, `docker_container`)
- Idempotency: running a playbook twice should make no changes the second time
- Variables: `group_vars/`, `host_vars/`, `defaults/`, `vars/`
- `ansible-vault` — encrypting secrets in version control
- Handlers — tasks triggered by changes (e.g., restart Nginx when config changes)
- `when` conditions, `loop`, `block`/`rescue`/`always`
- Jinja2 templates — dynamic configuration files
- Roles from Ansible Galaxy — community roles

**Ansible + Terraform integration:**
- Terraform provisions the VM → outputs the IP → Ansible configures the VM
- Dynamic inventory from Terraform state or cloud provider

### 3.4 Pulumi (Modern IaC)
- IaC using real programming languages (Python, TypeScript, Go)
- When Pulumi beats Terraform: complex logic, loops, conditions
- Pulumi state management: Pulumi Cloud vs self-managed
- Side-by-side comparison with Terraform for the same infrastructure

### 3.5 Cloud Provider Foundations
You must understand what you are provisioning. Focus on one provider first (AWS recommended).

**AWS Core Services for DevOps:**
| Service | Purpose |
|---------|---------|
| EC2 | Virtual machines |
| VPC | Virtual networking (subnets, route tables, IGW, NAT) |
| S3 | Object storage (also Terraform state) |
| RDS | Managed relational databases |
| ECS / EKS | Container orchestration |
| IAM | Identity and access management |
| Route 53 | DNS |
| CloudWatch | Monitoring and logging |
| ALB / NLB | Load balancing |
| ECR | Container image registry |
| Secrets Manager | Secret storage |
| ACM | TLS certificate management |

- **Networking fundamentals in AWS:** VPC, public/private subnets, NAT Gateway, Internet Gateway, security groups, NACLs
- **IAM:** least privilege, roles vs users, instance profiles, OIDC federation
- **Cost management:** Free Tier limits, Cost Explorer, billing alerts, resource tagging

### 3.6 Policy as Code
- Why infrastructure needs guardrails, not just documentation
- **Open Policy Agent (OPA)** — general-purpose policy engine
- **Checkov** — static analysis for Terraform, CloudFormation, Kubernetes
- **tfsec** / **Terrascan** — Terraform security scanning
- **Sentinel** (HashiCorp) — policy framework for Terraform Enterprise
- Integrating policy checks into CI pipelines: fail the PR on policy violation
- Cost estimation: `infracost` — see the cost impact of IaC changes in PRs

### 📝 Exercises (Phase 3)
1. **VPC from Scratch** — write Terraform to create a VPC with public and private subnets, NAT Gateway, Internet Gateway, and route tables across 3 AZs
2. **Reusable Module** — extract a common pattern (e.g., "EC2 instance with security group and IAM role") into a Terraform module; use it twice with different variables
3. **Ansible Role** — write an Ansible role that installs and configures Nginx with a Jinja2 template config, enables it as a systemd service, and opens the firewall
4. **Drift Detection** — manually change a resource in the AWS console; run `terraform plan` and observe the detected drift; apply to restore desired state
5. **Policy Gate** — add `checkov` to a GitHub Actions pipeline; configure it to fail on any HIGH-severity Terraform security finding

### 🔨 Mini-Project 3: Cloud Infrastructure Platform
Provision a complete, production-grade cloud environment using Terraform and Ansible:
- **Networking:** VPC with public/private subnets across 3 AZs, NAT Gateway, VPN or bastion host
- **Compute:** Auto Scaling Group of EC2 instances running the app from Phase 1, behind an Application Load Balancer with TLS termination
- **Database:** RDS PostgreSQL in private subnets, with automated backups and Multi-AZ
- **Storage:** S3 bucket for static assets, CloudFront CDN distribution
- **DNS:** Route 53 hosted zone with records pointing to ALB and CloudFront
- **Security:** All secrets in AWS Secrets Manager; IAM roles (no access keys); security groups following least privilege
- **Configuration:** Ansible playbooks to configure all EC2 instances (installed via user-data bootstrapping)
- **Policy:** `checkov` and `infracost` integrated in CI; block any HIGH CVEs or >20% cost increase
- **Modules:** All reusable components extracted into local modules
- Fully documented with `terraform-docs`

---

## 🔴 Phase 4 — Container Orchestration with Kubernetes
**Duration:** 6–7 weeks | **Goal:** Deploy, manage, and scale containerized applications on Kubernetes

### 4.1 Kubernetes Architecture
- Why Kubernetes? What problems does it solve beyond Docker Compose?
- Control plane components:
  - `kube-apiserver` — the API endpoint for all operations
  - `etcd` — distributed key-value store for cluster state
  - `kube-scheduler` — assigns pods to nodes
  - `kube-controller-manager` — reconciliation loops (desired vs actual state)
  - `cloud-controller-manager` — cloud provider integration
- Node components:
  - `kubelet` — node agent, ensures containers run as specified
  - `kube-proxy` — network rules on nodes
  - Container runtime (`containerd`, `cri-o`)
- The reconciliation loop — Kubernetes' core design principle

### 4.2 Core Kubernetes Objects
```
Kubernetes Objects
├── Workloads
│   ├── Pod            — smallest deployable unit (1+ containers)
│   ├── Deployment     — stateless apps with rolling updates
│   ├── StatefulSet    — stateful apps (databases) with stable identity
│   ├── DaemonSet      — one pod per node (monitoring agents, log shippers)
│   ├── Job            — run-to-completion tasks
│   └── CronJob        — scheduled Jobs
├── Networking
│   ├── Service        — stable network endpoint (ClusterIP, NodePort, LoadBalancer)
│   ├── Ingress        — HTTP routing and TLS termination
│   └── NetworkPolicy  — firewall rules between pods
├── Configuration
│   ├── ConfigMap      — non-secret configuration data
│   └── Secret         — sensitive data (base64-encoded, use external secret managers)
├── Storage
│   ├── PersistentVolume (PV)      — storage resource
│   ├── PersistentVolumeClaim (PVC) — request for storage
│   └── StorageClass   — dynamic provisioning
└── Access Control
    ├── ServiceAccount — identity for pods
    ├── Role / ClusterRole — permission definitions
    └── RoleBinding / ClusterRoleBinding — bind roles to subjects
```

### 4.3 kubectl Mastery
```bash
# Core operations
kubectl get pods -n <namespace> -o wide
kubectl describe pod <name>
kubectl logs <pod> -c <container> -f --previous
kubectl exec -it <pod> -- /bin/sh
kubectl apply -f manifest.yaml
kubectl delete -f manifest.yaml

# Debugging
kubectl get events --sort-by='.lastTimestamp'
kubectl top pods --sort-by=cpu
kubectl port-forward svc/myapp 8080:80

# Resource management
kubectl scale deployment myapp --replicas=5
kubectl rollout status deployment/myapp
kubectl rollout undo deployment/myapp
kubectl rollout history deployment/myapp
```

### 4.4 Writing Production Kubernetes Manifests
- YAML manifest anatomy: `apiVersion`, `kind`, `metadata`, `spec`
- Deployment best practices:
  ```yaml
  spec:
    replicas: 3
    strategy:
      type: RollingUpdate
      rollingUpdate:
        maxUnavailable: 1
        maxSurge: 1
    template:
      spec:
        containers:
          - name: app
            image: myapp:1.2.3      # Never use :latest in production
            resources:
              requests:
                cpu: "100m"
                memory: "128Mi"
              limits:
                cpu: "500m"
                memory: "512Mi"
            readinessProbe:         # When is the pod ready for traffic?
              httpGet:
                path: /healthz
                port: 8080
              initialDelaySeconds: 5
              periodSeconds: 10
            livenessProbe:          # When should the pod be restarted?
              httpGet:
                path: /healthz
                port: 8080
            securityContext:
              runAsNonRoot: true
              readOnlyRootFilesystem: true
              allowPrivilegeEscalation: false
  ```
- Resource requests and limits — always set both; understand QoS classes
- `HorizontalPodAutoscaler` (HPA) — scale on CPU/memory/custom metrics
- `PodDisruptionBudget` (PDB) — maintain availability during node drains
- `topologySpreadConstraints` — spread pods across zones

### 4.5 Helm — The Kubernetes Package Manager
- What Helm solves: templating and packaging Kubernetes manifests
- Charts: `Chart.yaml`, `values.yaml`, `templates/`
- `helm install`, `upgrade`, `rollback`, `uninstall`, `list`
- `helm template` — render manifests locally without deploying
- `values.yaml` overrides: `helm install myapp ./chart -f prod-values.yaml`
- Writing your own Helm chart for an application
- Using community charts: Artifact Hub (nginx-ingress, cert-manager, prometheus)
- Helmfile — declarative management of multiple Helm releases

### 4.6 Kubernetes Networking
- Pod networking: every pod gets its own IP; pods communicate directly
- CNI plugins: Calico (network policy), Cilium (eBPF-based), Flannel
- Services: ClusterIP (internal), NodePort (node access), LoadBalancer (cloud LB)
- Ingress controllers: Nginx Ingress, Traefik, AWS ALB Ingress
- `cert-manager` — automatic TLS certificate management (Let's Encrypt integration)
- DNS in Kubernetes: `CoreDNS`, service discovery by name
- NetworkPolicies — default deny, explicit allow patterns

### 4.7 Kubernetes Security
- RBAC: least privilege for every ServiceAccount
- Pod Security Standards (PSS): Privileged, Baseline, Restricted
- `OPA/Gatekeeper` or `Kyverno` — policy enforcement in the cluster
- External Secrets Operator (ESO) — sync secrets from Vault/AWS Secrets Manager to Kubernetes
- Image pull secrets and private registries
- Network policies: default-deny all, explicit ingress/egress rules
- Runtime security: Falco — detect anomalous behavior at runtime
- Supply chain security: sign images with `cosign`, verify with admission webhooks

### 4.8 GitOps with Argo CD
- GitOps: Git is the single source of truth for cluster state
- Argo CD: continuously reconciles cluster state to Git
- Application definitions: `Application` CRD pointing to a Git repo + path
- Sync policies: manual vs automated with self-heal and pruning
- Multi-cluster management: one Argo CD instance managing many clusters
- App of Apps pattern — managing Argo CD applications declaratively
- `ApplicationSet` — generate applications dynamically
- Argo CD vs Flux v2 — comparison

### 📝 Exercises (Phase 4)
1. **From Compose to Kubernetes** — translate the `compose.yaml` from Phase 1 into Kubernetes Deployment, Service, ConfigMap, and Secret manifests
2. **Rolling Update Zero-Downtime** — deploy an app, then update its image; verify with `kubectl rollout status` that no requests were dropped (use `k6` to generate load during the rollout)
3. **HPA Under Load** — configure an HPA, run a load test with `k6`, watch the autoscaler add pods, then observe scale-down after load stops
4. **Helm Chart Authorship** — package an application into a Helm chart with configurable replicas, image tag, resource limits, and ingress; install it with different values files for dev and prod
5. **GitOps Sync** — set up Argo CD on a local cluster (kind or k3s); push a change to a Git repo and watch Argo CD automatically sync it to the cluster

### 🔨 Mini-Project 4: Production Kubernetes Platform
Deploy a complete production Kubernetes environment:
- **Cluster:** EKS (AWS) or GKE (GCP) provisioned with Terraform
- **Networking:** Nginx Ingress + `cert-manager` (Let's Encrypt TLS)
- **App deployment:** Helm chart for the Phase 1 application with dev/staging/prod values files
- **GitOps:** Argo CD managing all application deployments from Git
- **Secrets:** External Secrets Operator syncing from AWS Secrets Manager
- **Autoscaling:** HPA on CPU + VPA recommendations; Cluster Autoscaler for node scaling
- **Security:** Network policies (default deny), Pod Security Standards (restricted), Kyverno policies
- **Monitoring:** kube-prometheus-stack (Prometheus + Grafana + Alertmanager)
- **Runbook:** documented procedures for: rolling update, rollback, scaling, incident response

---

## 🔵 Phase 5 — Observability & Site Reliability Engineering
**Duration:** 4–5 weeks | **Goal:** See everything that happens in production; respond to incidents systematically

### 5.1 The Three Pillars of Observability
- **Metrics:** numeric measurements over time (what is happening)
- **Logs:** timestamped records of events (what happened)
- **Traces:** request flow across services (where time was spent)
- The difference between *monitoring* (watching dashboards) and *observability* (asking arbitrary questions about system behavior)
- Cardinality — why it matters for metrics and traces
- Sampling strategies for traces and logs

### 5.2 Metrics with Prometheus & Grafana
- Prometheus data model: metrics, labels, time series
- Metric types: Counter, Gauge, Histogram, Summary
- PromQL — Prometheus Query Language:
  ```promql
  # HTTP error rate
  rate(http_requests_total{status=~"5.."}[5m])
  / rate(http_requests_total[5m])

  # 95th percentile latency
  histogram_quantile(0.95,
    rate(http_request_duration_seconds_bucket[5m])
  )
  ```
- Exporters: `node_exporter`, `kube-state-metrics`, `blackbox_exporter`, application-level `/metrics` endpoints
- Instrumentation with `prometheus-client` (Python) — adding metrics to your own app
- **Grafana:**
  - Data sources: Prometheus, Loki, Tempo, CloudWatch
  - Dashboard design: signal-to-noise ratio, the USE and RED methods
  - Alerts from Grafana or Alertmanager
  - Provisioning dashboards as code (JSON models in Git)
- **Alertmanager:** routing, grouping, inhibition, silences, receivers (PagerDuty, Slack, email)

### 5.3 Logging with the ELK / Grafana Loki Stack
**Grafana Loki (recommended for Kubernetes):**
- Loki architecture: distributor, ingester, querier, storage
- `Promtail` — log shipping agent (sidecar or DaemonSet)
- LogQL — Loki query language (similar to PromQL):
  ```logql
  {namespace="production", app="api"} |= "ERROR"
    | json
    | line_format "{{.message}}"
  ```
- Structured logging: JSON logs are machine-parseable
- Log retention and storage optimization

**Elasticsearch + Kibana (ELK) — enterprise context:**
- Elasticsearch concepts: indices, shards, mappings
- Logstash / Filebeat — log shipping
- Kibana: Discover, dashboards, alerting

### 5.4 Distributed Tracing with OpenTelemetry & Tempo
- Why traces? Understanding latency in microservices
- OpenTelemetry (OTel) — the standard: SDK, Collector, OTLP protocol
- Instrumenting a Python/Node.js service with OTel auto-instrumentation
- `W3C TraceContext` — propagating trace IDs across services
- **Grafana Tempo** — distributed tracing backend
- Trace sampling: head-based vs tail-based
- Correlating logs, metrics, and traces in Grafana

### 5.5 SRE Practices
- **SLI (Service Level Indicator):** what you measure (e.g., request success rate)
- **SLO (Service Level Objective):** the target (e.g., 99.9% success over 30 days)
- **SLA (Service Level Agreement):** the contractual commitment to customers
- **Error Budget:** 100% - SLO; how much unreliability you are allowed
- Error budget policies: when to stop feature work and focus on reliability
- **Toil:** manual, repetitive, automatable work — measuring and eliminating it
- **Blameless post-mortems:** learning from incidents without finger-pointing
  - Post-mortem structure: timeline, root cause, contributing factors, action items
  - The 5 Whys technique
- **On-call best practices:** escalation policies, runbooks, alert fatigue reduction
- **Chaos Engineering:** intentionally injecting failures to find weaknesses
  - `Chaos Monkey` (Netflix)
  - `LitmusChaos` — Kubernetes-native chaos experiments
  - Game days — structured chaos experiments

### 5.6 Incident Management
- Incident severity levels: P0/P1/P2/P3 definitions
- Incident response workflow: detect → acknowledge → investigate → mitigate → resolve → review
- Runbooks — operational procedures for known failure modes
- War room / incident bridge communication
- Communication templates: status page updates, stakeholder notifications
- Tools: PagerDuty, OpsGenie, Incident.io

### 📝 Exercises (Phase 5)
1. **Instrument Your App** — add Prometheus metrics to the Phase 1 API: request count, error rate, and latency histogram; verify in a Grafana dashboard
2. **Alert Design** — write Alertmanager rules for: error rate > 1%, p95 latency > 500ms, pod restart count > 3; configure Slack notifications with runbook links
3. **Log Correlation** — inject a correlation ID into every log line; demonstrate tracing a single request across 3 services in Loki using the ID
4. **Write a Post-Mortem** — simulate an incident (e.g., wrong config deployed → 503s); write a full post-mortem document: timeline, root cause, 5 Whys, action items
5. **Chaos Experiment** — use LitmusChaos to kill a random pod in a namespace; verify that the HPA and deployment maintain availability; measure the impact on your SLO

### 🔨 Mini-Project 5: Full Observability Platform
Build a complete observability stack for the Kubernetes platform from Phase 4:
- **Metrics:** kube-prometheus-stack with custom app dashboards (USE method for infrastructure, RED method for services)
- **Logging:** Loki + Promtail; structured JSON logging in the application; log-based alerting
- **Tracing:** OpenTelemetry Collector + Tempo; traces visible and correlated with logs in Grafana
- **Alerting:** tiered alerts (warning/critical) with Alertmanager routing to Slack; all alerts link to runbooks
- **SLOs:** defined SLOs for the API (availability + latency); error budget dashboard
- **Synthetic monitoring:** `blackbox_exporter` probing all public endpoints every 30 seconds
- **Runbooks:** documented response procedures for every alert
- **Chaos validation:** LitmusChaos experiment that kills pods; SLO dashboard shows the impact stayed within budget

---

## 🟣 Phase 6 — Advanced Tracks
**Duration:** 6–8 weeks | **Choose based on your target role**

---

### 🏗️ Track A: Platform Engineering

**The emerging discipline:** building internal developer platforms (IDPs) that make application teams self-sufficient without compromising on standards.

#### Topics
- **Platform Engineering vs DevOps:** DevOps is the culture; Platform Engineering builds the paved roads
- **Internal Developer Platforms (IDP):** Port, Backstage (Spotify), Humanitec
- **Backstage** — open-source developer portal:
  - Software catalog: registering all services
  - Templates: self-service scaffolding for new services
  - TechDocs: centralized documentation
  - Plugins: integrating Kubernetes, Argo CD, PagerDuty, cost data
- **Developer Experience (DX) metrics:** SPACE framework (Satisfaction, Performance, Activity, Communication, Efficiency)
- **Golden Paths:** paved roads for common patterns (new service, new data pipeline, etc.)
- **Platform as a Product:** treating internal users as customers; collecting feedback; roadmaps
- **Multi-tenancy at platform level:** namespaces, network policies, quotas per team
- **Crossplane** — Kubernetes-native infrastructure provisioning (IaC inside k8s)
- **Cost visibility and chargeback:** Kubecost, OpenCost — per-team resource cost
- **Service mesh:** Istio or Linkerd — mTLS, traffic management, observability at the network layer

#### 🔨 Capstone A: Internal Developer Platform
Build a self-service developer platform:
- Backstage portal with software catalog for all Phase roadmap services
- Self-service template: developer fills a form → Backstage creates a GitHub repo with CI/CD, Kubernetes manifests, and Argo CD application pre-configured
- Crossplane compositions: one CRD (`Application`) abstracts EC2 + RDS + S3 + IAM into a single deployable unit
- Per-team Kubernetes namespaces with resource quotas and network policies
- Kubecost dashboard showing per-team and per-service cloud spend
- Istio service mesh: mTLS between all services, traffic splitting for canary releases
- Full golden path documented end-to-end: idea → deployed service in under 30 minutes

---

### 🔐 Track B: DevSecOps & Supply Chain Security

#### Topics
- **Shift-left security:** security is everyone's responsibility, starting at development
- **SAST (Static Application Security Testing):** Semgrep, Bandit (Python), SonarQube
- **DAST (Dynamic Application Security Testing):** OWASP ZAP, Burp Suite
- **Software Composition Analysis (SCA):** Dependabot, Snyk, OWASP Dependency-Check
- **Secret scanning:** `trufflehog`, `gitleaks` — catch secrets before they reach Git
- **Container image security:**
  - Minimal base images: `distroless`, `scratch`, `alpine`
  - Trivy, Grype, Syft — scanning and SBOM generation
  - Image signing with `cosign` and Sigstore
- **Supply Chain Levels for Software Artifacts (SLSA):**
  - SLSA levels 1–4: provenance, build platform integrity
  - Generating and verifying build provenance
- **Software Bill of Materials (SBOM):** generating with Syft; attaching to images; consuming with Grype
- **Policy enforcement in pipelines:** OPA + Conftest for SBOM and policy-as-code
- **Runtime security:** Falco rules for detecting container escapes, privilege escalation
- **Compliance as code:** SOC2, ISO 27001, PCI-DSS control mapping to pipeline checks
- **Vulnerability management program:** triage → prioritize → remediate → verify

#### 🔨 Capstone B: Secure Software Factory
Build an end-to-end secure software supply chain:
- Pre-commit hooks: `gitleaks` (secrets), `bandit` (SAST), `black`/`ruff` (lint)
- CI pipeline: SAST (Semgrep) → SCA (Snyk) → build → Trivy scan → SBOM generation (Syft) → image signing (cosign) → provenance attestation (SLSA level 2)
- Admission controller in Kubernetes: reject any image without a valid cosign signature
- Falco rules: alert on any container running as root, any shell spawned in a container, any outbound connection to unexpected IPs
- Monthly vulnerability report: scan all running images, triage findings by CVSS score, assign owners
- Policy dashboard: all services show their SLSA level, last scan date, and open CVE count
- Documented security runbook: respond to a critical CVE from detection to patched deploy in < 4 hours

---

## 📚 Curated Resources

### Essential Books
| Title | Level | Focus |
|-------|-------|-------|
| *The Phoenix Project* — Kim, Behr, Spafford | Beginner | DevOps culture (novel format) |
| *The DevOps Handbook* — Kim et al. | Beginner–Intermediate | Principles and practices |
| *Accelerate* — Forsgren, Humble, Kim | Intermediate | DORA metrics, scientific basis |
| *Site Reliability Engineering* — Google SRE Book | Intermediate–Advanced | SRE practices (free online) |
| *Kubernetes in Action* — Lukša | Intermediate | Deep Kubernetes understanding |
| *Terraform: Up and Running* — Brikman | Intermediate | Terraform mastery |
| *The Unicorn Project* — Kim | All | DevOps culture (novel format) |

### Online Platforms & Labs
- **KillerCoda** — free browser-based Kubernetes labs
- **KodeKloud** — hands-on DevOps labs (Docker, Kubernetes, Terraform, Ansible)
- **Kubernetes the Hard Way** (Kelsey Hightower) — build a cluster from scratch to understand every component
- **CNCF Landscape** (landscape.cncf.io) — map of the cloud-native ecosystem
- **Play with Kubernetes** — free in-browser cluster
- **Terraform Registry** — official module and provider documentation
- **Awesome DevOps** (GitHub) — curated community resource list

### Certifications (Industry-Recognized)
| Certification | Provider | Level | Value |
|--------------|----------|-------|-------|
| CKA (Certified Kubernetes Administrator) | CNCF | Intermediate | Very High |
| CKAD (Certified Kubernetes Application Developer) | CNCF | Intermediate | High |
| CKS (Certified Kubernetes Security Specialist) | CNCF | Advanced | Very High |
| AWS Solutions Architect Associate | AWS | Intermediate | High |
| AWS DevOps Engineer Professional | AWS | Advanced | Very High |
| HashiCorp Terraform Associate | HashiCorp | Intermediate | High |
| GitLab Certified CI/CD Associate | GitLab | Beginner | Medium |

---

## 🗓️ Recommended Study Schedule

| Phase | Commitment | Timeline |
|-------|-----------|----------|
| Phase 0: Foundations & Git | 1.5 hrs/day | Weeks 1–2 |
| Phase 1: Docker & Containers | 1.5–2 hrs/day | Weeks 3–7 |
| Phase 2: CI/CD Pipelines | 1.5–2 hrs/day | Weeks 8–13 |
| Phase 3: Infrastructure as Code | 2 hrs/day | Weeks 14–19 |
| Phase 4: Kubernetes | 2 hrs/day | Weeks 20–26 |
| Phase 5: Observability & SRE | 2 hrs/day | Weeks 27–31 |
| Phase 6: Specialization Track | 2 hrs/day | Weeks 32–40 |

> 💡 **Tip:** DevOps tools change fast; the principles do not. Invest deeply in understanding *why* before chasing every new tool. The engineer who understands why CI/CD matters will adopt any new pipeline tool in days.

---

## 🧠 DevOps Golden Rules (Internalize These)

1. **Everything as code** — if it's not in Git, it doesn't exist and can't be reviewed, tested, or rolled back
2. **Automate the second time** — the first time is learning; the second time, write the script
3. **Small, frequent changes** — large releases are dangerous; deploy often and reduce blast radius
4. **Build quality in, don't bolt it on** — tests, scans, and policies in the pipeline, not after
5. **Measure DORA metrics** — you cannot improve what you do not measure
6. **Blameless post-mortems** — systems fail; people learn; blame prevents learning
7. **Least privilege everywhere** — IAM roles, service accounts, network policies: deny by default
8. **Observability before features** — you cannot fix what you cannot see; instrument first
9. **Idempotency is non-negotiable** — every script, playbook, and pipeline must be safe to run twice
10. **Delete what you don't understand** — unused infrastructure, unknown firewall rules, and mystery scripts are liabilities

---

## ✅ Progress Tracker

- [ ] Phase 0 complete — Git mastered, environment ready
- [ ] Phase 1 complete — Containerized Microservices Application shipped
- [ ] Phase 2 complete — Full CI/CD Pipeline operational
- [ ] Phase 3 complete — Cloud Infrastructure Platform provisioned with Terraform
- [ ] Phase 4 complete — Production Kubernetes Platform running
- [ ] Phase 5 complete — Full Observability Platform with SLOs defined
- [ ] Phase 6 Track chosen: ___________
- [ ] Phase 6 Capstone complete — production-grade platform delivered

---

*Roadmap version 1.0 · Cloud-native · Kubernetes-first · Updated May 2026*