# CI/CD Pipeline with GitHub Actions, Docker, SonarQube, Terraform, AWS EKS & RDS MySQL

## Overview

This project demonstrates a complete CI/CD pipeline integrating modern DevOps tools and best practices to build, scan, containerize, and deploy a Java application on AWS EKS with a backend MySQL database hosted on AWS RDS. 

---

## Key Features

- GitHub Actions: for automated build, test, security scanning, and deployment pipeline.
- SonarQube: integration for static code analysis and code quality enforcement.
- Docker: containerization and pushing images to a Docker registry.
- Terraform: for provisioning AWS infrastructure, including:
  - EKS (Elastic Kubernetes Service) cluster for container orchestration.
  - RDS MySQL database for persistent application data.
- Kubernetes: deployment using a `deployment.yaml` manifest to deploy the containerized app on EKS.
- **Secure management of secrets and credentials** for database access and other sensitive information using GitHub Secrets, Kubernetes Secrets.

---

## Pipeline Stages

1. **Compile:** Compile the Java application using Maven.
2. **SonarQube Scan:** Static code analysis and quality gate checks.
3. **Security Check:** Run security scans with Trivy and Gitleaks.
4. **Test:** Execute unit tests.
5. **Build:** Package the application and build Docker images.
6. **Push Docker Image:** Push the Docker image to a container registry.
7. **Deploy:** Use Terraform to provision AWS resources (EKS cluster and RDS MySQL), then deploy the app on EKS.

---

## Prerequisites

- AWS account with permissions for EKS, RDS, and related services.
- Docker registry account (Docker Hub or others).
- GitHub repository with Actions enabled.
- Terraform installed locally or in your CI environment.
- SonarQube server running and accessible.
- Secure secret management strategy (GitHub Secrets, Kubernetes Secrets, or AWS Secrets Manager).

---

## Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repo.git
cd your-repo

2. Configure GitHub Secrets
Add these secrets to your GitHub repository settings for secure credential management:

SONAR_TOKEN — SonarQube access token.

SONAR_HOST_URL — SonarQube server URL.

DOCKER_USERNAME and DOCKER_PASSWORD — Docker registry credentials.

AWS_ACCESS_KEY_ID and AWS_SECRET_ACCESS_KEY — AWS credentials with appropriate permissions.

DB_USERNAME and DB_PASSWORD — Database credentials (or use AWS Secrets Manager integration).

Any other required secrets for deployment or infrastructure.
3. Deploy Infrastructure with Terraform
Run Terraform commands to provision your AWS infrastructure including the EKS cluster and RDS MySQL instance:
####terraform init
###terraform apply

4. Update Kubernetes Secrets
Ensure your Kubernetes manifests (or Helm charts) are configured to consume database credentials securely via Kubernetes Secrets or integrate with AWS Secrets Manager.

5. Run GitHub Actions Pipeline
Push code changes to trigger the GitHub Actions workflow which will build, scan, test, containerize, push images, and deploy your application onto EKS with connectivity to the RDS MySQL backend.

Code Security: Use SonarQube and security scanning tools (Trivy, Gitleaks) to identify vulnerabilities and secrets leakage.

Security Considerations:
Secrets Management: All sensitive information such as database credentials and tokens are stored securely using GitHub Secrets and Kubernetes Secrets

Network Security: Proper security groups and IAM roles are configured to restrict access to the RDS instance and EKS nodes.

