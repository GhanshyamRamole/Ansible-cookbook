# DockOps-Ansible

Automated Docker deployment pipeline using Ansible for containerized web applications.

## Overview

This project automates the deployment of web applications using Docker containers with Ansible. It handles the complete workflow from source code cloning to Docker image building, pushing to Docker Hub, and container deployment.

## Features

- Automated Docker installation and configuration
- Git repository cloning
- Docker image building from source
- Docker Hub integration for image registry
- Container deployment with port mapping
- Ansible Vault for secure credential management

## Prerequisites

- Ansible installed on control machine
- Target hosts with SSH access
- Docker Hub account
- Git repository with Dockerfile

## Project Structure

```
DockOps-Ansible/
├── playbook.yml          # Main deployment playbook
├── pull-and-deploy.yml   # Additional deployment tasks
├── vars.yml              # Configuration variables
├── vault.yml             # Encrypted credentials
├── inventory             # Target hosts configuration
└── ansible.cfg           # Ansible configuration
```

## Configuration

### Variables (vars.yml)
- `repo_url`: Git repository URL
- `repo_dir`: Local directory for cloned code
- `image_name`: Docker image name
- `image_tag`: Docker image tag
- `container_name`: Running container name
- `app_port`: Application port

### Vault (vault.yml)
Encrypted file containing:
- Docker Hub credentials
- Other sensitive configuration

## Usage

1. **Configure inventory**:
   ```bash
   # Edit inventory file with target hosts
   vim inventory
   ```

2. **Set variables**:
   ```bash
   # Update vars.yml with your configuration
   vim vars.yml
   ```

3. **Create vault**:
   ```bash
   # Create encrypted vault for credentials
   ansible-vault create vault.yml
   ```

4. **Run deployment**:
   ```bash
   # Deploy application
   ansible-playbook -i inventory playbook.yml --ask-vault-pass
   ```

## Playbook Tasks

1. Install required packages (git, docker)
2. Start and enable Docker service
3. Clone application source code
4. Build Docker image from source
5. Login to Docker Hub
6. Push image to registry
7. Deploy container with port mapping

## Security

- Credentials stored in Ansible Vault
- SSH key-based authentication recommended
- Docker daemon secured with proper permissions

## Requirements

- Ansible 2.9+
- Python docker module
- Target hosts: RHEL/CentOS with yum package manager

## License

MIT License
