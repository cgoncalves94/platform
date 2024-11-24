# Docker Build and Push Action

A composite action that builds and pushes Docker images to any container registry.

## Features

- Generates unique image tags using commit SHA and timestamp
- Supports environment-specific Dockerfiles
- Works with any container registry
- Provides image URI and tag as outputs

## Usage

```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/docker-build-and-push@main
    with:
      environment: 'prod'
      registry_url: 'registry.example.com'
      image_name: 'my-app'
```

## Inputs

| Input | Description | Required |
|-------|-------------|----------|
| `environment` | Environment to build for (e.g., dev, staging, prod) | Yes |
| `registry_url` | URL of the container registry | Yes |
| `image_name` | Name of the image to build and push | Yes |

## Outputs

| Output | Description |
|--------|-------------|
| `image_uri` | Full URI of the pushed image |
| `image_tag` | Tag of the pushed image |

## Requirements

- Docker must be installed and configured
- Authentication to the container registry must be handled separately
- Environment-specific Dockerfiles must follow the naming pattern: `Dockerfile.<environment>`

## Example

```yaml
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      - name: Login to registry
        uses: docker/login-action@v3
        with:
          registry: registry.example.com
          username: ${{ secrets.REGISTRY_USERNAME }}
          password: ${{ secrets.REGISTRY_PASSWORD }}

      - name: Build and push
        uses: cgoncalves94/platform/github/composite-actions/docker-build-and-push@main
        with:
          environment: 'prod'
          registry_url: 'registry.example.com'
          image_name: 'my-app'
```
