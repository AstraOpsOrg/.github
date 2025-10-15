# AstraOps

<div align="center">
  <h1 align="center"><img src = "" width = 45px></picture> AstraOps </h1>
    <h4 align="center">A tool to automate the deployment of containerized applications on AWS EKS securely within the user's account.</h4>
  <a href="https://github.com/AstraOpsOrg">
    <img src="" alt="snake" />
  </a>
</div>

AstraOps is a unified cloud deployment automation platform that simplifies AWS EKS infrastructure management through a single REST API. The platform coordinates infrastructure provisioning, application deployment, and monitoring setup, abstracting the complexity of managing Terraform, Kubernetes, AWS services, and observability tools.

## Overview

AstraOps provides end-to-end deployment orchestration from infrastructure provisioning to application deployment and monitoring setup. The system enables developers to deploy complete application stacks on AWS EKS clusters through a simple command-line interface, handling all the underlying complexity automatically.

## Architecture

The AstraOps platform consists of three main components:

### AstraBack (Backend Platform)

The core orchestration engine that manages deployment workflows, infrastructure provisioning, and real-time logging. It provides a REST API that coordinates Terraform operations, Kubernetes deployments, AWS service integrations, and monitoring stack setup.

**Key Features:**
- REST API for deployment orchestration
- Real-time log streaming via Server-Sent Events (SSE)
- Automated EKS cluster provisioning using Terraform
- Kubernetes application deployment with kubectl
- Grafana and Prometheus monitoring stack setup
- Job lifecycle management with phase tracking
- Infrastructure teardown capabilities

### AstraCLI (Command-Line Interface)

A TypeScript-based CLI tool that serves as the primary interface for developers to interact with the AstraOps platform. The CLI handles AWS authentication, IAM role management, and communicates with the AstraOps backend to orchestrate deployments.

**Key Features:**
- Simple deployment commands (deploy, destroy)
- Automated IAM role creation with least-privilege policies
- Deployment simulation capabilities
- Real-time deployment progress tracking
- Automated monitoring setup
- Multi-platform support (Linux, Windows, macOS)
- Distributed via NPM and GitHub Releases

### AstraDemo (Reference Application)

A demonstration full-stack application that showcases AstraOps deployment capabilities. It implements a points counter application with a React frontend, Express.js backend, and MongoDB database, all deployed automatically via AstraOps.

**Components:**
- React SPA served by Nginx
- Express.js REST API backend
- MongoDB database for persistence
- Automated CI/CD pipeline with GitHub Actions
- Complete infrastructure-as-code configuration

## Technology Stack

### Backend Platform
- **Runtime:** Bun JavaScript runtime
- **Web Framework:** Hono for REST API
- **Language:** TypeScript
- **AWS Integration:** AWS SDK (STS, S3, EKS)
- **Infrastructure Tools:** Terraform, kubectl, Helm, AWS CLI

### CLI Tool
- **Language:** TypeScript
- **Runtime:** Bun-compiled standalone binaries
- **CLI Framework:** Commander.js
- **AWS Integration:** AWS SDK (IAM, STS)
- **Configuration:** YAML parsing for astraops.yaml

### Demo Application
- **Frontend:** React 18, Vite, Nginx
- **Backend:** Node.js 18, Express.js, Mongoose
- **Database:** MongoDB
- **Containerization:** Docker
- **CI/CD:** GitHub Actions

## Deployment Workflow

1. **Authentication Phase:** CLI establishes AWS credentials and assumes execution role
2. **Infrastructure Phase:** Backend provisions EKS cluster, VPC, and networking via Terraform
3. **Deployment Phase:** Backend deploys application containers to EKS using kubectl
4. **Monitoring Phase:** Backend installs Grafana and Prometheus for observability (optional)

## Core Capabilities

| Capability | Description | Implementation |
|-----------|-------------|----------------|
| Infrastructure Provisioning | Automated AWS EKS cluster creation with VPC, subnets, and security groups | Terraform with S3 state management |
| Application Deployment | Kubernetes application deployment with service exposure | kubectl with generated manifests |
| Monitoring Setup | Automated Grafana and Prometheus stack deployment | Helm charts on EKS clusters |
| Real-time Logging | Live deployment progress tracking and log streaming | Server-Sent Events (SSE) |
| Job Management | Deployment job orchestration with phase tracking | In-memory job state management |
| Infrastructure Teardown | Complete infrastructure cleanup and resource deletion | Terraform destroy operations |

## Getting Started

### Prerequisites

- AWS Account with appropriate permissions
- AWS Access Key ID and Secret Access Key
- AstraOps API Key (for backend access)
- Node.js (for local development)

### Installation

Install the AstraOps CLI via NPM:

```bash
npm install -g @astraops/astraops-cli
```

### Configuration

Set the required environment variables:

```bash
export AWS_ACCESS_KEY_ID="your-access-key"
export AWS_SECRET_ACCESS_KEY="your-secret-key"
export AWS_ACCOUNT_ID="your-account-id"
export AWS_REGION="us-west-2"
export ASTRAOPS_API_KEY="your-api-key"
export ASTRAOPS_API_URL="https://api.astraops.com"
```

### Basic Usage

Create an `astraops.yaml` configuration file:

```yaml
applicationName: my-app
services:
  - name: frontend
    image: my-frontend:latest
    port: 80
  - name: backend
    image: my-backend:latest
    port: 5000
    environment:
      DATABASE_URL: mongodb://database:27017/mydb
  - name: database
    image: mongo:latest
    port: 27017
```

Deploy your application:

```bash
astraops-cli deploy --monitoring
```

Destroy infrastructure when done:

```bash
astraops-cli destroy
```

## Repository Structure

```
AstraOps/
├── AstraBack/          # Backend orchestration platform
├── AstraCLI/           # Command-line interface
├── AstraDemo/          # Reference application
└── docs/               # Documentation and architecture diagrams
```

## Use Cases

- **Rapid Prototyping:** Quickly spin up complete application stacks for testing and development
- **Continuous Deployment:** Integrate with CI/CD pipelines for automated deployments
- **Infrastructure Management:** Provision and teardown AWS EKS environments on demand
- **Multi-Service Applications:** Deploy complex microservices architectures with a single command
- **Development Environments:** Create isolated cloud environments for development teams

## Security

AstraOps implements security best practices:

- Least-privilege IAM policies for execution roles
- AWS STS for temporary credential management
- Automated IAM role and user creation
- Secure credential handling via environment variables
- S3 backend for Terraform state management

## Monitoring and Observability

The platform includes optional monitoring capabilities:

- Automated Grafana dashboard setup
- Prometheus metrics collection
- Real-time deployment log streaming
- Job status tracking with phase-level granularity

## License

This project is licensed under the Apache License 2.0.

## Contributing

Contributions are welcome. Please see individual repository READMEs for specific contribution guidelines.

## Support

For issues, questions, or contributions:
- **Backend:** [AstraBack Repository](https://github.com/AstraOpsOrg/AstraBack)
- **CLI:** [AstraCLI Repository](https://github.com/AstraOpsOrg/AstraCLI)
- **Demo:** [AstraDemo Repository](https://github.com/AstraOpsOrg/AstraDemo)

## Documentation

Comprehensive documentation is available through DeepWiki:
- [AstraBack Documentation](https://deepwiki.com/AstraOpsOrg/AstraBack)
- [AstraCLI Documentation](https://deepwiki.com/AstraOpsOrg/AstraCLI)
- [AstraDemo Documentation](https://deepwiki.com/AstraOpsOrg/AstraDemo)
