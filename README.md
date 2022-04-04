# OpenID Connect to authenticate with AWS
OpenID Connect within your workflows to authenticate with AWS.

## Overview
OpenID Connect (OIDC) allows your GitHub Actions workflows to access resources in Amazon Web Services (AWS), without needing to store the AWS credentials as long-lived GitHub secrets.

```
name: AWS workflow
on:
  push
env:
  AWS_REGION : "eu-central-1" 
permissions:
  id-token: write
  contents: read
jobs:
  AWSAuth:
    runs-on: ubuntu-latest
    steps:
      - name: Git clone the repository
        uses: actions/checkout@v3
      - name: Configure AWS credentials
        uses: aws-actions/configure-aws-credentials@v1
        with:
          role-to-assume: ${{ secrets.ROLE_ARN }}
          aws-region: ${{ env.AWS_REGION }}
      - name: Get Caller Identity
        run: |
          aws sts get-caller-identity
```
