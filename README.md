# GitHub Actions Templates

This repository hosts reusable GitHub Actions workflow templates for common CI/CD tasks.

## Available Templates

This repository groups reusable workflow-templates and template source folders.

**Workflows (standalone templates):** The `.github/workflows/` directory groups standalone workflow-templates — each subfolder is an independent reusable template you can call via `uses:`.

Examples of template subfolders:

- `.github/workflows/static-site/`
- `.github/workflows/terraform/`

This repo currently contains:

- `.github/workflows/static-site/` — reusable workflows and helpers for deploying static sites (S3 deploy workflow is provided).

See the README inside each workflow subfolder for inputs, required secrets, and examples (for example, `.github/workflows/static-site/README.md`).

## Examples

Call the reusable S3 deploy workflow from another repository (remote reference):

```yaml
jobs:
	deploy:
		uses: owner/repo/.github/workflows/static-site/deploy-s3-static-site.yml@main
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
- create a new subfolder under `.github/workflows/`
- add one or more reusable workflow files and a README for inputs, secrets, and examples
- call the workflow from another repo or from a local workflow using `uses:`
