# Infrastructure as Code (IaC) Developer Documentation

Welcome to the comprehensive developer documentation for the Infrastructure as Code project. This documentation provides detailed information for developers, contributors, and those wanting to understand the project architecture.

> 🚀 **For quick deployment and basic usage**: See the [main README.md](../README.md)

## 📋 Documentation Overview

This documentation is organized for developers and contributors who need deep understanding of the project structure, architecture, and development processes.

### For Users (Getting Started)
- **Quick Deployment**: Follow the [main README.md](../README.md) for immediate deployment
- **Basic Usage**: See main README for common deployment commands
- **Troubleshooting**: Basic issues covered in main README

### For Developers (Deep Dive)
- **Architecture Overview**: Complete system design and component relationships
- **Implementation Status**: Detailed tracking of what's implemented vs. planned
- **Development Setup**: Comprehensive local development environment setup
- **Testing Guidelines**: Complete testing strategies and frameworks
- **Contributing**: Code standards, review processes, and contribution workflows

## 🏗️ Repository Structure Guide

### `/` (Project Root)
```
IaC/
├── src/                          # Core Python modules (future)
├── deployment/                   # Current implementation
│   ├── oci-deployment/          # OCI-specific deployment automation
│   └── docker/                  # Docker containerization files
├── docs/                        # This documentation directory
│   ├── specs/                   # Technical specifications
│   └── README.md               # This navigation guide
├── config/                      # Configuration templates (future)
├── scripts/                     # Utility scripts (future)
├── tests/                       # Test suite (future)
├── pyproject.toml              # Main project configuration (future)
└── CLAUDE.md                   # Development instructions
```

### `/deployment/` (Current Implementation)
The main implementation currently resides in the deployment directory:

```
deployment/
├── oci-deployment/              # Python automation package
│   ├── src/oci_deploy/         # Core deployment modules
│   │   ├── cli.py              # Command-line interface
│   │   ├── config.py           # Configuration management
│   │   ├── containers.py       # Container deployment logic
│   │   ├── storage.py          # Object storage operations
│   │   └── networking.py       # Load balancer & networking
│   ├── configs/                # Environment configurations
│   │   ├── dev.env             # Development environment
│   │   ├── staging.env         # Staging environment
│   │   └── prod.env            # Production environment
│   ├── tests/                  # Comprehensive test suite
│   ├── scripts/                # Deployment scripts
│   ├── pyproject.toml          # Python project configuration
│   └── README.md               # Deployment-specific documentation
└── docker/                     # Docker containerization
    ├── Dockerfile.frontend     # Multi-stage React build
    ├── nginx.conf              # Production Nginx configuration
    └── docker-entrypoint.sh    # Environment variable injection
```

## 🎯 Current Implementation Status

### ✅ **Fully Implemented**
- **Core Deployment Engine**: Python-based OCI deployment automation
- **Multi-Environment Support**: Dev, staging, and production configurations
- **Container Orchestration**: OCI Container Instances deployment
- **Static Asset Management**: Object Storage integration for React builds
- **CLI Interface**: User-friendly command-line tool with rich output
- **Docker Infrastructure**: Complete containerization with Nginx
- **Testing Framework**: Comprehensive unit and integration tests
- **Configuration Management**: Environment-specific settings with validation

### 🚧 **Partially Implemented**
- **Networking Module**: Load balancer creation (CDN placeholder)
- **Monitoring Tools**: Status checking (needs enhancement)
- **Error Recovery**: Basic rollback (needs full automation)

### 📋 **Planned Features**
- **Multi-Cloud Support**: AWS and Azure modules
- **CI/CD Integration**: GitHub Actions workflows
- **Advanced Monitoring**: Application performance monitoring
- **Auto-scaling**: Dynamic resource management
- **Security Hardening**: Advanced security configurations

## 📚 Documentation Structure

### `/docs/specs/` - Technical Specifications
- **[IaC_python.md](specs/IaC_python.md)**: Original implementation plan and specification
  - Detailed architecture design
  - Phase-by-phase implementation timeline
  - Code examples and templates
  - Security and cost considerations

