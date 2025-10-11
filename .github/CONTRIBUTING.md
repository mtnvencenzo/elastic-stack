# 🔍 Contributing to Elastic Stack

Thank you for your interest in contributing to our Elastic Stack with OpenTelemetry Collector project! We welcome contributions that help improve our observability setup and expand our monitoring capabilities.

## 📋 Table of Contents

- [Getting Started](#-getting-started)
- [Development Setup](#-development-setup)
- [Contributing Process](#-contributing-process)
- [Configuration Standards](#-configuration-standards)
- [Testing](#-testing)
- [Getting Help](#-getting-help)

## 🚀 Getting Started

### 🧰 Prerequisites

Before you begin, ensure you have the following installed:
- [Docker](https://docs.docker.com/get-docker/) and [Docker Compose](https://docs.docker.com/compose/)
- Git
- Basic understanding of Elastic Stack (Elasticsearch, Kibana, APM)
- Familiarity with OpenTelemetry concepts

### 🗂️ Project Structure

```
├── docker-compose.yml          # Main Docker Compose configuration
├── otel-collector-config.yml   # OpenTelemetry Collector configuration
├── assets/                     # Documentation assets and diagrams
├── .github/                    # GitHub workflows and templates
└── README.md                   # Project overview and setup guide
```

## 💻 Development Setup

1. **Fork and Clone the Repository**
   ```bash
   git clone https://github.com/mtnvencenzo/elastic-stack.git
   cd elastic-stack
   ```

2. **Test the Current Setup**
   ```bash
   # Start the stack
   docker compose -p elastic-stack -f docker-compose.yml up -d
   
   # Check service health
   docker compose -p elastic-stack -f docker-compose.yml ps
   
   # View logs
   docker compose -p elastic-stack -f docker-compose.yml logs
   
   # Stop the stack
   docker compose -p elastic-stack -f docker-compose.yml down -v
   ```

3. **Validate Configuration**
   ```bash
   # Validate Docker Compose syntax
   docker compose -f docker-compose.yml config
   
   # Check OpenTelemetry Collector config
   docker run --rm -v $(pwd)/otel-collector-config.yml:/etc/otel-collector-config.yml \
     otel/opentelemetry-collector:latest --config-validate --config=/etc/otel-collector-config.yml
   ```

## 🔄 Contributing Process

### 1. 📝 Before You Start

- **Check for existing issues** to avoid duplicate work
- **Create or comment on an issue** to discuss your proposed changes
- **Wait for approval** from maintainers before starting work (required for this repository)

### 2. 🛠️ Making Changes

1. **Create a feature branch**
   ```bash
   git checkout -b feature/new-configuration
   # or
   git checkout -b fix/collector-issue
   ```

2. **Make your changes** following our [configuration standards](#-configuration-standards)

3. **Test your changes**
   ```bash
   # Validate Docker Compose
   docker compose -f docker-compose.yml config
   
   # Test the stack
   docker compose -p elastic-stack-test -f docker-compose.yml up -d
   
   # Check services are healthy
   curl -f http://localhost:9200/_cluster/health
   curl -f http://localhost:5601/api/status
   
   # Test OpenTelemetry endpoint
   curl -f http://localhost:4317/v1/health
   
   # Clean up test
   docker compose -p elastic-stack-test -f docker-compose.yml down -v
   ```

4. **Update documentation**
   - README.md with any new features or changes
   - Configuration comments for complex settings
   - Asset diagrams if architecture changes

5. **Commit your changes**
   ```bash
   git add .
   git commit -m "feat: add new OpenTelemetry processor configuration"
   ```

### 3. 📬 Submitting Changes

1. **Push your branch**
   ```bash
   git push origin feature/new-configuration
   ```

2. **Create a Pull Request**
   - Use our [PR template](./pull_request_template.md)
   - Fill out all sections completely
   - Link related issues using `Closes #123` or `Fixes #456`
   - Request review from maintainers

## 📏 Configuration Standards

### 🔍 Observability Best Practices

- **Service Discovery**: Use proper service names and networking
- **Resource Limits**: Set appropriate memory and CPU limits for containers
- **Health Checks**: Include health checks for all services
- **Security**: Follow Docker security best practices
- **Documentation**: Comprehensive comments in configuration files

### 🧪 Code Quality

```bash
# Validate Docker Compose
docker compose config

# Test service startup
docker compose up -d --wait

# Check service health
docker compose ps

# View service logs
docker compose logs
```

## 🆘 Getting Help

### 📡 Communication Channels

- **Issues**: Use GitHub issues for bugs and feature requests
- **Discussions**: Use GitHub Discussions for questions and ideas
- **Email**: Contact maintainers directly for sensitive issues

### 📄 Issue Templates

Use our issue templates for:
- [Task Stories](./ISSUE_TEMPLATE/task-template.md)
- [User Stories](./ISSUE_TEMPLATE/user-story-template.md)
- [Bug Reports](./ISSUE_TEMPLATE/bug_report.md)

## 📜 License

By contributing to this project, you agree that your contributions will be licensed under the same license as the project (see [LICENSE](../LICENSE)).

---

**Happy Observability Building! 🔍**

For any questions about this contributing guide, please open an issue or contact the maintainers.
