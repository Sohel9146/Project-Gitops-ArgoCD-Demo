# 🚀 GitOps HTML App with ArgoCD

[![Docker Pulls](https://img.shields.io/docker/pulls/sohel7866/gitops-html.svg)](https://hub.docker.com/r/sohel7866/gitops-html)
[![ArgoCD](https://img.shields.io/badge/Managed%20By-ArgoCD-brightgreen)](https://argoproj.github.io/)
[![License](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Stars](https://img.shields.io/github/stars/Sohel9146/Project-Gitops-ArgoCD-Demo.svg)](https://github.com/Sohel9146/Project-Gitops-ArgoCD-Demo/stargazers)
[![Forks](https://img.shields.io/github/forks/Sohel9146/Project-Gitops-ArgoCD-Demo.svg)](https://github.com/Sohel9146/Project-Gitops-ArgoCD-Demo/network/members)


A **GitOps demo project** that deploys a simple HTML application using **Docker** and **ArgoCD** on **Kubernetes** (via Minikube).  
This project demonstrates **continuous delivery using Git as the single source of truth**.

---

## 📋 Table of Contents
- [Features](#-Features)
- [Tech Stack](#-Tech-Stack)
- [Prerequisites](#-Prerequisites)
- [Installation](#-Installation & Deployment)
- [Usage](#-Usage)
- [Architecture](#-architecture)
- [GitOps Version Updates](#-gitops-in-action--version-updates)
- [Project Structure](#project-structure)
- [Screenshots](#screenshots)
- [Use Case / Why This Project Matters](#-use-case--why-this-project-matters) 
- [Key Learnings](#-key-learnings)
- [Future Enhancements / Roadmap](#-roadmap)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#contributing)
- [Author](#-author)

---

## ✅ Features
- ✔️ Dockerized HTML application for easy container deployment  
- ✔️ Continuous Delivery with **ArgoCD** (GitOps approach)  
- ✔️ Kubernetes deployment using **Minikube**  
- ✔️ Demonstrates **auto-sync** and **manual sync** in GitOps  

---

## 🛠 Tech Stack
- **Languages**: HTML, CSS  
- **Containerization**: Docker  
- **Orchestration**: Kubernetes (Minikube)  
- **GitOps Tool**: ArgoCD  
- **Version Control**: Git + GitHub  

---

## 🛠 Prerequisites
Before starting, ensure you have:
- [Git](https://git-scm.com/)
- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- (Optional) [ArgoCD CLI](https://argo-cd.readthedocs.io/en/stable/cli_installation/)

---

## ⚙️ Installation & Deployment

### 1. Clone the Repository
```bash
git clone https://github.com/Sohel9146/Project-Gitops-ArgoCD-Demo.git
cd Project-Gitops-ArgoCD-Demo
```

### 2. Build and Push the Docker Image
```bash
cd app
docker build -t sohel7866/gitops-html:v1.0.0 .
docker push sohel7866/gitops-html:v1.0.0
```

### 3. Install ArgoCD in Kubernetes
```bash
kubectl create namespace argocd
kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml
```

### 4. Access the ArgoCD UI
```bash
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
Now, open:  
👉 `https://localhost:8080`  
Default username: `admin`  
Get the initial password:
```bash
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
```

### 5. Deploy the App with ArgoCD
```bash
kubectl create namespace gitops-html
kubectl apply -f argocd/application.yaml -n argocd
```

### 6. Access the HTML App
```bash
minikube service gitops-html -n gitops-html
```

---

## ▶️ Usage
- Navigate to the Minikube service URL to view the deployed **HTML App**.
- Open **ArgoCD UI** to check application sync status and manage deployments.

---

## 🏗 Architecture
![Architecture Diagram](./screenshots/Architecture%20Diagram.png)  
**Workflow:**  
`GitHub Repository` → `ArgoCD Controller` → `Kubernetes Cluster` → `HTML App`

---

## 🔄 GitOps in Action – Version Updates
This project demonstrates **real GitOps workflow** by updating the application version via Git commits.

### ✅ How it works:
1. Update the image version in `kustomization.yaml` (e.g., `v1.0.0` → `v4.0.0` → `v5.0.0`).
2. Commit and push the changes to GitHub.
3. ArgoCD detects the change and updates the cluster automatically (or via manual sync).

**Versions Tested:**  
- Initial: `v1.0.0`
- Updated: `v2.0.0`, `v3.0.0`, `v4.0.0`, `v5.0.0`

---

## 📂 Project Structure
```
├── app/                # HTML app source and Dockerfile
├── argocd/             # ArgoCD application definition and manifests
├── screenshots/        # All screenshots for README
└── README.md           # Project overview and instructions
```

---

## 📸 Screenshots
- **ArgoCD Dashboard (Synced State)**  
![ArgoCD Dashboard](./screenshots/ArgoCD%20Dashboard.png)

- **HTML App light Mode**  
![App Light Mode](./screenshots/HTML%20App%20Light%20Mode.png)

- **HTML App Dark Mode**  
![App Dark Mode](./screenshots/HTML%20App%20Dark%20Mode.png)

- **ArgoCD Version 5.0.0 is Syncing**  
![Version 5.0.0 Syncing](./screenshots/Version%205%20Syncing.png)

- **ArgoCD Version 5.0.0 is Synced**  
![Version 5.0.0 Syncing](./screenshots/Version%205%20Synced.png)

---

## 💡 Use Case / Why This Project Matters

This project demonstrates the power of **GitOps with ArgoCD** — where Git becomes the single source of truth for Kubernetes deployments.  
Instead of manually applying YAML files or editing clusters, every change is version-controlled, auditable, and automatically synced.  

✅ **Real-world relevance:**  
- Teams avoid **configuration drift** between environments.  
- Every deployment is **traceable** to a Git commit.  
- Ensures **faster, safer, and repeatable** application delivery.  

In short, this project shows how modern DevOps teams manage Kubernetes apps in production-like environments.


---

## 📚 Key Learnings
- Implemented GitOps principles using **ArgoCD**
- Automated deployments using **Git as the single source of truth**
- Gained hands-on experience with **Kubernetes**, **Minikube**, and **Docker**
- Learned how **ArgoCD syncs deployments automatically**

---

## 🔮 Roadmap
- [ ] CI/CD pipeline with GitHub Actions  
- [ ] HTTPS with Ingress + TLS  
- [ ] Multi-environment support (Dev/Staging/Prod)  
- [ ] Deployment on AWS EKS  

---

## ❓ Troubleshooting
- **ArgoCD app stuck in OutOfSync?** → Click **Sync Now** in UI or run `argocd app sync <app-name>`.  
- **Can't access ArgoCD UI?** → Ensure `kubectl port-forward` is running and visit `https://localhost:30080`.  
- **Image not updating?** → Confirm the updated tag is pushed to Docker Hub and referenced in `kustomization.yaml`.  

---

## 🤝 Contributing
Contributions are welcome!  
To contribute:
1. Fork this repo
2. Create your feature branch (`git checkout -b feature/...`)
3. Commit your changes (`git commit -m 'Add something new'`)
4. Push to your branch (`git push origin feature/...`)
5. Open a Pull Request

---

## 👨‍💻 Author
**Shaikh Sohel**  
[GitHub](https://github.com/Sohel9146) | [Naukri](https://www.naukri.com/mnjuser/profile) 

---

