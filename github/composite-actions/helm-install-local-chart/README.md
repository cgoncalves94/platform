# Helm Install Local Chart Action

A composite action that installs or upgrades a Helm chart for local development environments.

## Features

- Installs or upgrades Helm charts
- Creates namespace if it doesn't exist
- Supports custom values files and set values
- Automatically adds required Helm repositories
- Verifies deployment success

## Usage

```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/helm-install-local-chart@main
    with:
      cluster_name: 'my-cluster'
      chart_path: './charts/my-app'
      release_name: 'my-release'
      namespace: 'my-namespace'
      values_file: './values.yaml'
      set_values: 'image.tag=latest,replicas=2'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `cluster_name` | Name of the Kubernetes cluster | Yes | - |
| `chart_path` | Path to the Helm chart | Yes | - |
| `release_name` | Name of the Helm release | Yes | - |
| `namespace` | Kubernetes namespace | No | 'default' |
| `values_file` | Path to values file | No | - |
| `set_values` | Additional values (key=value pairs) | No | - |
| `timeout` | Timeout for Helm operations | No | '5m' |

## Requirements

- Kubernetes cluster configured
- kubectl installed and configured
- Helm 3.x will be installed if not present

## Repository Configuration

Create a `repositories.txt` file in your chart directory to automatically add required Helm repositories:

```text
bitnami=https://charts.bitnami.com/bitnami
jetstack=https://charts.jetstack.io
```

## Examples

### Basic Installation
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/helm-install-local-chart@main
    with:
      cluster_name: 'dev-cluster'
      chart_path: './charts/app'
      release_name: 'my-app'
      namespace: 'development'
```

### Custom Values and Settings
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/helm-install-local-chart@main
    with:
      cluster_name: 'prod-cluster'
      chart_path: './charts/app'
      release_name: 'my-app'
      namespace: 'production'
      values_file: './values.prod.yaml'
      set_values: 'image.tag=v1.0.0,ingress.enabled=true'
      timeout: '10m'
```
