# ShipIt Weekend: Containerised Application and CI/CD Pipeline

![Deployment Pipeline](https://github.com/lota001/shipit-app/actions/workflows/deploy.yml/badge.svg)

## Project Overview

This project was built during **ShipIt Weekend by SKILL.SCH** to demonstrate application containerisation, cloud deployment, and CI/CD automation.

I successfully built a lightweight Python web application, containerised it using Docker, published the image to GitHub Container Registry (GHCR), and deployed it to Azure Container Apps.

Using GitHub Actions, I automated the entire build and deployment process, enabling continuous deployment whenever changes are pushed to the `main` branch.

## Technologies Used

- Python
- Docker
- GitHub Container Registry (GHCR)
- GitHub Actions
- Azure Container Apps
- Microsoft Entra ID and RBAC
- Azure CLI
- Git and GitHub

## CI/CD Pipeline Architecture

```text
       Local Development
              |
           Git Push
              |
              v
        GitHub Repository
              |
              v
        GitHub Actions
              |
              v
       Build Docker Image
              |
              v
    GitHub Container Registry
              |
              v
      Authenticate to Azure
              |
              v
      Azure Container Apps
              |
              v
        Live Application
```

## How It Works

1. Code changes are pushed to the `main` branch.
2. GitHub Actions automatically triggers the deployment workflow.
3. Docker builds a new container image.
4. The image is tagged with the shortened Git commit SHA and pushed to GHCR.
5. GitHub Actions authenticates with Azure using a service principal.
6. Azure Container Apps pulls the new image and provisions a new application revision.

## Repository Structure

| File | Description |
|---|---|
| `app.py` | Lightweight Python web application running on port 8080. |
| `Dockerfile` | Defines the container image configuration. |
| `.github/workflows/deploy.yml` | Automates the build, push, and deployment process. |
| `README.md` | Project documentation. |

## Running the Application Locally

Build the Docker image:

```bash
docker build -t shipit-app .
```

Start the container:

```bash
docker run -d --rm -p 8080:8080 --name shipit shipit-app
```

Test the application:

```bash
curl http://localhost:8080
```

Stop the container:

```bash
docker stop shipit
```

## Security Best Practices

- Runs the application inside the container as a non-root user.
- Stores Azure credentials securely using GitHub Actions secrets.
- Restricts service principal permissions to the project's resource group.
- Uses commit-based image tags for version tracking and deployment traceability.

## Challenges and Troubleshooting

During implementation, I encountered Azure authentication and container registry authorisation errors.

Troubleshooting these issues strengthened my understanding of service principal credentials, JSON configuration, registry permissions, and container image accessibility.

After troubleshooting, the GitHub Actions workflow completed successfully, confirming that the automated deployment pipeline was operational.

## What I Learned

- Containerising applications using Docker.
- Publishing and managing container images in GHCR.
- Provisioning and managing Azure resources using Azure CLI.
- Configuring service principal authentication and RBAC.
- Building automated deployment pipelines using GitHub Actions.
- Troubleshooting authentication and deployment failures.
- Applying cloud security, reliability, operational excellence, and cost optimisation principles.

## Future Improvements

- [ ] Add automated application tests before deployment.
- [ ] Integrate Trivy for container image vulnerability scanning.
- [ ] Replace service principal secrets with OpenID Connect (OIDC).
- [ ] Implement automated health checks and rollback mechanisms.
- [ ] Provision Azure infrastructure using Terraform.
- [ ] Integrate Azure Monitor for application observability.

## Project Outcome

The application was successfully deployed to Azure Container Apps through an automated GitHub Actions pipeline, demonstrating an end-to-end containerised application delivery process.

## About

Built by **Lotanna** during **ShipIt Weekend by SKILL.SCH**.
