<div align="center">
  <h1 align="center">
  <img
    width="100"
    height="100"
    alt="astraops"
    src="https://github.com/user-attachments/assets/4eee67ad-c27b-4113-ae8f-15d3d996365c"
  /><br>
  AstraOps
</h1>
   


<h4 align="center">A tool to automate the deployment of containerized applications on AWS EKS securely within the user's account.</h4>
  <a href="https://github.com/AstraOpsOrg">
        <img  src="https://github.com/AstraOpsOrg/.github/blob/main/profile/snake.svg" alt="snake" />

  </a>
</div>

AstraOps is a cloud deployment automation platform that simplifies the deployment of containerized applications on AWS EKS. The platform handles infrastructure provisioning, application deployment, and monitoring setup through a simple command-line interface.

## Components

The AstraOps platform consists of three main components:

### [AstraBack](https://github.com/AstraOpsOrg/AstraBack)

The backend orchestration engine that manages the deployment lifecycle. Built with Bun and Hono, it provides a REST API that coordinates Terraform for infrastructure provisioning, kubectl for Kubernetes deployments, and Helm for monitoring setup. Handles AWS service integrations and streams real-time deployment logs via SSE.

### [AstraCLI](https://github.com/AstraOpsOrg/AstraCLI)

A command-line interface tool that serves as the entry point for developers. Built with TypeScript and distributed as standalone binaries for Linux, Windows, and macOS. Manages AWS IAM authentication, creates execution roles with least-privilege policies, and communicates with the AstraBack API to orchestrate deployments.

### [AstraDemo](https://github.com/AstraOpsOrg/AstraDemo)

A reference implementation demonstrating the platform capabilities. A simple full-stack points counter application with React frontend, Express.js backend, and MongoDB database. Includes a complete CI/CD pipeline with GitHub Actions that automatically builds Docker images and deploys to AWS EKS using AstraOps.

## How It Works

1. Define your application services in an `astraops.yaml` file
2. Run `astraops-cli deploy` to provision infrastructure and deploy
3. AstraCLI authenticates with AWS and creates necessary IAM roles
4. AstraBack orchestrates Terraform to create EKS cluster and VPC
5. Application containers are deployed to Kubernetes
6. Optional monitoring stack (Grafana + Prometheus) is installed
7. Run `astraops-cli destroy` to tear down all infrastructure

## Quick Start

Install the CLI:
```bash
npm install -g @astraops/astraops-cli
```

Configure environment variables and create an `astraops.yaml` file:
```yaml
applicationName: my-app
services:
  - name: frontend
    image: my-frontend:latest
    port: 80
```

Deploy:
```bash
astraops-cli deploy --monitoring
```

## Documentation

For detailed documentation, visit:
- [AstraBack Documentation](https://deepwiki.com/AstraOpsOrg/AstraBack)
- [AstraCLI Documentation](https://deepwiki.com/AstraOpsOrg/AstraCLI)
- [AstraDemo Documentation](https://deepwiki.com/AstraOpsOrg/AstraDemo)

## License

Apache License 2.0
