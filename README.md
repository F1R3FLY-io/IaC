# Infrastructure as Code (IaC) Deployment Scripts

Python-based Infrastructure as Code scripts for deploying web applications to Oracle Cloud Infrastructure (OCI) and other cloud platforms. This project provides automated deployment solutions for React/Vite applications with pnpm, featuring generalized deployment patterns for modern web applications.

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

## Getting Started

### Prerequisites

- **Python** (v3.9 or higher) - Core requirement for deployment automation
- **uv** - Fast Python package manager ([install guide](https://docs.astral.sh/uv/getting-started/installation/))
- **OCI CLI** - Oracle Cloud Infrastructure command-line interface
- **Docker** - For containerized application deployment
- **Git** - Version control for infrastructure code
- **Node.js** (v18 or higher) - For web application builds (target applications)
- **pnpm** (v8 or higher) - Package manager for web applications (target applications)

### Quick Start

#### 1. Infrastructure Setup

```bash
# Install uv (if not already installed)
curl -LsSf https://astral.sh/uv/install.sh | sh

# Clone the repository
git clone <repository-url>
cd IaC

# Install dependencies (automatically creates virtual environment)
uv sync

# Configure OCI CLI (interactive setup)
oci setup config
```

#### 2. Deploy a Web Application

```bash
# Example: Deploy a React/Vite application
uv run deploy.py --app-type react-vite --environment dev --source-path ../my-react-app

# Monitor deployment status
uv run scripts/status.py --environment dev

# Check deployed resources
uv run scripts/list-resources.py --environment dev
```

#### 3. Environment Configuration

```bash
# Copy example configuration
cp config/config.example.yaml config/config.yaml

# Edit configuration for your environments
# Set OCI compartment IDs, regions, and resource specifications
vim config/config.yaml
```

### Development

#### Infrastructure Development

```bash
# Run tests
uv run pytest tests/

# Code formatting
uv run black src/ scripts/ tests/

# Import sorting
uv run isort src/ scripts/ tests/

# Linting
uv run flake8 src/ scripts/

# Type checking
uv run mypy src/ scripts/

# Add new dependencies
uv add package-name

# Add development dependencies
uv add --dev package-name
```

#### Configuration Management

```bash
# Validate configuration files
uv run scripts/validate-config.py --config config/config.yaml

# Generate environment-specific configs
uv run scripts/generate-configs.py --template config/template.yaml

# Test OCI connectivity
uv run scripts/test-connection.py --environment dev
```

### Deployment Operations

#### Production Deployment

```bash
# Deploy to production environment
uv run deploy.py --environment prod --app-type react-vite --source-path ../my-app --confirm

# Deploy with specific resource specifications
uv run deploy.py --environment prod --config config/prod-config.yaml --scaling-policy auto

# Deploy static assets only (faster updates)
uv run deploy.py --environment prod --static-only --source-path ../my-app/dist
```

#### Rollback and Recovery

```bash
# List available deployment versions
uv run scripts/list-deployments.py --environment prod

# Rollback to previous version
uv run scripts/rollback.py --environment prod --version v1.2.0

# Emergency cleanup (removes all resources)
uv run scripts/cleanup.py --environment dev --force
```

### Testing

#### Infrastructure Testing

```bash
# Run all tests
uv run pytest tests/ -v

# Run tests with coverage
uv run pytest tests/ --cov=src --cov-report=html

# Run specific test categories
uv run pytest tests/test_oci_resources.py -v
uv run pytest tests/test_deployment.py -v
uv run pytest tests/test_configuration.py -v

# Integration tests (requires OCI access)
uv run pytest tests/integration/ --oci-integration
```

#### Dry Run Testing

```bash
# Test deployment without actually creating resources
uv run deploy.py --environment dev --dry-run --source-path ../test-app

# Validate configuration without deployment
uv run scripts/validate-deployment.py --config config/dev-config.yaml

# Test resource provisioning scripts
uv run scripts/test-provisioning.py --environment test --mock
```

## Deployment Architecture

This Infrastructure as Code project supports multiple deployment patterns for web applications:

### Supported Application Types
- **React/Vite Applications**: Modern React applications built with Vite
- **Static Sites**: HTML/CSS/JS static websites
- **Single Page Applications (SPA)**: Client-side rendered applications
- **Server-Side Rendered (SSR)**: Next.js and similar frameworks

### OCI Deployment Options
- **Container Instances**: Containerized application deployment
- **Object Storage**: Static asset hosting with CDN
- **Compute Instances**: VM-based deployment for custom requirements
- **Load Balancers**: Traffic distribution and SSL termination
- **Functions**: Serverless deployment for API endpoints

### Quick Deployment

#### Prerequisites

```bash
# Install OCI CLI (if not already installed)
bash -c "$(curl -L https://raw.githubusercontent.com/oracle/oci-cli/master/scripts/install/install.sh)"

# Configure OCI credentials
oci setup config
```

#### Deploy to OCI

```bash
# 1. Build the frontend application
pnpm build

# 2. Navigate to deployment directory and install tools
cd deployment/oci-deployment
uv sync

# 3. Deploy to development environment
uv run sankey-deploy deploy --environment dev --image-tag latest

# 4. Check deployment status
uv run sankey-deploy status --environment dev

# 5. Deploy only static assets (faster for frontend-only changes)
uv run sankey-deploy deploy --environment dev --static-only
```

#### Environment-Specific Deployment

```bash
# From deployment/oci-deployment directory:

# Development
uv run sankey-deploy deploy --environment dev --image-tag v1.0.0

# Staging
uv run sankey-deploy deploy --environment staging --image-tag v1.0.0

# Production
uv run sankey-deploy deploy --environment prod --image-tag v1.0.0
```

## Project Structure

### Infrastructure as Code Layout

```
IaC/
├── src/                          # Core deployment modules
│   ├── oci/                      # Oracle Cloud Infrastructure modules
│   │   ├── compute.py            # Compute instance management
│   │   ├── containers.py         # Container service management
│   │   ├── storage.py            # Object storage management
│   │   ├── networking.py         # VCN and load balancer management
│   │   └── __init__.py           # OCI module initialization
│   ├── aws/                      # AWS deployment modules (future)
│   ├── azure/                    # Azure deployment modules (future)
│   ├── common/                   # Shared utilities
│   │   ├── config.py             # Configuration management
│   │   ├── logging.py            # Logging utilities
│   │   ├── validation.py         # Input validation
│   │   └── utils.py              # General utilities
│   └── deployment/               # Deployment orchestration
│       ├── manager.py            # Main deployment manager
│       ├── builder.py            # Application builder
│       └── monitor.py            # Deployment monitoring
├── scripts/                      # Standalone utility scripts
│   ├── deploy.py                 # Main deployment script
│   ├── cleanup.py                # Resource cleanup script
│   ├── status.py                 # Deployment status checker
│   ├── rollback.py               # Rollback functionality
│   └── validate-config.py        # Configuration validator
├── config/                       # Configuration files
│   ├── config.example.yaml       # Example configuration
│   ├── environments/             # Environment-specific configs
│   │   ├── dev.yaml              # Development environment
│   │   ├── staging.yaml          # Staging environment
│   │   └── prod.yaml             # Production environment
│   └── templates/                # Infrastructure templates
├── tests/                        # Test suite
│   ├── unit/                     # Unit tests
│   ├── integration/              # Integration tests
│   └── fixtures/                 # Test fixtures and mocks
├── docs/                         # Documentation
│   ├── deployment-guide.md       # Comprehensive deployment guide
│   ├── configuration.md          # Configuration reference
│   └── troubleshooting.md        # Common issues and solutions
├── pyproject.toml                # Project configuration and dependencies
├── uv.lock                       # Locked dependency versions
└── CLAUDE.md                     # Project instructions for Claude
```

### Deployment Pipeline Structure

The infrastructure supports a clean separation of concerns:

- **Resource Management**: Cloud-specific modules handle resource provisioning
- **Application Building**: Generic build processes for different app types
- **Configuration**: Environment-specific settings and templates
- **Testing**: Comprehensive test coverage for infrastructure code
- **Monitoring**: Deployment status and health checking utilities

### Multi-Cloud Architecture

The project is designed for extensibility:

- **Primary Focus**: Oracle Cloud Infrastructure (OCI)
- **Future Support**: AWS, Azure, and other cloud providers
- **Modular Design**: Cloud-specific implementations with common interfaces
- **Configuration-Driven**: Environment and cloud provider selection via config files

## Configuration Management

### Environment Variables

The deployment scripts use environment variables for sensitive configuration:

```bash
# Oracle Cloud Infrastructure Configuration
export OCI_CONFIG_FILE=~/.oci/config
export OCI_CONFIG_PROFILE=DEFAULT
export OCI_COMPARTMENT_ID=ocid1.compartment.oc1..your-compartment-id

# Deployment Configuration
export DEPLOYMENT_REGION=us-ashburn-1
export DEPLOYMENT_ENVIRONMENT=dev
export LOG_LEVEL=INFO

# Application-Specific Variables
export APP_NAME=my-web-app
export DOMAIN_NAME=example.com
export SSL_CERTIFICATE_PATH=/path/to/ssl/cert
```

### Configuration Files

Create environment-specific YAML configuration files:

```yaml
# config/environments/dev.yaml
environment: dev
region: us-ashburn-1
compartment_id: ocid1.compartment.oc1..your-compartment-id

resources:
  compute:
    shape: VM.Standard.E3.Flex
    memory_gb: 4
    cpu_count: 2
  
  storage:
    bucket_name: my-app-dev-static
    public_access: true
  
  networking:
    vcn_cidr: "10.0.0.0/16"
    subnet_cidr: "10.0.1.0/24"

application:
  type: react-vite
  build_command: "pnpm build"
  dist_directory: "dist"
  port: 3000
```

## Current Development Status

This Infrastructure as Code project is actively being developed with the following features:

### Implemented Features
- **OCI Resource Management**: Core modules for Oracle Cloud Infrastructure
- **Multi-Environment Support**: Development, staging, and production configurations  
- **Application Build Integration**: Support for React/Vite applications with pnpm
- **Configuration Management**: YAML-based environment-specific configurations
- **Testing Framework**: Unit and integration tests for infrastructure code
- **Logging and Monitoring**: Comprehensive logging and deployment status tracking

### In Development
- **AWS Module**: Amazon Web Services deployment support
- **Azure Module**: Microsoft Azure deployment capabilities
- **CI/CD Pipelines**: GitHub Actions and GitLab CI integration
- **Advanced Monitoring**: Application performance and infrastructure monitoring

### Planned Features
- **Multi-Cloud Orchestration**: Deploy across multiple cloud providers simultaneously
- **Disaster Recovery**: Automated backup and recovery procedures
- **Auto-Scaling**: Dynamic resource scaling based on application load
- **Security Hardening**: Advanced security configurations and compliance checking

## Troubleshooting

### Common Issues

#### OCI Authentication Problems

```bash
# Configure OCI CLI if not already done
oci setup config

# Test OCI connectivity
oci iam compartment list --compartment-id-in-subtree true

# Check configuration file
cat ~/.oci/config

# Verify credentials
python scripts/test-connection.py --environment dev
```

#### Python Environment Issues

```bash
# Python version problems
python --version  # Should be 3.9+
uv python install 3.11  # Install specific Python version
uv python use 3.11      # Use specific Python version for project

# Dependencies not installing
uv sync --reinstall

# Module import errors
uv run python -c "import src.oci.compute; print('Import successful')"

# Check uv installation
uv --version
```

#### Deployment Failures

```bash
# Check deployment logs
uv run scripts/status.py --environment dev --verbose

# Validate configuration before deployment
uv run scripts/validate-config.py --config config/environments/dev.yaml

# Clean up failed deployments
uv run scripts/cleanup.py --environment dev --partial

# Retry deployment with debug logging
export LOG_LEVEL=DEBUG
uv run deploy.py --environment dev --source-path ../my-app
```

#### Resource Access Issues

```bash
# Check compartment permissions
oci iam compartment list --compartment-id YOUR_COMPARTMENT_ID

# Verify resource quotas
uv run scripts/check-quotas.py --environment dev

# List existing resources
uv run scripts/list-resources.py --environment dev --detailed
```

## Command Reference

### Core Deployment Commands

| Command | Description |
|---------|-------------|
| `uv run deploy.py` | Main deployment script |
| `uv run scripts/status.py` | Check deployment status |
| `uv run scripts/cleanup.py` | Clean up resources |
| `uv run scripts/rollback.py` | Rollback deployment |
| `uv run scripts/list-resources.py` | List cloud resources |
| `uv run scripts/validate-config.py` | Validate configuration |

### Development Commands

| Command | Description |
|---------|-------------|
| `uv run pytest` | Run test suite |
| `uv run black src/ scripts/` | Format Python code |
| `uv run flake8 src/ scripts/` | Lint Python code |
| `uv run mypy src/ scripts/` | Type check Python code |
| `uv run isort src/ scripts/` | Sort Python imports |

### Environment Management

| Command | Description |
|---------|-------------|
| `uv sync` | Install dependencies and create venv |
| `uv add package-name` | Add production dependency |
| `uv add --dev package-name` | Add development dependency |
| `uv remove package-name` | Remove dependency |
| `uv lock` | Update lock file |
| `uvx script-name` | Run one-off scripts without installing

### Quick Commands

```bash
# Complete infrastructure setup
curl -LsSf https://astral.sh/uv/install.sh | sh
git clone <repository-url>
cd IaC
uv sync
oci setup config

# Deploy React/Vite application
uv run deploy.py --app-type react-vite --environment dev --source-path ../my-app

# Run tests and deploy
uv run pytest && uv run deploy.py --environment dev --source-path ../my-app

# Clean deployment and redeploy
uv run scripts/cleanup.py --environment dev --force
uv run deploy.py --environment dev --source-path ../my-app --fresh-deployment

# One-off script execution (no project setup required)
uvx script-name --args
```

## License

[Sovereign Source License](https://gitlab.com/smart-assets.io/SovereignLicense/-/raw/main/SovereignLicense.md)
