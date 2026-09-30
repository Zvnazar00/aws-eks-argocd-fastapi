# AWS EKS + ArgoCD + FastAPI (GitOps Deployment)

DevOps project: a full cycle of provisioning Kubernetes infrastructure on AWS EKS and deploying a containerized application through a GitOps workflow with ArgoCD.

## What's implemented

- **Infrastructure (Terraform)**:
  - EKS cluster with worker nodes (`eks-cluster.tf`, `eks-worker-nodes.tf`)
  - VPC with private/public subnets (`vpc.tf`)
  - IAM roles and policies (`iam.tf`)
  - Security Groups (`sg.tf`)
  - EBS CSI Driver for persistent volumes (`ebs-csi.tf`)
  - Nginx Ingress Controller (`ingress_controller.tf`)
  - External DNS for automatic domain registration in Route53 (`eks-external-dns.tf`)
  - ACM certificates for HTTPS (`acm.tf`)
  - ArgoCD, deployed via the Helm provider (`argocd.tf`)
  - Remote state backend (`backend.tf`)

- **Application**: a simple **FastAPI** backend (`Src/main.py`) that returns the pod's name and IP — handy for verifying that load balancing/deployment in Kubernetes actually work.

- **Kubernetes manifests** (`k8s/`): Deployment, Service and Ingress to expose the application through nginx-ingress with automatic DNS.

- **Docker**: containerization of the FastAPI application (`Dockerfile`).

## Tech stack

`Terraform` · `AWS EKS` · `Kubernetes` · `ArgoCD` · `Helm` · `Nginx Ingress` · `External DNS` · `Docker` · `Python / FastAPI`

## Architecture

1. Terraform provisions the VPC, EKS cluster and all related AWS resources.
2. ArgoCD (a GitOps controller) is deployed into the cluster via Helm.
3. Nginx Ingress Controller and External DNS automatically expose services with DNS records.
4. The FastAPI application is built into a Docker image and deployed to the cluster via Kubernetes manifests.
5. Ingress with an ACM certificate provides HTTPS access to the application.

## Repository structure

```
Src/
├── main.py                 # FastAPI application
├── requirements.txt
├── Dockerfile
├── k8s/                    # Kubernetes manifests (Deployment, Service, Ingress)
└── terraform/               # IaC for EKS, VPC, ArgoCD, ingress, DNS, ACM
Screens/                     # Screenshots of the deployment process
```

## Screenshots

Screenshots of the deployment and verification process are in the `Screens/` folder.
