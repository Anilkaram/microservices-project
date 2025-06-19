🚀 Microservices Deployment Using Jenkins & EKS
This project demonstrates deploying a microservices architecture using Jenkins CI/CD and AWS EKS.

📁 Project Structure
13 Branches: Each branch contains:
Microservice code
Its own Dockerfile
Its own Jenkinsfile

main Branch:
Contains Kubernetes manifests for EKS deployment
Central orchestration for final deployment

🛠️ Step-by-Step Setup Guide

1. EC2 Instance Setup (Jenkins Master)
Launch a new EC2 (Amazon Linux 2 / Ubuntu) instance.
install docker & jenkins
install AWS CLI, eksctl, kubectl
Install additional tools: Trivy

2. Create and Configure EKS Cluster
3. Jenkins Configurations
Install Jenkins Plugins:
Docker Pipeline
Git
Multibranch Pipeline
Kubernetes CLI Plugin
Pipeline Utility Steps

Create Jenkins Credential:
Type: Username with password
ID: dockerhub-creds
Use: For docker login in Jenkinsfiles

4. Multibranch Pipeline Setup
Go to Jenkins > New Item > Multibranch Pipeline
Configure:
Source: Git (e.g., GitHub repo URL)
Credentials: Add Git credentials if private repo
Branches: Jenkins will automatically scan and create jobs for all 13 branches
Script Path: Jenkinsfile (default per branch)

5. Pipeline Workflow (Per Branch)
Each branch does the following in its Jenkinsfile
Checkout code
Build Docker image
Run Trivy scan
Push image to Docker Hub

6. Deployment to EKS (from main branch)
The main branch contains all Kubernetes YAML manifests for the services
Final stage of CI/CD in main/Jenkinsfile:
sh '''
  kubectl apply -f k8s/
'''

📦 Folder Structure
├── branch-1/
│   ├── Dockerfile
│   └── Jenkinsfile
├── branch-2/
│   ├── Dockerfile
│   └── Jenkinsfile
...
├── main/
│   ├── Jenkinsfile
│   └── k8s/
│       ├── service-a-deployment.yaml
│       ├── service-b-deployment.yaml
│       └── ...

✅ Highlights
🚀 Microservices built & deployed independently

🔐 Scanned for vulnerabilities using Trivy

🐳 Docker images pushed to Docker Hub

☸️ Deployed to AWS EKS via manifests in main branch

🔄 Fully automated via Jenkins Multibranch Pipeline
# CI pipeline(build, scan, push to Dockerhub)
![image](https://github.com/user-attachments/assets/753b1c67-6cd8-4c8e-bbf0-ec20f12da14d)
# CD(deploy, slack, Monitoring)
![image](https://github.com/user-attachments/assets/2ce84b61-cc87-4194-9a38-ba8ea1997729)
# Application output
![image](https://github.com/user-attachments/assets/3b263d94-8a9e-4699-9bf6-fdb51bc9657c)
# Intregrate Slack
![Screenshot (226)](https://github.com/user-attachments/assets/5c96e7c0-83e5-47e8-adf4-b181882dbe05)

