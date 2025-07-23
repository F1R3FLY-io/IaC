# Infrastructure as Code (IaC) Deployment Scripts

Python-based Infrastructure as Code scripts for deploying web applications to Oracle Cloud Infrastructure (OCI) and other cloud platforms. This project provides automated deployment solutions for React/Vite applications with pnpm, featuring generalized deployment patterns for modern web applications.

> 📖 **For developers, contributors, and detailed project information**: See the [complete documentation](docs/README.md)

## Features

- **Multi-Cloud Support**: Primary focus on Oracle Cloud Infrastructure (OCI) with extensibility for other cloud providers
- **Web Application Deployment**: Automated deployment of React/Vite applications built with pnpm
- **Infrastructure Automation**: Python-based scripts for provisioning and managing cloud resources
- **Environment Management**: Support for development, staging, and production environments
- **Container Orchestration**: Deployment to container services and serverless platforms
- **Static Asset Management**: Automated deployment to cloud storage services
- **CI/CD Integration**: GitHub Actions and other pipeline integrations
- **Resource Cleanup**: Automated cleanup and rollback mechanisms
- **Configuration Management**: Environment-specific configurations and secrets management

## Technologies

- **Python 3.9+**: Core deployment automation language
- **Oracle Cloud Infrastructure (OCI) SDK**: Python SDK for OCI resource management
- **OCI CLI**: Command-line interface for Oracle Cloud operations
- **Docker**: Containerization for application deployment
- **GitHub Actions**: CI/CD pipeline automation
- **pnpm**: Package manager for web applications
- **Vite**: Build tool for modern web applications
- **React/TypeScript**: Target application technology stack

## Quick Start

### Prerequisites

Before starting, ensure you have these requirements installed:

- **Python** (v3.9 or higher) - Core requirement for deployment automation
  ```bash
  python --version  # Should show 3.9.0 or higher
  ```
- **uv** - Fast Python package manager ([install guide](https://docs.astral.sh/uv/getting-started/installation/))
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  ```
- **OCI CLI** - Oracle Cloud Infrastructure command-line interface
  ```bash
  bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"
  ```
- **Docker** - For containerized application deployment (optional, for custom builds)
- **Git** - Version control for infrastructure code

### 3-Step Deployment

#### 1. Setup Requirements & Installation
```bash
# Verify Python version (3.9+ required)
python --version

# Install uv (fast Python package manager)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Install OCI CLI (Oracle Cloud Infrastructure CLI)
bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"

# Clone repository and install dependencies
git clone <repository-url>
cd IaC/deployment/oci-deployment
uv sync  # Automatically creates virtual environment and installs all dependencies

# Configure OCI credentials (interactive setup)
oci setup config
```

#### 2. Configure Environment
```bash
# Copy and edit environment configuration
cp configs/dev.env.example configs/dev.env
# Edit configs/dev.env with your OCI compartment ID and settings
```

#### 3. Deploy
```bash
# Deploy your React/Vite application
uv run oci-deploy deploy --environment dev --image-tag latest

# Check deployment status
uv run oci-deploy status --environment dev
```

## Basic Usage

### Deploy Applications
```bash
# Deploy to development
uv run oci-deploy deploy --environment dev --image-tag v1.0.0

# Deploy to production
uv run oci-deploy deploy --environment prod --image-tag v1.0.0

# Deploy only static assets (faster updates)
uv run oci-deploy deploy --environment dev --static-only

# Deploy only container instances
uv run oci-deploy deploy --environment dev --container-only
```

### Manage Deployments
```bash
# Check deployment status
uv run oci-deploy status --environment dev

# List all resources
uv run oci-deploy list-resources --environment dev

# Clean up resources
uv run oci-deploy cleanup --environment dev
```

### Configuration
```bash
# Validate configuration
uv run oci-deploy config-check --environment dev

# Test OCI connectivity
uv run scripts/test-connection.py --environment dev
```

## Environment Configuration

Create environment-specific configuration files in the `configs/` directory:

```bash
# Development environment
cp configs/dev.env.example configs/dev.env

# Production environment
cp configs/prod.env.example configs/prod.env
```

Key configuration variables:
- `OCI_COMPARTMENT_ID`: Your OCI compartment ID
- `OCI_REGION`: OCI region (e.g., us-ashburn-1)
- `CONTAINER_REGISTRY_URL`: OCI container registry URL
- `FRONTEND_BUCKET_NAME`: Object storage bucket name

## Common Troubleshooting

### OCI Authentication Issues
```bash
# Configure OCI CLI
oci setup config

# Test connectivity
oci iam compartment list --compartment-id-in-subtree true

# Verify credentials
uv run scripts/test-connection.py --environment dev
```

### Python Environment Issues
```bash
# Check uv installation
uv --version

# Reinstall dependencies
uv sync --reinstall

# Check Python version
python --version  # Should be 3.9+
```

### Deployment Failures
```bash
# Check deployment logs with verbose output
uv run oci-deploy status --environment dev --verbose

# Validate configuration
uv run oci-deploy config-check --environment dev

# Clean up and retry
uv run oci-deploy cleanup --environment dev
uv run oci-deploy deploy --environment dev --image-tag latest
```

## Command Reference

| Command | Description |
|---------|-------------|
| `uv run oci-deploy deploy` | Deploy application |
| `uv run oci-deploy status` | Check deployment status |
| `uv run oci-deploy cleanup` | Clean up resources |
| `uv run oci-deploy config-check` | Validate configuration |
| `uv run oci-deploy list-resources` | List cloud resources |

### Quick Commands
```bash
# Complete setup and deploy (all requirements included)
python --version  # Verify Python 3.9+
curl -LsSf https://astral.sh/uv/install.sh | sh  # Install uv
bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"  # Install OCI CLI
git clone <repository-url>
cd IaC/deployment/oci-deployment
uv sync  # Install all dependencies
oci setup config  # Configure OCI credentials
uv run oci-deploy deploy --environment dev --image-tag latest

# One-off script execution (no project setup required)
uvx script-name --args
```

## Documentation

- **[Developer Documentation](docs/README.md)** - Complete project structure, architecture, and development guide
- **[Technical Specifications](docs/specs/IaC_python.md)** - Detailed implementation specification
- **[Project Roadmap](docs/ToDos.md)** - Remaining work and feature completion roadmap

## Support

For detailed information on:
- **Project Architecture**: See [docs/README.md](docs/README.md)
- **Development Setup**: See [docs/README.md#development](docs/README.md#development)
- **Contributing**: See [docs/README.md#contributing](docs/README.md#contributing)
- **Testing**: See [docs/README.md#testing](docs/README.md#testing)

## License

[Sovereign Source License](https://gitlab.com/smart-assets.io/SovereignLicense/-/raw/main/SovereignLicense.md)