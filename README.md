# 📘 Ansible Automation Cookbook

**Author:** Ghanshyam Ramole  
**Repository:** [Ansible-cookbook](https://github.com/GhanshyamRamole/Ansible-cookbook)

## 🚀 Overview

This repository is a comprehensive collection of **Ansible projects, roles, and playbooks** designed to automate various DevOps tasks. It covers a wide spectrum of automation needs, including **Docker Swarm clustering**, **CI/CD pipelines for containerized apps**, **AWS infrastructure provisioning**, and **general system administration** on RHEL/CentOS and Debian systems.

Whether you are looking for production-ready deployment scripts or learning materials for Ansible control structures, this cookbook serves as a central reference.

---

## 📂 Repository Structure

The repository is organized into distinct projects and utility categories:

| Directory | Description |
| :--- | :--- |
| **`DockSwarm-Ansible/`** | Full project to provision a **Docker Swarm Cluster** (Manager & Workers). |
| **`DockOps-Ansible/`** | **CI/CD Pipeline** to build, push, and deploy Docker containers from Git sources. |
| **`roles/`** | Reusable, modular Ansible roles (e.g., `nginx`). |
| **`aws-provision/`** | Playbooks for managing **AWS EC2** lifecycles (Create, Start, Stop, Terminate). |
| **`Playbooks/`** | Collection of standalone utility playbooks for system tasks (HTTPD, VSFTPD, Firewalld). |
| **`task-control/`** | Learning examples for Ansible logic (Loops, Conditions, Handlers). |
| **`vault/`** | Examples and cheatsheets for securing secrets with **Ansible Vault**. |

---

## 🛠️ Major Projects

### 1. DockSwarm-Ansible (Docker Swarm Cluster)
A dedicated project to bootstrap a multi-node Docker Swarm cluster automatically.

* **Location:** `DockSwarm-Ansible/`
* **Roles Included:**
    * `docker`: Installs Docker and configures the daemon.
    * `swarm-manager`: Initializes the Swarm and generates join tokens.
    * `swarm-worker`: Joins worker nodes to the cluster using the generated token.
* **Key Files:** `playbook.yml`, `inventory`.

### 2. DockOps-Ansible (Container Deployment Pipeline)
An automated pipeline for deploying web applications using Docker.

* **Location:** `DockOps-Ansible/`
* **Workflow:**
    1.  Installs Git & Docker.
    2.  Clones source code from a remote Git repository.
    3.  Builds a Docker image from the source.
    4.  Logs in and pushes the image to **Docker Hub**.
    5.  Deploys the container with port mapping.
* **Configuration:** Managed via `vars.yml` (repo URL, image tags) and `vault.yml` (credentials).

---

## 🧩 Modular Roles

### Nginx Role
A production-ready role to deploy and configure the Nginx web server on RHEL/CentOS.

* **Location:** `roles/nginx/`
* **Features:**
    * Installs EPEL release and Nginx packages.
    * Configures **Firewalld** to allow HTTP traffic.
    * Deploys custom `nginx.conf` via Jinja2 templates.
    * Deploys a custom `index.html` website.
    * Includes handlers for service restarts.

---

## ⚡ Utility Playbooks

Located in the `Playbooks/` directory, these scripts handle specific administrative tasks:

* **Web Servers:**
    * `installhttpd.yaml` / `removehttpd.yaml`: Lifecycle management for Apache HTTPD.
    * `nginx.yaml` / `removenginx.yaml`: Lifecycle management for Nginx.
    * `httpd-vsftpd.yaml`: Installs and configures both HTTPD and VSFTPD servers.
* **System Config:**
    * `firewalld.yaml`: Manages firewall services.
    * `packages-install.yml`: Bulk installation of essential tools (git, wget, vim).

---

## ☁️ AWS Provisioning

Located in `aws-provision/`, these playbooks automate AWS infrastructure interactions using the `amazon.aws.ec2_instance` module.

* `create_ec2.yml`: Launches new EC2 instances with specific tags and security groups.
* `start_ec2.yml` / `stop_ec2.yml`: Manages instance power states.
* `terminate_ec2.yml`: Destroys specified instances.

---

## 📚 Learning Resources

### Task Control & Logic (`task-control/`)
Examples demonstrating Ansible's control structures:
* **Loops:** Iterating over simple lists (`loop.yml`) and lists of hashes (`looplist.yml`).
* **Conditions:** Using `when` for OS-specific tasks (Debian vs. RedHat).
* **Handlers:** Triggering service restarts on configuration changes.

### Security (`vault/`)
* Includes a **Cheat Sheet** (`manage_vault`) for common Vault commands (encrypt, decrypt, rekey).
* Examples of encrypted playbooks and variable files.

---

## ⚙️ Usage

### Prerequisites
* Ansible installed on the control node.
* Target nodes configured with SSH access (key-based auth recommended).
* User with `sudo` privileges.

### Running a Project (Example: DockOps)
1.  Navigate to the directory:
    ```bash
    cd DockOps-Ansible
    ```
2.  Update `inventory` with your target IPs.
3.  Run the playbook (with Vault password if secrets are used):
    ```bash
    ansible-playbook -i inventory playbook.yml --ask-vault-pass
    ```

### Running a Standalone Playbook
```bash
ansible-playbook Playbooks/installhttpd.yaml
```
