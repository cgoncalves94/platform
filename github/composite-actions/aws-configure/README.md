# AWS Configure Action

A composite action that configures AWS credentials, authenticates with ECR, and optionally sets up EKS access.

## Features

- Configures AWS credentials
- Authenticates with Amazon ECR
- Sets up kubectl for EKS (optional)
- Provides ECR registry URL as output

## Usage

```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/aws-configure@main
    with:
      aws-access-key: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws-region: eu-west-1
      eks-cluster: my-cluster
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `aws-access-key` | AWS Access Key ID | Yes | - |
| `aws-secret-key` | AWS Secret Access Key | Yes | - |
| `aws-region` | AWS region | No | eu-west-1 |
| `eks-cluster` | EKS cluster name | No | - |

## Outputs

| Output | Description |
|--------|-------------|
| `registry_url` | The URL of the ECR registry |

## Requirements

- AWS credentials with appropriate permissions
- Docker installed (for ECR authentication)
- kubectl installed (for EKS configuration)

## Example

### Basic Usage with ECR
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/aws-configure@main
    with:
      aws-access-key: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws-region: eu-west-1
```

### Complete Setup with EKS
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/aws-configure@main
    with:
      aws-access-key: ${{ secrets.AWS_ACCESS_KEY_ID }}
      aws-secret-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
      aws-region: eu-west-1
      eks-cluster: production-cluster
```
