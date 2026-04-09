# DevOps-Ready Task Management API

A RESTful task management API built with FastAPI and PostgreSQL, containerized with Docker, orchestrated with Kubernetes, and deployed via an automated Jenkins CI/CD pipeline. Infrastructure is provisioned on AWS using Terraform.

---

## Tech Stack

| Category | Technology |
|---|---|
| **Backend** | Python, FastAPI, SQLAlchemy |
| **Database** | PostgreSQL, Alembic migrations |
| **Containerization** | Docker, Docker Compose, Nginx |
| **Orchestration** | Kubernetes |
| **CI/CD** | Jenkins |
| **Infrastructure** | Terraform (AWS) |

---

## Features

- CRUD operations for task management
- Database migrations with Alembic
- Containerized with Docker and Docker Compose
- Nginx as reverse proxy
- Kubernetes manifests for production deployment
- Automated CI/CD pipeline with Jenkins
- AWS infrastructure provisioned via Terraform

---

## Project Structure

```
fastapi-backend/
├── app/
│   ├── main.py          # FastAPI application entry point
│   ├── models.py        # SQLAlchemy models
│   ├── schemas.py       # Pydantic schemas
│   ├── crud.py          # Database operations
│   └── database.py      # Database connection
├── alembic/             # Database migrations
├── k8s/                 # Kubernetes manifests
│   ├── fastapi-deployment.yaml
│   ├── fastapi-service.yaml
│   ├── fastapi-configmap.yaml
│   ├── ingress.yaml
│   ├── migration-job.yaml
│   ├── postgres-deployment.yaml
│   ├── postgres-service.yaml
│   └── postgres-secret.yaml
├── terraform/           # AWS infrastructure as code
├── nginx/               # Nginx reverse proxy config
├── Dockerfile
├── Dockerfile.jenkins
├── jenkinsfile
└── docker-compose.yml
```

---

## Quick Start (Local)

### Prerequisites

- Docker and Docker Compose

### 1. Clone the repository

```bash
git clone https://github.com/dimashabdyken/fastapi-backend.git
cd fastapi-backend
```

### 2. Set up environment variables

```bash
cp .env.example .env
```

```env
DATABASE_URL=postgresql://postgres:password@db:5432/taskdb
```

### 3. Start the stack

```bash
docker compose up -d
```

### 4. Run database migrations

```bash
docker compose exec app alembic upgrade head
```

### 5. Access the API

- API docs (Swagger): http://localhost:8000/docs

---

## API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| GET | `/tasks` | List all tasks |
| GET | `/tasks/{id}` | Get task by ID |
| POST | `/tasks` | Create a new task |
| PUT | `/tasks/{id}` | Update a task |
| DELETE | `/tasks/{id}` | Delete a task |

---

## Kubernetes Deployment

The `k8s/` directory contains all manifests for production deployment:

- FastAPI app deployment with configmap
- PostgreSQL deployment with persistent storage and secrets
- Nginx ingress for external traffic routing
- Migration job for automated schema updates on deploy

```bash
kubectl apply -f k8s/
```

---

## CI/CD Pipeline (Jenkins)

The `jenkinsfile` defines an automated pipeline that runs on every push:

1. Build Docker image
2. Run tests
3. Push image to registry
4. Deploy to Kubernetes cluster

Jenkins runs in its own Docker container defined in `Dockerfile.jenkins`.

---

## AWS Infrastructure (Terraform)

The `terraform/` directory provisions the required AWS infrastructure:

```bash
cd terraform
terraform init
terraform plan
terraform apply
```

---

