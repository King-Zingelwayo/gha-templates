# Reusable GitHub Action: Deploy S3 Static Website

## Purpose

This repository includes a reusable GitHub workflow for deploying a static website to Amazon S3.
It supports:
- OIDC-based AWS role assumption
- Optional PR approval gating via GitHub environments
- Static website sync with cache-control and optional deletion of stale files

## Usage Examples

### Without PR Approval

For automatic deployment on every push to main:

```yaml
name: Deploy Static Website

on:
  push:
    branches:
      - main

jobs:
  deploy:
    uses: owner/repo/static-website/.github/workflows/deploy-s3-static-site.yml@main
    secrets:
      AWS_ROLE_ARN: 'arn:aws:iam::123456789012:role/github-actions-oidc'
      AWS_REGION: 'us-east-1'
      S3_BUCKET_NAME: 'my-static-site-bucket'
    with:
      source_dir: 'public'
      cache_control: 'max-age=31536000,public'
      delete_remote: 'false'
      pr_approval_required: 'false'
```

### With PR Approval

For approval-gated deployments (requires reviewers on the `production` environment):

```yaml
name: Deploy Static Website

on:
  push:
    branches:
      - main

jobs:
  deploy:
    uses: owner/repo/static-website/.github/workflows/deploy-s3-static-site.yml@main
    environment: production
    secrets:
      AWS_ROLE_ARN: 'arn:aws:iam::123456789012:role/github-actions-oidc'
      AWS_REGION: 'us-east-1'
      S3_BUCKET_NAME: 'my-static-site-bucket'
    with:
      source_dir: 'public'
      cache_control: 'max-age=31536000,public'
      delete_remote: 'false'
      pr_approval_required: 'true'
      deployment_environment: 'production'
```

**Note:** When using PR approval, add `environment: production` to your job and configure required reviewers on the GitHub environment.

### Local Usage

If you want to use the workflow within the same repository, refer to the local path instead:

```yaml
uses: ./.github/workflows/deploy-s3-static-site.yml
```

## Secrets Configuration

The following secrets must be configured in your GitHub repository:

- `AWS_ROLE_ARN`: AWS role ARN to assume when using GitHub OIDC
- `AWS_REGION`: AWS region for the target bucket
- `S3_BUCKET_NAME`: Target S3 bucket name

## Notes

- This workflow is fully OIDC-only and does not use AWS access keys.
- You must configure the AWS role trust policy for GitHub OIDC.
- If `pr_approval_required` is `true`, set `deployment_environment` to a GitHub environment that has required reviewers configured.
