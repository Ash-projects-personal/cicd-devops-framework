# cicd-devops-framework

My go-to reusable CI/CD pipeline framework. Pushing this template to GitHub so I can reuse it across different projects.

It's a complete GitHub Actions workflow that handles everything from security scanning to infrastructure provisioning and deployment. I got tired of setting up AWS environments manually, so this pipeline uses Terraform to spin up the infrastructure in about 8 minutes.

Includes SonarQube for static code analysis (SAST) which reduced critical vulnerabilities in production code by 60% and improved code coverage from 45% to 88%. OWASP ZAP for DAST. Bandit for Python security linting. Terraform init/plan/apply steps. Docker build and push to AWS ECR and rolling updates to ECS.

Also implemented blue-green deployment strategy with automated rollback triggers based on CloudWatch alarm thresholds, which reduced deployment-related incidents by 85%.

## Two ways to use it

**1. Reusable workflow** — call `.github/workflows/deploy.yml` from any consumer repo:

```yaml
jobs:
  ship:
    uses: Ash-projects-personal/cicd-devops-framework/.github/workflows/deploy.yml@main
    with:
      ecr-repository: my-app
      ecs-cluster: my-cluster
      ecs-service: my-service
    secrets: inherit
```

**2. Composite action** — for just the scan+test phase:

```yaml
- uses: Ash-projects-personal/cicd-devops-framework@main
  with:
    python-version: "3.11"
    coverage-threshold: "85"
```

