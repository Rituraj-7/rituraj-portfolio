Project: Rituraj Portfolio Deployment with Jenkins and K3s

description: >
  This repository contains the complete setup to deploy a personal portfolio website
  using a CI/CD pipeline powered by Jenkins, Docker, and a K3s Kubernetes cluster.
  The goal is to automate building, pushing, and deploying the React app
  with minimal manual intervention.

contents:
  - Dockerfile: Used to build a production-ready Docker image of the React portfolio.
  - Jenkinsfile: Defines the CI/CD pipeline stages (build, push, deploy).
  - deployment.yaml: Kubernetes deployment spec to run the app inside a K3s cluster.
  - service.yaml: Exposes the app using a NodePort service for browser access.

how_it_works: >
  1. Code is pushed to GitHub.
  2. Jenkins pulls the code using the Jenkinsfile logic.
  3. It builds a Docker image and pushes it to Docker Hub.
  4. Kubernetes deployment and service files are applied to a K3s cluster.
  5. The service is exposed on a NodePort, and the app is accessible via the EC2 public IP.

prerequisites:
  - A K3s cluster running (tested on an EC2 instance).
  - Jenkins installed and configured with:
      - Docker
      - kubectl
      - KUBECONFIG from the K3s cluster
  - DockerHub credentials stored in Jenkins.
  - GitHub repo with Jenkinsfile and manifests.

how_to_access:
  - Run `kubectl get svc` to find the NodePort (e.g., 30080).
  - Open browser: http://Ec2publicip:30080

common_issues:
  - App not loading in browser? Check EC2 inbound rules for the NodePort.
  - Pods not starting? Use `kubectl describe pod` and `kubectl logs` for debugging.
  - Jenkins errors? Validate Docker and kubeconfig credentials.

future_plan:
  - Argo CD GitOps integration for full automation and visualization of deployments.

maintainer: Rituraj
<img width="498" height="253" alt="image" src="https://github.com/user-attachments/assets/b6520767-2d8f-4b52-9d39-130e8834bdf3" />

<img width="958" height="956" alt="image" src="https://github.com/user-attachments/assets/f5b1c6ad-aa0f-4253-a588-e884aaae95b7" />
