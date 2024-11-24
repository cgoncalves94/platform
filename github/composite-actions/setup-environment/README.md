# Setup Environment Action

A composite action that sets up development environments with proper caching for multiple programming languages.

## Features

- Supports Node.js, Python, and Java
- Automatic dependency caching
- Configurable versions
- Language-specific optimizations

## Usage

```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/setup-environment@main
    with:
      node-version: '18'
      python-version: '3.11'
      java-version: '17'
      cache: 'true'
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `node-version` | Node.js version to use | No | '' |
| `python-version` | Python version to use | No | '' |
| `java-version` | Java version to use | No | '' |
| `cache` | Enable dependency caching | No | 'true' |

## Caching Details

- **Node.js**: Caches `node_modules` based on `package-lock.json`
- **Python**: Caches pip packages based on `requirements.txt`
- **Java**: Caches Maven dependencies

## Examples

### Node.js Only
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/setup-environment@main
    with:
      node-version: '18'
```

### Python Only
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/setup-environment@main
    with:
      python-version: '3.11'
```

### Multiple Languages
```yaml
steps:
  - uses: cgoncalves94/platform/github/composite-actions/setup-environment@main
    with:
      node-version: '18'
      python-version: '3.11'
      java-version: '17'
```
