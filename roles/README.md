# Ansible Role: Multi-Task Nginx Deployment on RHEL/CentOS

This project demonstrates a **modular Ansible role** to deploy and configure **Nginx** on Red Hat Enterprise Linux (RHEL) / CentOS servers using multiple tasks.  
It follows best practices using **roles, templates, handlers, and variables**.

---

## 📂 Project Structure

ansible-nginx-rhel/
├── ansible.cfg
├── inventory.ini
├─�role_playbook.yml
└── es/
└── nginx/
├── tasks/
│ ├─�nstall.yml
│ ├── configure.yml
│ ├─�eploy.yml
│ └── main.yml
├── handlers/
│ └── main.yml
├── templates/
│ └── nginx.conf.j2
├── files/
│ └── index.html
├── vars/
│ └── main.yml
└── defaults/
└── mayml


---

## ⚙️ Features

- Installs **Nginx** using `yum` (with EPEL repository if required).  
- Configures **firewalld** to allow HTTP traffic on port 80.  
- Deploys a custom website (`index.html`) to `/usr/share/nginx/html`.  
- Configures Nginx using a **template file** (`nginx.conf.j2`).  
- Ensures Nginx service is **enabled and running**.  
- Modular role with **multiple tasks** (`install`, `configure`, `deploy`).  
- Includes **handlers** to restart Nginx on configuration changes.  
- Fully compatible with **RHEL/CentOS** servers.  

---

## 📝 Prerequisites

- Ansible >= 2.9  
- RHEL/CentOS server(s) with SSH access  
- Python installed on managed nodes  
- User with **sudo privileges**  

---

## 🛠️ Setup & Run

1. **Configure inventory** (`inventory.ini`) with your server IP and SSH key:

```ini
[webservers]
192.168.56.20 ansible_user=centos ansible_ssh_private_key_file=~/.ssh/id_rsa

2. Run the playbook:

```bash
 ansible-playbook role_playbook.yml
```

3. Access the website:

Open your browser: http://<server-ip>
You should see the custom index page deployed by Ansible.

📌 Variables

nginx_port: Port on which Nginx will listen (default: 80)

Can be modified in roles/nginx/vars/main.yml

🔧 Tech Stack

Ansible: Automation & orchestration

Nginx: Web server

RHEL/CentOS: Target OS

YAML: Playbooks, roles, templates

✅ Advantages

Modular and reusable role for multiple servers

Easy to extend (SSL, reverse proxy, load balancer)

Production-ready multi-task role structure
