# GitHub Actions Templates

This repository hosts reusable GitHub Actions workflow templates for common CI/CD tasks.

## Available Templates

### [S3 Static Website Deployment](./static-website/)

A reusable GitHub workflow for deploying static websites to Amazon S3.

**Features:**
- OIDC-based AWS role assumption (no AWS access keys required)
- Optional PR approval gating via GitHub environments
- Static website sync with configurable cache control
- Optional deletion of stale files

**Use this template to:**
- Deploy static websites, documentation sites, or front-end applications to S3
- Automate deployments on push to main branch
- Require approval before production deployments
- Manage cache headers for optimal performance

For detailed usage instructions, see the [S3 Static Website template README](./static-website/README.md).

## Getting Started

Each template includes:
- A reusable workflow definition (`.github/workflows/`)
- Documentation with usage examples
- Input parameters for customization

To use any template, reference it in your repository's workflow file.
