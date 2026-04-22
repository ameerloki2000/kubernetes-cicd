Three-Tier Application Deployment on Kubernetes (EKS)

This repository demonstrates the end-to-end deployment of a three-tier application using modern DevOps tools and practices. The architecture includes containerization, CI/CD automation, Kubernetes orchestration, GitOps delivery, and observability.

📌 Architecture Overview

The application follows a three-tier architecture:


🛠️ Tech Stack
Containerization: Docker (Dockerfile)

CI/CD: GitHub Actions

Container Registry: AWS ECR (Elastic Container Registry)

Orchestration: Amazon EKS (Elastic Kubernetes Service)

Package Manager: Helm

GitOps Deployment: Argo CD

Ingress Controller: Kubernetes Ingress (NGINX)

Monitoring: Prometheus & Grafana 

-AWS ECR Setup

Created private repositories for:

frontend

backend

<img width="1612" height="708" alt="Screenshot 2026-04-13 144210" src="https://github.com/user-attachments/assets/f625161b-0401-4a91-be0c-03587da1de09" />
<img width="1598" height="693" alt="Screenshot 2026-04-13 144318" src="https://github.com/user-attachments/assets/e3da356e-ac81-42ba-9caf-7e9b5df209b6" />



-CI/CD Pipeline (GitHub Actions)

The pipeline automates:

Build Docker images for frontend & backend

Tag images with commit SHA

Push images to AWS ECR

<img width="1793" height="772" alt="Screenshot 2026-04-13 144107" src="https://github.com/user-attachments/assets/6c0b3c13-9879-4dbd-9277-5a02bee49d40" />

-Kubernetes (EKS)
EKS cluster provisioned using eksctl 
Worker nodes configured
kubectl configured for cluster access

<img width="1605" height="658" alt="Screenshot 2026-04-13 145755" src="https://github.com/user-attachments/assets/f1347b29-83e1-4db1-b44e-8424df225d59" />


-Helming

Helm charts are used to install:

*Argo CD

<img width="1623" height="720" alt="Screenshot 2026-04-13 154055" src="https://github.com/user-attachments/assets/c6e93119-e1f0-406c-80e4-d6701c95f364" />


*Prometheus , *Grafana


<img width="1607" height="795" alt="Screenshot 2026-04-13 164101" src="https://github.com/user-attachments/assets/e6fa5668-091a-461c-93e3-b610d665a464" />


*Ingress


<img width="1517" height="317" alt="Screenshot 2026-04-13 162403" src="https://github.com/user-attachments/assets/d82575d5-d0e0-4227-9426-31b01cac3710" />


-GitOps with Argo CD

<img width="1225" height="722" alt="Screenshot 2026-04-13 155850" src="https://github.com/user-attachments/assets/8da131f9-8ac4-49e4-b8e5-7f26feb2aece" />


Argo CD continuously syncs Kubernetes manifests from GitHub.


<img width="1687" height="797" alt="Screenshot 2026-04-13 154928" src="https://github.com/user-attachments/assets/d13be092-1f8a-4184-af36-401acb5b77ce" />


frontend (deployment, service, ingress)

backend (deployment, service, secret), read by argo cd 

<img width="1253" height="615" alt="Screenshot 2026-04-13 155309" src="https://github.com/user-attachments/assets/d7d692ba-6f69-4ac8-a8de-7e08d8e62c85" />


Automatically deploys them to the cluster

<img width="1528" height="940" alt="Screenshot 2026-04-13 160006" src="https://github.com/user-attachments/assets/3ca32bff-f72e-49bb-ba21-f994cbe1ae8e" />


Keeps cluster state in sync with Git


<img width="1821" height="982" alt="Screenshot 2026-04-13 160439" src="https://github.com/user-attachments/assets/ee61f374-e66f-4bb6-8659-1b6712e6288b" />

Deployed application 

<img width="1486" height="931" alt="Screenshot 2026-04-13 163435" src="https://github.com/user-attachments/assets/d6edc402-8a31-4379-b115-17b7a2b310b4" />

PV is used for database (generally we use RDS)

Monitoring (Prometheus & Grafana)


Prometheus: Metrics collection
<img width="1792" height="936" alt="Screenshot 2026-04-13 172659" src="https://github.com/user-attachments/assets/fcb7c06d-8dde-43f7-afda-fd5d397052c4" />
--------------------------------------------------------------------------------------------------

<img width="1856" height="898" alt="Screenshot 2026-04-13 172735" src="https://github.com/user-attachments/assets/341b7721-26f5-4a12-a72e-11c9f1d79a04" />




Grafana: Visualization dashboards

<img width="1882" height="927" alt="Screenshot 2026-04-13 173027" src="https://github.com/user-attachments/assets/4886aa17-6324-4b4d-9cf6-305633993f21" />


-Security Considerations:


IAM roles for service accounts 


Secrets managed via Kubernetes Secrets


Restricted security groups


--->Deployment Flow:


-Developer pushes code to GitHub


-GitHub Actions builds & pushes Docker images to ECR


-Helm chart is updated with new image tag


-Argo CD detects changes and syncs automatically


-Application is deployed to EKS


-Ingress exposes the application


-Prometheus & Grafana monitor system health

