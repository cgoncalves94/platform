## Platform Workflows
![GitHub stars](https://img.shields.io/github/stars/cgoncalves94/platform?style=social)
![GitHub forks](https://img.shields.io/github/forks/cgoncalves94/platform?style=social)
![GitHub issues](https://img.shields.io/github/issues/cgoncalves94/platform)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](./LICENSE)
[![Pre-commit hooks status](https://github.com/cgoncalves94/platform/workflows/Pre-commit%20Hooks/badge.svg)](https://github.com/cgoncalves94/platform/actions)

A collection of reusable workflows and composite actions for standardizing CI/CD processes across repositories.

## Structure

```
.
├── .github/
│   ├── workflows/
│   │   └──  pre-commit-hooks.yml
│   ├── CODEOWNERS
├── github/
│   ├── composite-actions/
│   │   ├── aws-configure/
│   │   ├── docker-build-and-push/
│   │   ├── helm-install-local-chart/
│   │   └── setup-environment/
│   └── reusable-workflows/
│       ├── aws-build-push/
│       ├── docker-build-deploy/
│       └── node-build-test/
└── README.md
```

## Available Components

### Composite Actions

1. **aws-configure**
   - Configures AWS credentials and authenticates to ECR
   - Creates AWS profile and sets up environment
   - [Documentation](github/composite-actions/aws-configure/README.md)

2. **docker-build-and-push**
   - Builds and pushes Docker images to any container registry
   - Supports multiple environments and registries
   - [Documentation](github/composite-actions/docker-build-and-push/README.md)

3. **helm-install-local-chart**
   - Installs Helm charts for local development
   - Configures Kubernetes deployments
   - [Documentation](github/composite-actions/helm-install-local-chart/README.md)

4. **setup-environment**
   - Sets up build environment with caching
   - Configures language-specific tools (Node.js, Python, Java)
   - [Documentation](github/composite-actions/setup-environment/README.md)

### Reusable Workflows

1. **aws-build-push**
   - Complete workflow for AWS deployments
   - Includes ECR push and EKS deployment
   - [Documentation](github/reusable-workflows/aws-build-push/README.md)

2. **docker-build-deploy**
   - Complete workflow for Docker-based applications
   - Supports multiple deployment targets
   - [Documentation](github/reusable-workflows/docker-build-deploy/README.md)

3. **node-build-test**
   - Builds and tests Node.js applications
   - Includes caching and parallel testing
   - [Documentation](github/reusable-workflows/node-build-test/README.md)

## Usage

1. Reference composite actions:
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/docker-build-and-push@main
    with:
      registry_url: ${{ inputs.registry_url }}
      image_name: my-app
```

2. Call reusable workflows:
```yaml
jobs:
  deploy:
    uses: cgoncalves94/platform/.github/workflows/aws-build-push.yml@main
    with:
      environment: production
      registry-type: aws
      image-name: my-app
    secrets:
      aws-access-key: ${{ secrets.AWS_ACCESS_KEY }}
      aws-secret-key: ${{ secrets.AWS_SECRET_KEY }}
```

## Contributing

1. Create a new branch for your changes
2. Follow the existing structure and naming conventions
3. Include documentation and examples
4. Submit a PR with a clear description of the changes

## License

MIT License - See [LICENSE](LICENSE) for details
