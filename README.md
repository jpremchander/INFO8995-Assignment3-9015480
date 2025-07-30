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

```bash
git clone https://github.com/jpremchander/info8995-cdevops-gitea.git
cd info8995-cdevops-gitea
✅ 2. Add Submodule for Kubernetes Playbooks
bash
Copy
Edit
git submodule add https://github.com/rhildred/ansible-k8s.git k8s
git submodule update --init --recursive
✅ 3. Deploy Kubernetes Cluster and Gitea via Ansible
bash
Copy
Edit
ansible-playbook up.yml
This playbook:

Installs K3s

Adds Helm chart repo

Deploys Gitea

Sets up Ingress

📸 Add Screenshot: k8s pods + gitea pods running

🐛 Troubleshooting & Fixes
❌ Error: helm not found
Fix:
Installed using Snap:

bash
Copy
Edit
sudo snap install helm --classic
❌ Error: Git submodule already exists
Fix:

bash
Copy
Edit
git rm --cached k8s
rm -rf k8s
git submodule add https://github.com/rhildred/ansible-k8s.git k8s
❌ Error: unarchive failed due to missing unzip
Fix:

bash
Copy
Edit
sudo apt install unzip -y
🗄️ Custom MySQL Backend for Gitea
Created a custom mysql.yml that includes:

PersistentVolumeClaim

Secret with secure credentials

Deployment using MySQL 5.7

Kubernetes Service

📸 Add Screenshot: MySQL pod running and service active

🌐 Ngrok Port Forwarding
Created an ngrok-portforward.yml Ansible playbook to:

Download and configure Ngrok

Open a tunnel on port 3000

Retrieve and display public Ngrok URL

📸 Add Screenshot: Ngrok public URL showing Gitea in browser
📸 Add Screenshot: Accessing Gitea via Codespace Proxy
📸 Add Screenshot: Ngrok page loading the Gitea login screen

🔗 Final Access URLs
✅ Ngrok URL: (Insert screenshot showing the https://xxxx.ngrok-free.app)

✅ Codespace Proxy: https://codespace.premchanderj.me/proxy/3000/

✅ Clean-Up
To tear down the environment:

bash
Copy
Edit
ansible-playbook down.yml