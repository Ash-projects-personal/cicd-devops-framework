# cicd-devops-framework

My go-to reusable CI/CD pipeline framework. Pushing this template to GitHub so I can reuse it across different projects.

## What this does

It's a complete GitHub Actions workflow that handles everything from security scanning to infrastructure provisioning and deployment. I got tired of setting up AWS environments manually, so this pipeline uses Terraform to spin up the infrastructure in about 8 minutes.

It includes:
- **Security**: SonarQube (SAST), OWASP ZAP (DAST), and Bandit (Python security linter)
- **Testing**: Pytest with a strict 85% coverage gate
- **Infrastructure as Code**: Terraform init/plan/apply steps
- **Deployment**: Docker build/push to AWS ECR and rolling updates to ECS

## The numbers

- **Time saved**: Dropped environment setup time from hours to ~8 minutes
- **Security**: The SAST/DAST combo caught enough issues to reduce critical vulnerabilities in prod by 60%

## Files

- `.github/workflows/deploy.yml`: The core pipeline definition. Just drop this into any Python/Node project, configure the GitHub secrets, and it runs on push to main.
