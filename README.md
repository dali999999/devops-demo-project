# DevOps CI/CD Pipeline — Mohamed Ali Jaouadi

A complete DevOps pipeline built locally using industry-standard tools, automating the full lifecycle of a Java Spring Boot application from source code to Kubernetes deployment.

## Architecture
GitHub → Jenkins → Maven → SonarQube → Docker → DockerHub → Helm → Kubernetes (Minikube) → ArgoCD

## Tools & Technologies

| Category | Tools |
|---|---|
| CI/CD | Jenkins, GitHub Actions |
| Code Quality | SonarQube |
| Build | Maven |
| Containerization | Docker, DockerHub |
| Orchestration | Kubernetes, Minikube, Helm |
| GitOps | ArgoCD |
| Auto-scaling | HPA, Metrics Server |
| Environment | WSL2, Ubuntu |

## Project Structure
devops-demo-project/
├── ci/
│   └── Jenkins/
│       ├── Dockerfile        # Custom Jenkins image with Docker & Maven
│       ├── Jenkinsfile       # CI/CD pipeline definition
│       └── docker-compose.yaml
├── cd/
│   └── argocd/
│       └── argocd-basic.yaml # ArgoCD configuration
├── demo-java-app/            # Spring Boot application
│   ├── Dockerfile
│   ├── pom.xml
│   └── src/
└── helm/
└── app/                  # Helm chart for Kubernetes deployment

## Pipeline Stages

1. **Checkout** — Pull source code from GitHub
2. **Build & Test** — Compile with Maven, run tests
3. **Static Code Analysis** — SonarQube quality gates
4. **Docker Build & Push** — Build image, push to DockerHub
5. **Update Helm Values** — Update image tag in values.yaml
6. **GitOps Sync** — ArgoCD detects change, deploys to Kubernetes

## Getting Started

### Prerequisites
- Docker & Docker Compose
- WSL2 (Ubuntu)
- Minikube
- kubectl & Helm
- ArgoCD

### Run CI Environment

```bash
cd ci
docker-compose up -d
```

Jenkins will be available at `http://localhost:8010`
SonarQube will be available at `http://localhost:9000`

### Deploy to Kubernetes

```bash
helm install demo-app helm/app/
```

## Author

**Mohamed Ali Jaouadi**
GitHub: [@dali999999](https://github.com/dali999999)
