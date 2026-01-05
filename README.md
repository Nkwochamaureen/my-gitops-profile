# My-Gitops-Profile
# Local GitOps-Managed Personal Profile

This project demonstrates a fully automated, GitOps-driven **"production-like" environment** running entirely on a local machine. It bridges the gap between manual deployments and modern cloud-native automation.

---

## 🏗️ Project Overview

The goal of this project is to host a personal profile page where the **Desired State** is defined entirely in Git. By utilizing **Argo CD** and **Kubernetes**, any change pushed to this repository is automatically synchronized to the local cluster **without running a single manual `kubectl` command**.

---

## 🔁 The GitOps Intention

This project implements **declarative infrastructure management**. By treating the Git repository as the **Single Source of Truth**, we ensure that the live environment always matches our code.

This workflow provides:

- **Self-Healing**  
  If a deployment is manually altered or deleted, Argo CD detects the *Out of Sync* state and automatically restores it.

- **Version Control for Infrastructure**  
  Every change to server resources (CPU/RAM) or application versions is tracked via Git commits.

- **Zero-Touch Continuous Deployment**  
  Updates move from code to production automatically upon `git push`.

---

## 🛠️ Tech Stack

- **Application:** Nginx-based static HTML profile page  
- **Containerization:** Docker (image hosted on Docker Hub)  
- **Orchestration:** K3d (lightweight Kubernetes/K3s running in Docker)  
- **GitOps Engine:** Argo CD  
- **CI/CD Workflow:** Manual image build + Git-triggered Continuous Deployment  

---

## 🚀 How It Works

1. **Code**  
   Changes are made to `app/index.html` or Kubernetes manifests in `k8s/`.

2. **Build**  
   A new Docker image is built and pushed to Docker Hub:  
   `nkwocha1234/profile-page`

3. **Push**  
   The `k8s/deployment.yaml` file is updated with the new image tag and pushed to GitHub.

4. **Sync**  
   Argo CD (watching the `main` branch) detects a difference between Git and the cluster.

5. **Deploy**  
   Argo CD automatically pulls and applies the changes to the K3d cluster.


