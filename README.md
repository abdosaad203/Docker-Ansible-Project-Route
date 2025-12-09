# 🚀 Docker + Ansible Automation Project  
A complete 3-tier application deployed using Docker, Docker Compose, and Ansible.

## 📦 Architecture
Frontend (React + Vite) → Nginx Reverse Proxy → Backend (.NET 8 API) → MySQL Database  
All components run in containers and deployment is automated with Ansible.

## 📁 Folder Structure
Docker-Ansible-Project/
├── React-Frontend/
│   ├── Dockerfile
│   ├── nginx.conf
│   └── src/...
├── DotNet-Backend/
│   ├── Dockerfile
│   └── source files
├── docker-compose.yml
├── playbook.yml
├── inventory
└── vars/
    ├── main.yml
    └── secrets.yml (encrypted)

## 🐳 Docker Usage

### Build Frontend Image
cd React-Frontend  
docker build -t abdosaad0/frontend-react:latest .

### Build Backend Image
cd ../DotNet-Backend  
docker build -t abdosaad0/backend-dotnet-api:latest .

## ▶ Run with Docker Compose
docker compose up -d

Open the app:  
http://localhost:8080

Check running containers:  
docker compose ps

## 🔐 Vars Files

### vars/main.yml
DOCKER_USERNAME: "abdosaad0"
images:
  - name: "{{ DOCKER_USERNAME }}/frontend-react"
    tag: "latest"
    path: "./React-Frontend"
  - name: "{{ DOCKER_USERNAME }}/backend-dotnet-api"
    tag: "latest"
    path: "./DotNet-Backend"

### vars/secrets.yml (before encryption)
DB_PASSWORD: "your-db-password"
DOCKER_PASSWORD: "your-dockerhub-password-or-token"

Encrypt with:
ansible-vault encrypt vars/secrets.yml

## 🤖 Ansible Deployment

Install collection:
ansible-galaxy collection install community.docker --force

Run playbook:
ansible-playbook -i inventory playbook.yml --ask-vault-pass

The playbook will:
- Login to Docker Hub
- Build and push both images
- Create db_password.txt
- Run docker compose
- Delete db_password.txt

## 📜 playbook Summary
Automates:
- Docker Hub login
- Building images
- Pushing images
- Creating DB password file
- Running docker compose
- Cleaning secrets

## ✅ Final Result
Frontend → http://localhost:8080  
Backend runs internally on port 8080  
MySQL initialized automatically  
Full deployment using:
ansible-playbook -i inventory playbook.yml --ask-vault-pass

## 🎉 Project Completed
Demonstrates:
- Multi-stage Docker builds
- Docker Compose Networking & Secrets
- Ansible automation
- Secure Credentials Handling with Vault
- Secure Credentials Handling with Vault
