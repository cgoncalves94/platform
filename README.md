# Platform Workflows

A collection of reusable workflows and composite actions for standardizing CI/CD processes across repositories.

## Structure

```
.
├── .github/
│   ├── workflows/           # Example workflows showing how to use the reusable components
│   └── CODEOWNERS
├── github/
│   ├── composite-actions/   # Composite actions that can be used in workflows
│   └── reusable-workflows/  # Reusable workflows that can be shared across repos
├── docs/                    # Documentation for workflows and actions
└── README.md
```

## Available Components

### Composite Actions

1. **docker-build-and-push**
   - Builds and pushes Docker images to any container registry
   - Supports multiple environments and registries
   - [Documentation](github/composite-actions/docker-build-and-push/README.md)

2. **setup-environment**
   - Sets up build environment with caching
   - Configures language-specific tools (Node.js, Python, etc.)
   - [Documentation](github/composite-actions/setup-environment/README.md)

### Reusable Workflows

1. **node-build-test**
   - Builds and tests Node.js applications
   - Includes caching and parallel testing
   - [Documentation](github/reusable-workflows/node-build-test/README.md)

2. **docker-build-deploy**
   - Complete workflow for Docker-based applications
   - Supports multiple deployment targets
   - [Documentation](github/reusable-workflows/docker-build-deploy/README.md)

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
  build:
    uses: cgoncalves94/platform/.github/workflows/node-build-test.yml@main
    with:
      node-version: '18'
```

## Contributing

1. Create a new branch for your changes
2. Follow the existing structure and naming conventions
3. Include documentation and examples
4. Submit a PR with a clear description of the changes

## License

MIT License - See [LICENSE](LICENSE) for details
