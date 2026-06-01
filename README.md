# GitHub Actions Templates

This repository hosts reusable GitHub Actions workflow templates for common CI/CD tasks.

## Available Templates

This repository groups reusable workflow templates under `.github/workflows/`.

**Workflows (standalone templates):** The `.github/workflows/` directory contains reusable workflow YAML files that can be called via `uses:`.

This repo currently contains:

- `.github/workflows/deploy-s3-static-site.yml` — reusable workflow for deploying static sites. See `.github/workflows/deploy-s3-static-site.md` for inputs, required secrets, and examples.

## Examples

Call the reusable S3 deploy workflow from another repository (remote reference):

```yaml
jobs:
	deploy:
		uses: owner/repo/.github/workflows/deploy-s3-static-site.yml@main
		secrets:
			AWS_ROLE_ARN: ${{ secrets.AWS_ROLE_ARN }}
			AWS_REGION: ${{ secrets.AWS_REGION }}
			S3_BUCKET_NAME: ${{ secrets.S3_BUCKET_NAME }}
		with:
			source_dir: 'public'
```

## Getting Started

This repository currently contains standalone workflow templates under `.github/workflows/`.

To add a new workflow template:
- create a new subfolder under `.github/workflows/` for template documentation and supporting files
- add one or more reusable workflow files directly under `.github/workflows/` and a README for inputs, secrets, and examples
- call the workflow from another repo or from a local workflow using `uses:`
