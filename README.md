# 🏥 Doctor's Office Appointment System on AWS EKS

A scalable, secure, and containerized microservices-based web application deployed using Amazon EKS. This project enables patients to schedule doctor appointments via a responsive frontend, a Node.js backend, and a MongoDB database — all orchestrated through Kubernetes on AWS.

🌐 **Live URL**: [https://doctorapp-group3enpm818r.site](https://doctorapp-group3enpm818r.site)

---

## 📦 Project Overview

- **Frontend**: ReactJS (Create React App), deployed in a Kubernetes deployment with external ALB access.
- **Backend**: Node.js with Express and Mongoose for API and MongoDB interaction.
- **Database**: MongoDB deployed as a StatefulSet with persistent EBS volumes.
- **Deployment**: Kubernetes cluster managed via Amazon EKS.
- **CI/CD**: GitHub Actions with AWS ECR, EKS, and IAM integration.
- **Monitoring**: AWS CloudWatch Container Insights, Application Signals, and alerts.
- **Security**: TLS via AWS Certificate Manager (ACM), DNS management via Route 53.

---

## 🧭 Architecture

### Infrastructure Highlights

- **Amazon EKS**: Orchestrates containerized services.
- **Amazon EC2**: Hosts worker nodes in different Availability Zones.
- **Amazon ECR**: Stores Docker images for backend/frontend services.
- **Amazon CloudWatch**: Monitors application metrics and logs.
- **Amazon Route 53**: Handles DNS routing to the ALB.
- **AWS Certificate Manager**: Issues SSL/TLS certificates for HTTPS.

### Kubernetes Components

- **Frontend**: React app exposed via Ingress and ALB.
- **Backend**: Internal Node.js service connecting to MongoDB.
- **MongoDB**: StatefulSet with Persistent Volume Claims.
- **Ingress**: ALB controller for external HTTPS traffic.

---

## 🚀 Getting Started

### Prerequisites

Install the following tools:

- [Git](https://git-scm.com/downloads)
- [Docker](https://www.docker.com/products/docker-desktop)
- [Kubectl](https://kubernetes.io/docs/tasks/tools/)
- [Node.js](https://nodejs.org/)
- [AWS CLI](https://docs.aws.amazon.com/cli/)
- [eksctl](https://eksctl.io/)

### Clone Repository

```bash
git clone https://github.com/reubenthomas107/doctor-office-app.git
cd doctor-office-app
```

---

## 🐳 Local Testing

### Docker Compose

```bash
docker-compose up -d
```

### Kubernetes with Minikube

```bash
minikube start
kubectl apply -f k8s/
minikube tunnel
```

Access via `http://localhost/`

---

## ☁️ AWS Deployment

### Push to ECR

```bash
docker build -t doctor-office-frontend .
docker tag doctor-office-frontend:latest <account-id>.dkr.ecr.<region>.amazonaws.com/doctor-office-frontend:v1
docker push <ecr-url>
```

Repeat the same for the backend service.

### Create EKS Cluster

```bash
eksctl create cluster -f aws_infra/eks_cluster_setup.yaml
```

### Deploy App

```bash
kubectl apply -f k8s/
```

### Access the app

```bash
kubectl get ingress
```

Visit the Load Balancer DNS or the domain:  
🔗 [https://doctorapp-group3enpm818r.site](https://doctorapp-group3enpm818r.site)

---

## 📈 Monitoring & Autoscaling

- CloudWatch logs, metrics, and alerts configured
- Horizontal Pod Autoscaler (HPA) for backend service
- Alerts for:
  - CPU utilization
  - Memory usage
  - Container termination errors

---

## 🔐 Security & DNS

- SSL/TLS via **AWS Certificate Manager (ACM)**
- Domain routing via **Amazon Route 53**
- HTTPS termination configured in Ingress YAML
- DNS validation via CNAME for public certificate issuance

---

## ⚙️ CI/CD Pipeline

CI/CD automated using GitHub Actions.

### Workflow File: [.github/workflows/deploy.yaml](.github/workflows/deploy.yaml)

#### Pipeline Jobs:

- **`check-prerequisites`**: Validates setup.
- **`build`**: Builds and pushes Docker images to ECR.
- **`deploy-eks-cluster`**: Creates or configures EKS cluster.
- **`prod-k8s-deploy`**: Applies all Kubernetes manifests.

> Sensitive data like IAM roles, secrets, and tokens are securely stored using GitHub Secrets.

---

## 📂 Repository Structure

```
/frontend/             # React frontend code
/backend/              # Node.js backend code
/aws_infra/            # EKS cluster setup (eksctl)
/k8s/                  # Kubernetes manifests (Deployments, Services, Ingress)
/.github/workflows/    # CI/CD workflow for GitHub Actions
```

---

## 👥 Team Members

| Name                         | Email                    |
|------------------------------|--------------------------|
| Reuben Thomas                | reuben10@umd.edu         |
| Jongho Lee                   | jongho@umd.edu           |
| Praveen Kumar Masupatri      | pmasupat@umd.edu         |
| Ganesh P. More               | gpmore@umd.edu           |
| Rishabh Goel                 | rgoel22@umd.edu          |
| Bhanu Teja Panguluri         | bhanutp@umd.edu          |
| Dhanushree S. Onkaramurthy   | dhanuso7@umd.edu         |

---

## 📬 Feedback & Contributions

We welcome contributions! Please feel free to fork the repository and submit a pull request.  
If you encounter any bugs or have suggestions, open an [issue](https://github.com/reubenthomas107/doctor-office-app/issues).

---

## 📜 License

This project was developed as part of the **ENPM818R Midterm Project** at the University of Maryland.  
For educational purposes only.
