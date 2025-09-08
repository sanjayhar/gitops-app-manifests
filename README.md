# GitOps Workflow using ArgoCD on Kubernetes

## Project Overview
This project demonstrates a **GitOps workflow** by syncing Kubernetes deployment states directly from a Git repository using **ArgoCD**. Any updates to Kubernetes manifests in the GitHub repository are automatically applied to the cluster, enabling a fully automated deployment process.

---

## Objective
Implement GitOps by:

- Managing Kubernetes manifests in a Git repository.
- Deploying applications automatically via ArgoCD.
- Observing changes in real-time by updating manifests and watching ArgoCD sync.

---

## Tools Used
- **Kubernetes** (Minikube/K3s)
- **ArgoCD** (Free/Open Source)
- **GitHub** (Repository for manifests)
- **kubectl** (CLI for Kubernetes management)
- **Docker** (for container images)

---

## Repo Structure

gitops-app-manifests/

│── base/

│ ├── deployment.yaml # Kubernetes Deployment manifest

│ └── service.yaml # Kubernetes Service manifest

│── app.yaml # ArgoCD Application manifest

│── README.md # This documentation


- `base/` contains all Kubernetes manifests for the application.
- `app.yaml` configures ArgoCD to watch the repository and auto-sync the application.

---

## Steps Involved in Building the Project

1. **Setup Kubernetes cluster**  
   - Install Minikube or K3s on your local machine.

2. **Deploy ArgoCD on Kubernetes**  
   ```bash
   kubectl create namespace argocd
   kubectl apply -n argocd -f https://raw.githubusercontent.com/argoproj/argo-cd/stable/manifests/install.yaml

3. **Create ArgoCD Application**

Use app.yaml to configure ArgoCD to monitor the base/ folder in the GitHub repo.

4. **Push manifests to GitHub**

Add or update Kubernetes manifests:
```
git add .
git commit -m "Initial deployment"
git push origin main
```

5. **Sync and observe changes in ArgoCD**

ArgoCD UI shows application status (Synced & Healthy).

Update manifests (e.g., change image version), commit, and push → ArgoCD automatically applies changes.
