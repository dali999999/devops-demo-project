# DevOps CI/CD Pipeline — Mohamed Ali Jaouadi

A complete DevOps pipeline built locally using industry-standard tools, automating the full lifecycle of a Java Spring Boot application from source code to Kubernetes deployment.

## Architecture
GitHub → Jenkins → Maven → SonarQube → Docker → DockerHub → ArgoCD → Helm → Kubernetes (Minikube)

## Tools & Technologies

| Category         | Tools                           |
|------------------|---------------------------------|
| CI/CD            | Jenkins, GitHub Actions         |
| Code Quality     | SonarQube, Maven                |
| Containerization | Docker, DockerHub               |
| Orchestration    | Kubernetes (Minikube), Helm     |
| GitOps           | ArgoCD                          |
| Auto-scaling     | HPA, Metrics Server             |
| Environment      | WSL2, Ubuntu                    |

## Project Structure
stage-ete/
├── .github/
│   └── workflows/
│       └── notify_on_push.yml       # Email notification on push
├── ci/
│   ├── docker-compose.yml           # Jenkins + SonarQube services
│   └── Jenkins/
│       ├── Dockerfile               # Custom Jenkins image (Docker + Maven)
│       └── Jenkinsfile              # CI pipeline definition
├── cd/
│   └── argocd/
│       └── argocd-basic.yaml        # ArgoCD Application manifest
├── demo-java-app/                   # Spring Boot application
│   ├── Dockerfile                   # Multi-stage build (Java 17)
│   ├── pom.xml
│   └── src/
└── helm/
└── app/                         # Helm chart for Kubernetes deployment
├── Chart.yaml
├── values.yaml
└── templates/
├── deployment.yaml
├── service.yaml
└── hpa.yaml             # Horizontal Pod Autoscaler

## Pipeline Stages

1. **Checkout** — Pull source code from GitHub
2. **Build & Test** — Compile with Maven, run unit tests
3. **Static Code Analysis** — SonarQube quality gate check
4. **Docker Build & Push** — Build image and push to DockerHub
5. **Update Helm Values** — Jenkins updates image tag in `values.yaml`
6. **GitOps Sync** — ArgoCD detects the change and deploys to Kubernetes

## Getting Started

### Prerequisites

- Docker & Docker Compose
- WSL2 (Ubuntu)
- Minikube
- kubectl & Helm

### Run the CI Environment

```bash
cd ci
docker-compose up -d
```

- Jenkins → `http://localhost:8010`
- SonarQube → `http://localhost:9000`

### Deploy to Kubernetes

```bash
helm install demo-app helm/app/
```

### Access ArgoCD

```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```

ArgoCD UI → `https://localhost:8080`

## Credits

Based on the original project by [@deepakkr35](https://github.com/deepakkr35/devops-demo-project), extended and adapted as part of a summer internship.

## Author

**Mohamed Ali Jaouadi**
GitHub: [@dali999999](https://github.com/dali999999)

## License

This project is licensed under the [MIT License](LICENSE).
