# AWS Build and Push Workflow

A reusable workflow for building Docker images and pushing them to Amazon ECR.

## Features

- AWS credentials configuration
- IAM role assumption (optional)
- ECR authentication
- Docker build with caching
- Automatic image tagging
- Build arguments support
- Environment-specific builds

## Usage

```yaml
name: Deploy to AWS

on:
  push:
    branches: [ main ]

jobs:
  deploy:
    uses: cgoncalves94/platform/.github/workflows/aws-build-push.yml@main
    with:
      environment: 'production'
      aws-region: 'eu-west-1'
      image-name: 'my-app'
    secrets:
      aws-access-key: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws-role-arn: ${{ secrets.AWS_ROLE_ARN }}
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `environment` | Environment to deploy to | Yes | - |
| `aws-region` | AWS region | No | 'eu-west-1' |
| `image-name` | Name of the Docker image | Yes | - |
| `dockerfile` | Path to Dockerfile | No | 'Dockerfile' |
| `build-args` | Build arguments as JSON | No | '{}' |

## Secrets

| Secret | Description | Required |
|--------|-------------|----------|
| `aws-access-key` | AWS Access Key ID | Yes |
| `aws-secret-key` | AWS Secret Access Key | Yes |
| `aws-role-arn` | AWS IAM Role ARN | No |

## Examples

### Basic Usage
```yaml
jobs:
  deploy:
    uses: cgoncalves94/platform/.github/workflows/aws-build-push.yml@main
    with:
      environment: 'staging'
      image-name: 'backend-api'
    secrets:
      aws-access-key: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

### Advanced Configuration
```yaml
jobs:
  deploy:
    uses: cgoncalves94/platform/.github/workflows/aws-build-push.yml@main
    with:
      environment: 'production'
      aws-region: 'us-east-1'
      image-name: 'backend-api'
      dockerfile: 'Dockerfile.prod'
      build-args: '{"NODE_ENV": "production", "API_URL": "https://api.example.com"}'
    secrets:
      aws-access-key: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws-role-arn: ${{ secrets.PROD_ROLE_ARN }}
```

### Multiple Environments
```yaml
jobs:
  staging:
    uses: cgoncalves94/platform/.github/workflows/aws-build-push.yml@main
    with:
      environment: 'staging'
      image-name: 'my-app'
    secrets:
      aws-access-key: ${{ secrets.STAGING_AWS_KEY }}
      aws-secret-key: ${{ secrets.STAGING_AWS_SECRET }}

  production:
    needs: staging
    uses: cgoncalves94/platform/.github/workflows/aws-build-push.yml@main
    with:
      environment: 'production'
      image-name: 'my-app'
    secrets:
      aws-access-key: ${{ secrets.PROD_AWS_KEY }}
      aws-secret-key: ${{ secrets.PROD_AWS_SECRET }}
      aws-role-arn: ${{ secrets.PROD_ROLE_ARN }}
```