### Key Sections in the Specification:
1. **Phase 1**: Setup and Configuration
2. **Phase 2**: Core Implementation (containers, storage, CLI)
3. **Phase 3**: CI/CD Integration
4. **Phase 4**: Documentation and Testing
5. **Usage Examples**: Local development and deployment patterns

## 🚀 Quick Start Guide

### For Users - Deploy an Application
```bash
# 1. Install prerequisites
curl -LsSf https://astral.sh/uv/install.sh | sh  # Install uv
oci setup config  # Configure OCI credentials

# 2. Navigate to deployment tools
cd deployment/oci-deployment

# 3. Install dependencies
uv sync

# 4. Deploy your React/Vite application
uv run oci-deploy deploy --environment dev --image-tag latest
```

### For Developers - Comprehensive Development Setup
```bash
# 1. Clone and navigate
git clone <repository-url>
cd IaC/deployment/oci-deployment

# 2. Install development dependencies
uv sync

# 3. Run tests
uv run pytest

# 4. Format and lint code
uv run black src/ tests/
uv run flake8 src/ tests/
uv run mypy src/

# 5. Install pre-commit hooks (recommended)
uv run pre-commit install

# 6. Run comprehensive test suite
uv run pytest --cov=src/oci_deploy --cov-report=html

# 7. Validate deployment configuration
uv run oci-deploy config-check --environment dev
```

### For Developers - Advanced Development Tasks
```bash
# Development workflow commands
uv run black src/ scripts/ tests/     # Code formatting
uv run isort src/ scripts/ tests/     # Import sorting  
uv run flake8 src/ scripts/           # Linting
uv run mypy src/ scripts/             # Type checking

# Add new dependencies
uv add package-name                   # Production dependency
uv add --dev package-name            # Development dependency
uv remove package-name               # Remove dependency
uv lock                              # Update lock file

# Testing and validation
uv run pytest tests/ -v              # Verbose test output
uv run pytest --cov=src --cov-report=html    # Coverage report
uv run pytest tests/integration/ --oci-integration  # Integration tests

# Configuration and validation
uv run scripts/validate-config.py --config config/config.yaml
uv run scripts/generate-configs.py --template config/template.yaml
uv run scripts/test-connection.py --environment dev
```

## 🔧 Configuration Management

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

### Environment Files
Configuration is managed through environment-specific `.env` files:

- **`configs/dev.env`**: Development environment with basic resources
- **`configs/staging.env`**: Production-like staging environment
- **`configs/prod.env`**: High-performance production configuration

### Key Configuration Areas
1. **OCI Resources**: Compartment IDs, regions, availability domains
2. **Container Settings**: Registry URLs, resource allocations
3. **Storage Configuration**: Bucket names, CDN settings
4. **Application Settings**: API endpoints, build configurations

## 🧪 Testing Strategy

### Test Categories
- **Unit Tests**: Individual module testing with mocks
- **Integration Tests**: OCI service integration testing
- **End-to-End Tests**: Full deployment workflow testing

### Running Tests
```bash
# All tests
uv run pytest

# Specific test files
uv run pytest tests/test_containers.py

# With coverage
uv run pytest --cov=src/oci_deploy --cov-report=html

# Integration tests (requires OCI access)
uv run pytest tests/integration/ --oci-integration

# Dry run testing (no actual resource creation)
uv run deploy.py --environment dev --dry-run --source-path ../test-app
uv run scripts/validate-deployment.py --config config/dev-config.yaml
uv run scripts/test-provisioning.py --environment test --mock
```

## 🚀 Deployment Operations

### Production Deployment

```bash
# Deploy to production environment
uv run deploy.py --environment prod --app-type react-vite --source-path ../my-app --confirm

# Deploy with specific resource specifications
uv run deploy.py --environment prod --config config/prod-config.yaml --scaling-policy auto

# Deploy static assets only (faster updates)
uv run deploy.py --environment prod --static-only --source-path ../my-app/dist
```

### Rollback and Recovery

```bash
# List available deployment versions
uv run scripts/list-deployments.py --environment prod

# Rollback to previous version
uv run scripts/rollback.py --environment prod --version v1.2.0

# Emergency cleanup (removes all resources)
uv run scripts/cleanup.py --environment dev --force
```

