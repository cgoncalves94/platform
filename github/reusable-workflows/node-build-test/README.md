# Node.js Build and Test Workflow

A reusable workflow for building and testing Node.js applications with comprehensive checks and coverage reporting.

## Features

- Flexible Node.js version selection
- Automatic dependency caching
- Linting (if configured)
- Type checking (if configured)
- Test execution with customizable commands
- Coverage reporting
- Artifact upload for test results

## Usage

```yaml
name: CI

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    uses: cgoncalves94/platform/.github/workflows/node-build-test.yml@main
    with:
      node-version: '18'
      working-directory: '.'
      test-command: 'npm run test:coverage'
      coverage-enabled: true
```

## Inputs

| Input | Description | Required | Default |
|-------|-------------|----------|---------|
| `node-version` | Node.js version to use | No | '18' |
| `working-directory` | Directory containing package.json | No | '.' |
| `test-command` | Custom test command | No | 'npm test' |
| `coverage-enabled` | Enable coverage reporting | No | true |

## Outputs

| Output | Description |
|--------|-------------|
| `tests-passed` | Boolean indicating whether all tests passed |

## Requirements

- `package.json` in the specified working directory
- Optional but recommended:
  - `lint` script for linting
  - `typecheck` script for type checking
  - Test coverage configuration

## Examples

### Basic Usage
```yaml
jobs:
  test:
    uses: cgoncalves94/platform/.github/workflows/node-build-test.yml@main
```

### Custom Configuration
```yaml
jobs:
  test:
    uses: cgoncalves94/platform/.github/workflows/node-build-test.yml@main
    with:
      node-version: '20'
      working-directory: 'packages/core'
      test-command: 'npm run test:ci'
      coverage-enabled: true
```
