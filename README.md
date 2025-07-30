# INFO8995 - Assignment 3: Gitea CI/CD Deployment on Kubernetes

**Name:** Prem Chander  
**Student ID:** 9015480  
**Program Code:** INFO8995  
**Assignment:** 3 - CI/CD with Gitea & Kubernetes  

---

## 📌 Objective

This assignment demonstrates deploying a self-hosted Gitea Git server on a Kubernetes cluster using Helm and managing port exposure using Ngrok for public access. The goal is to automate Gitea setup and simulate CI/CD integration in a private environment (e.g., GitHub Codespaces or local K3s).

---

## 🏗️ Architecture Overview

- Kubernetes cluster provisioned using **K3s**
- Gitea deployed via **Helm**
- MySQL backend deployed as a custom resource
- Port 3000 exposed externally using **Ngrok**
- DNS-based access via Codespace domain:  
  `https://codespace.premchanderj.me/proxy/3000/`

---

## ⚙️ Steps Followed

### ✅ 1. Clone and Prepare the Repository
git clone https://github.com/jpremchander/info8995-cdevops-gitea.git
cd info8995-cdevops-gitea

## ✅ 2. Add Submodule for Kubernetes Playbooks
git submodule add https://github.com/rhildred/ansible-k8s.git k8s
git submodule update --init --recursive

## ✅ 3. Deploy Kubernetes Cluster and Gitea via Ansible
ansible-playbook up.yml
playbook usecasee:

1. Installs K3s
2. Adds Helm chart repo
3. Deploys Gitea

📸 Screenshot: k8s pods + gitea pods running

<img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/21c78f44-65a2-45aa-b4f2-c2093b032015" />


🐛 Troubleshooting & Fixes

❌ Error: helm not found
Fix:
Installed using Snap:
sudo snap install helm --classic

❌ Error: Git submodule already exists
Fix:
git rm --cached k8s
rm -rf k8s
git submodule add https://github.com/rhildred/ansible-k8s.git k8s

❌ Error: unarchive failed due to missing unzip
Fix:
sudo apt install unzip -y
🗄️ Custom MySQL Backend for Gitea

Created a custom mysql.yml that includes:

PersistentVolumeClaim

Secret with secure credentials

Deployment using MySQL 5.7

Kubernetes Service

📸 Screenshot: MySQL pod running and service active

<img width="2880" height="1704" alt="k8s-mysql-db" src="https://github.com/user-attachments/assets/ff5e7381-8f7e-4cc6-822c-42c6e34d5956" />


🌐 Ngrok Port Forwarding
Created an ngrok-portforward.yml Ansible playbook to:

Download and configure Ngrok

Open a tunnel on port 3000

Retrieve and display public Ngrok URL

📸 Screenshot: Ngrok public URL showing Gitea in browser
<img width="2880" height="1704" alt="image" src="https://github.com/user-attachments/assets/8de93511-2137-4fe3-86d5-42db2071e90f" />

📸 Screenshot: Accessing Gitea via Codespace Proxy
<img width="2880" height="1704" alt="ngrok-url" src="https://github.com/user-attachments/assets/abda190a-8239-4df5-95bc-620eec3728b1" />




✅ Clean-Up
to down the environment:

ansible-playbook down.yml