### Advanced Deployment Scenarios

```bash
# Multi-environment deployment
uv run deploy.py --environment staging --image-tag v1.0.0
uv run deploy.py --environment prod --image-tag v1.0.0

# Container-only deployment (skip static assets)
uv run deploy.py --environment dev --container-only --image-tag latest

# Static-only deployment (skip containers)
uv run deploy.py --environment dev --static-only --source-path ../my-app/dist

# Deployment with custom configuration
uv run deploy.py --environment prod --config custom-prod-config.yaml
```

## 🏗️ Architecture Overview

### Core Components
1. **CLI Interface** (`cli.py`): User-facing command-line tool
2. **Configuration** (`config.py`): Environment and settings management
3. **Container Management** (`containers.py`): OCI Container Instances
4. **Storage Operations** (`storage.py`): Object Storage for static assets
5. **Networking** (`networking.py`): Load balancers and CDN setup

### Deployment Workflow
1. **Build Phase**: React application compilation
2. **Container Phase**: Docker image creation and registry push
3. **Infrastructure Phase**: OCI resource provisioning
4. **Static Assets Phase**: Object Storage upload
5. **Networking Phase**: Load balancer and CDN configuration
6. **Monitoring Phase**: Health checks and status verification

## 🔍 Gap Analysis: Spec vs Implementation

### Implementation Exceeds Specification
- **Rich CLI Experience**: Advanced console output with progress bars
- **Comprehensive Testing**: More extensive test coverage than planned
- **Docker Infrastructure**: Complete containerization setup
- **Error Handling**: Robust exception management and recovery

### Specification Features Not Yet Implemented
- **GitHub Actions Workflow**: CI/CD pipeline automation
- **Advanced CDN Setup**: Currently placeholder implementation
- **Cost Optimization Tools**: Resource monitoring and optimization
- **Security Auditing**: Deployment logging and audit trails

### Architectural Improvements Made
- **Async Support**: Container deployment with async/await patterns
- **Modular Design**: Better separation of concerns than originally planned
- **Type Safety**: Comprehensive type hints and Pydantic validation
- **Modern Python**: uv package management instead of traditional pip/venv

## 🤝 Contributing Guidelines

### For Code Contributors
1. **Setup**: Follow development environment setup above
2. **Testing**: Add tests for new features (`tests/` directory)
3. **Code Quality**: Run `uv run black .` and `uv run mypy .` before committing
4. **Documentation**: Update relevant documentation for changes

### For Documentation Contributors
1. **Specifications**: Update `specs/` for architectural changes
2. **User Guides**: Enhance main README.md for user-facing features
3. **Developer Docs**: Update this README.md for development changes

### Code Standards
- **Python Style**: Follow PEP 8 with Black formatting
- **Type Hints**: Required for all functions and classes
- **Error Handling**: Comprehensive exception handling with logging
- **Testing**: Unit tests required for new features

## 🔗 Related Resources

### External Documentation
- **Oracle Cloud Infrastructure**: [OCI Documentation](https://docs.oracle.com/en-us/iaas/)
- **OCI Python SDK**: [SDK Documentation](https://oracle-cloud-infrastructure-python-sdk.readthedocs.io/)
- **uv Package Manager**: [uv Documentation](https://docs.astral.sh/uv/)

### Internal Resources
- **Main README**: [../README.md](../README.md) - Primary user documentation
- **CLAUDE.md**: [../CLAUDE.md](../CLAUDE.md) - Development instructions for AI assistance
- **Deployment README**: [../deployment/oci-deployment/README.md](../deployment/oci-deployment/README.md) - Deployment-specific guide

## 📞 Support and Feedback

### Getting Help
1. **Issues**: Check common troubleshooting in main README.md
2. **Configuration**: Review environment-specific .env files
3. **Development**: Consult the specification document for implementation details

### Reporting Issues
1. **Bugs**: Create detailed issue reports with reproduction steps
2. **Feature Requests**: Describe use cases and expected behavior
3. **Documentation**: Suggest improvements for clarity and completeness

---

*This documentation is maintained as part of the Infrastructure as Code project. For the most up-to-date information, refer to the main project README and specification documents.*