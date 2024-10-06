# Flask App with CI/CD and Kubernetes Deployment

This project demonstrates a simple Flask application with a complete CI/CD pipeline using GitHub Actions and deployment to Kubernetes. It serves as a learning tool for understanding these technologies and how they work together.

## Table of Contents

1. [Project Overview](#project-overview)
2. [Prerequisites](#prerequisites)
3. [Local Development](#local-development)
4. [Docker](#docker)
5. [CI/CD Pipeline](#cicd-pipeline)
6. [Kubernetes Deployment](#kubernetes-deployment)
7. [Security and Secrets](#security-and-secrets)
8. [Troubleshooting](#troubleshooting)
9. [Contributing](#contributing)
10. [License](#license)

## Project Overview

This project consists of:
- A simple Flask app that returns "Hello, World!"
- Dockerfile for containerization
- GitHub Actions workflow for CI/CD
- Kubernetes configuration for deployment

## Prerequisites

- Python 3.9+
- Docker
- kubectl
- A Kubernetes cluster (Minikube for local development)
- GitHub account
- Docker Hub account

## Local Development

1. Clone the repository:
   ```
   git clone https://github.com/your-username/your-repo-name.git
   cd your-repo-name
   ```

2. Create a virtual environment and activate it:
   ```
   python -m venv venv
   source venv/bin/activate  # On Windows, use `venv\Scripts\activate`
   ```

3. Install dependencies:
   ```
   pip install -r requirements.txt
   ```

4. Run the Flask app:
   ```
   python app.py
   ```

5. Visit `http://localhost:5000` in your browser.

## Docker

Build and run the Docker image locally:

```
docker build -t flask-app .
docker run -p 5000:5000 flask-app
```

## CI/CD Pipeline

The CI/CD pipeline is implemented using GitHub Actions. It does the following:

1. Builds the application
2. Runs tests
3. Builds a Docker image
4. Pushes the image to Docker Hub
5. Deploys to Kubernetes (if on the main branch)

To set up the CI/CD pipeline:

1. Fork this repository to your GitHub account.
2. Set up the following secrets in your GitHub repository:
   - `DOCKER_USERNAME`: Your Docker Hub username
   - `DOCKER_PASSWORD`: Your Docker Hub password or access token
3. Push changes to the `main` branch to trigger the workflow.

## Kubernetes Deployment

To deploy the application to Kubernetes:

1. Ensure you have a Kubernetes cluster running and `kubectl` configured.
2. Apply the Kubernetes configuration:
   ```
   kubectl apply -f kubernetes/deployment.yaml
   ```
3. Check the deployment status:
   ```
   kubectl get deployments
   kubectl get services
   ```

## Security and Secrets

Secrets are managed securely using GitHub Secrets for CI/CD and Kubernetes Secrets for deployment. Never commit sensitive information directly to the repository.

To add a new secret to Kubernetes:

1. Create a `secret.yaml` file (do not commit this file):
   ```yaml
   apiVersion: v1
   kind: Secret
   metadata:
     name: my-app-secrets
   type: Opaque
   data:
     SECRET_KEY: <base64-encoded-secret>
   ```
2. Apply the secret:
   ```
   kubectl apply -f secret.yaml
   ```

## Troubleshooting

- If the GitHub Actions workflow fails, check the workflow logs for error messages.
- For Kubernetes issues, use `kubectl describe` and `kubectl logs` to diagnose problems.
- Ensure all necessary secrets are properly set in both GitHub and Kubernetes.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
