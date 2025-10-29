# Shared Pipeline Repository

A centralized repository for reusable GitHub Actions workflows that implement DevSecOps practices across multiple projects.

## Overview

This repository contains reusable CI/CD workflows that can be referenced by other projects to ensure consistent security scanning, code quality checks, and deployment practices across all repositories in the organization.

## Repository Structure

```
shared-pipeline/
├── .github/workflows/          # Reusable workflow templates
│   ├── security-scan.yml       # Comprehensive security scanning
│   ├── docker-build.yml        # Docker image building with security
│   ├── k8s-deploy.yml          # Kubernetes deployment validation
│   ├── terraform-plan.yml      # Infrastructure validation
│   ├── docs-build.yml          # Documentation building
│   └── release.yml             # Release automation
├── templates/                   # Pipeline templates
│   ├── security-template.yml
│   ├── docker-template.yml
│   └── k8s-template.yml
├── scripts/                     # Shared scripts
│   ├── security-scan.sh
│   ├── docker-build.sh
│   └── k8s-deploy.sh
├── configs/                     # Configuration files
│   ├── .gitleaks.toml
│   ├── .secrets.baseline
│   └── security-policies.yml
└── docs/                        # Documentation
    ├── usage.md
    ├── examples.md
    └── migration.md
```

## Available Workflows

### 🔒 **Security Scan Workflow**
- **File**: `security-scan.yml`
- **Purpose**: Comprehensive security scanning across all project types
- **Tools**: TruffleHog, GitLeaks, detect-secrets, Bandit, Safety
- **Usage**: Reference in any project for security validation

### 🐳 **Docker Build Workflow**
- **File**: `docker-build.yml`
- **Purpose**: Secure Docker image building with Hadolint validation
- **Tools**: Hadolint, Docker Buildx, Trivy scanning
- **Usage**: Build and scan Docker images with security best practices

### ☸️ **Kubernetes Deploy Workflow**
- **File**: `k8s-deploy.yml`
- **Purpose**: Kubernetes manifest validation and deployment
- **Tools**: kubeval, kube-score, Helm linting
- **Usage**: Validate and deploy Kubernetes configurations

### 🏗️ **Terraform Plan Workflow**
- **File**: `terraform-plan.yml`
- **Purpose**: Infrastructure validation and planning
- **Tools**: tflint, terraform fmt, terraform plan
- **Usage**: Validate Terraform configurations before deployment

### 📚 **Documentation Build Workflow**
- **File**: `docs-build.yml`
- **Purpose**: Documentation building and validation
- **Tools**: MkDocs, markdownlint, linkchecker
- **Usage**: Build and validate documentation sites

## Quick Start

### 1. **Reference Security Scan**
```yaml
# In your project's .github/workflows/ci.yml
name: CI Pipeline
on: [push, pull_request]

jobs:
  security:
    uses: koriwayne/shared-pipeline/.github/workflows/security-scan.yml@v1.0.0
    with:
      scan-type: 'full'
      fail-on-high: 'true'
```

### 2. **Reference Docker Build**
```yaml
jobs:
  docker-build:
    uses: koriwayne/shared-pipeline/.github/workflows/docker-build.yml@v1.0.0
    with:
      dockerfile: './Dockerfile'
      image-name: 'my-app'
      registry: 'ghcr.io'
```

### 3. **Reference Kubernetes Deploy**
```yaml
jobs:
  k8s-deploy:
    uses: koriwayne/shared-pipeline/.github/workflows/k8s-deploy.yml@v1.0.0
    with:
      k8s-files: './k8s'
      namespace: 'production'
```

## Version Management

This repository uses semantic versioning for workflow releases:

- **v1.0.0** - Initial release with core workflows
- **v1.1.0** - Added new features (backward compatible)
- **v2.0.0** - Breaking changes (requires updates)

### **Pinning Versions**
Always pin to specific versions in your project workflows:
```yaml
# ✅ Good - Pinned version
uses: koriwayne/shared-pipeline/.github/workflows/security-scan.yml@v1.0.0

# ❌ Bad - Unpinned version
uses: koriwayne/shared-pipeline/.github/workflows/security-scan.yml@main
```

## Security Features

### **Secrets Detection**
- **TruffleHog OSS**: Scans for hardcoded secrets
- **GitLeaks**: Detects secrets in git history
- **detect-secrets**: Baseline-based detection

### **Code Quality**
- **Black**: Python code formatting
- **isort**: Import statement sorting
- **Flake8**: Python linting
- **MyPy**: Static type checking
- **Bandit**: Security linting

### **Infrastructure Security**
- **Hadolint**: Dockerfile security
- **kubeval**: Kubernetes validation
- **kube-score**: K8s security scoring
- **tflint**: Terraform linting

## Contributing

### **Adding New Workflows**
1. Create workflow file in `.github/workflows/`
2. Add comprehensive documentation
3. Test with multiple project types
4. Tag new version
5. Update usage examples

### **Updating Existing Workflows**
1. Make changes in feature branch
2. Test thoroughly
3. Update version number
4. Create pull request
5. Tag new release

## Documentation

- **[Usage Guide](docs/usage.md)** - How to use shared workflows
- **[Examples](docs/examples.md)** - Real-world usage examples
- **[Migration Guide](docs/migration.md)** - Migrating from project-specific workflows

## License

This project is open source and available under the [MIT License](LICENSE).

## Support

For questions or issues:
- **GitHub Issues**: Create an issue in this repository
- **Documentation**: Check the docs/ directory
- **Examples**: See the examples/ directory for usage patterns