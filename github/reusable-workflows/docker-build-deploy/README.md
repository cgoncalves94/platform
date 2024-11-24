# Docker Build and Deploy Workflow

A reusable workflow for building Docker images and deploying them to various environments.

## Features

- Supports multiple container registries (Docker Hub, GHCR, AWS ECR)
- Environment-specific builds and deployments
- Kubernetes and Docker Compose deployment options
- Secure credentials handling
- Build caching and optimization

## Usage

```yaml
name: Deploy Application

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    uses: cgoncalves94/platform/.github/workflows/docker-build-deploy.yml@main
    with:
      environment: 'production'
      registry-type: 'ghcr'
      image-name: 'my-app'
      deploy-type: 'k8s'
    secrets:
      registry-username: ${{ secrets.REGISTRY_USERNAME }}
      registry-password: ${{ secrets.REGISTRY_PASSWORD }}
      deploy-token: ${{ secrets.DEPLOY_TOKEN }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `environment` | Environment to deploy to | Yes | - |
| `registry-type` | Container registry type | Yes | 'docker' |
| `image-name` | Name of the Docker image | Yes | - |
| `dockerfile-path` | Path to the Dockerfile | No | 'Dockerfile' |
| `deploy-type` | Deployment type | No | 'k8s' |

## Secrets

| Secret | Description | Required |
|--------|-------------|----------|
| `registry-username` | Registry username | Yes |
| `registry-password` | Registry password | Yes |
| `deploy-token` | Deployment token | Yes |

## Examples

### Deploy to Kubernetes
```yaml
jobs:
  deploy:
    uses: cgoncalves94/platform/.github/workflows/docker-build-deploy.yml@main
    with:
      environment: 'staging'
      registry-type: 'aws'
      image-name: 'backend-api'
      deploy-type: 'k8s'
    secrets:
      registry-username: ${{ secrets.AWS_ACCESS_KEY_ID }}
      registry-password: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      deploy-token: ${{ secrets.KUBECONFIG }}
```

### Deploy with Docker Compose
```yaml
jobs:
  deploy:
    uses: cgoncalves94/platform/.github/workflows/docker-build-deploy.yml@main
    with:
      environment: 'dev'
      registry-type: 'ghcr'
      image-name: 'frontend-app'
      deploy-type: 'compose'
    secrets:
      registry-username: ${{ secrets.GHCR_USER }}
      registry-password: ${{ secrets.GHCR_TOKEN }}
      deploy-token: ${{ secrets.DEPLOY_KEY }}
```
