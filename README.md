 Microservice E-Commerce Project --- CI/CD with Jenkins on Kubernetes (Amazon EKS)

 [![Microservice E-Commerce Architecture](https://github.com/thisismuhammadessa/Microservice-E-Commerce-project-CI-CD-with-Jenkins-on-Kubernetes-EKS/blob/main/architecture-di.png?raw=true)](https://github.com/thisismuhammadessa/Microservice-E-Commerce-project-CI-CD-with-Jenkins-on-Kubernetes-EKS/blob/main/architecture-di.png)

A production-style microservices e-commerce application deployed on
Amazon EKS (Elastic Kubernetes Service) using Kubernetes, with
Jenkins providing automated CI/CD.

This project demonstrates an end-to-end DevOps workflow covering source
control, automated pipeline execution, containerization, Kubernetes
deployment, service discovery, external load balancing, and AWS
infrastructure integration.

📌 Project Overview

The application is built as a collection of independent microservices.
Each service runs as a containerized workload inside an Amazon EKS
cluster and communicates with other services through Kubernetes
Services.

The CI/CD workflow is designed around GitHub and Jenkins:

Developer → GitHub → Jenkins → Docker Build → Kubernetes Deployment →
Amazon EKS → AWS Load Balancer → End Users

The application runs in the Kubernetes namespace:

webapps

🏗️ Architecture

The architecture contains four main layers:

1. Source Control

GitHub is used to store the application source code, Kubernetes
manifests, Jenkinsfile, and multiple development/service branches.

Developers push code changes to GitHub, which are detected by the
Jenkins Multibranch Pipeline.

2. CI/CD Pipeline

Jenkins automates the deployment workflow.

The pipeline performs the following activities:

Checkout code from GitHub

Install application dependencies

Build and test the application

Build Docker images for the required microservices

Deploy Kubernetes manifests using kubectl

Verify the deployed Kubernetes resources

This provides a repeatable and automated deployment process.

3. Container Orchestration

Kubernetes on Amazon EKS manages the microservices.

Kubernetes provides:

Container orchestration

Pod scheduling

Service discovery

Application self-healing

Deployment management

Scaling support

Internal service communication

4. AWS Application Access

The frontend is exposed through an AWS Load Balancer.

Users access the application through the load balancer, which forwards
traffic to the frontend service running inside the EKS cluster.

🔄 CI/CD Workflow

                    Developer
                        │
                        ▼
                     GitHub
                        │
                        ▼
              Jenkins Multibranch
                   Pipeline
                        │
                        ▼
               Checkout Source
                        │
                        ▼
              Install Dependencies
                        │
                        ▼
                 Build & Test
                        │
                        ▼
                Docker Build
                        │
                        ▼
             Kubernetes Deployment
                        │
                        ▼
                Amazon EKS
                        │
                        ▼
              Frontend Service
                        │
                        ▼
              AWS Load Balancer
                        │
                        ▼
                     Users

🧩 Microservices

The application consists of the following components:

Service                   Purpose

Frontend                  User interface for the e-commerce application
Product Catalog Service   Manages product information
Cart Service              Handles shopping cart operations
Checkout Service          Coordinates the checkout process
Payment Service           Handles payment-related operations
Currency Service          Provides currency conversion
Recommendation Service    Provides product recommendations
Email Service             Handles email-related functionality
Shipping Service          Handles shipping operations
Ad Service                Provides advertisement functionality
Redis Cart                Provides Redis-based cart caching
Load Generator            Generates application traffic for testing

☸️ Kubernetes

The microservices are deployed inside the webapps namespace on
Amazon EKS.

Kubernetes Deployments manage the application Pods, while Kubernetes
Services provide networking and service discovery between microservices.

The frontend is exposed externally through a LoadBalancer service.

Example:

Internet
   │
   ▼
AWS Load Balancer
   │
   ▼
Frontend Service
   │
   ▼
Frontend Pod
   │
   ├── Product Catalog
   ├── Cart
   ├── Checkout
   ├── Payment
   ├── Shipping
   ├── Currency
   ├── Recommendation
   ├── Email
   └── Ad Service

🔐 Jenkins → Kubernetes Deployment

Jenkins authenticates to the Kubernetes cluster using Kubernetes
credentials and executes deployment commands such as:

kubectl apply -f deployment-service.yml

After deployment, the pipeline verifies the Kubernetes resources:

kubectl get all -n webapps

This ensures that the application resources have been successfully
deployed and are available in the cluster.

🛠️ Technology Stack

Technology          Role

GitHub              Source Code Management
Jenkins             CI/CD Automation
Docker              Containerization
Kubernetes          Container Orchestration
Amazon EKS          Managed Kubernetes Cluster
AWS Load Balancer   External Application Access
Redis               Cart Cache
Node.js / npm       Frontend dependency management
kubectl             Kubernetes CLI

📂 Repository Structure

.
├── Jenkinsfile
├── deployment-service.yml
├── README.md
├── architecture-di.png
└── microservices/
    ├── frontend/
    ├── adservice/
    ├── cartservice/
    ├── checkoutservice/
    ├── currencyservice/
    ├── emailservice/
    ├── loadgenerator/
    ├── paymentservice/
    ├── productcatalogservice/
    ├── recommendationservice/
    └── shippingservice/

The exact directory structure can vary depending on the branch and
source layout.

🚀 Deployment

Prerequisites

Before deploying the project, make sure the following are available:

AWS account

Amazon EKS cluster

Docker

kubectl

Jenkins

Git

Kubernetes credentials configured in Jenkins

Deploy manually with kubectl

Configure access to the EKS cluster and select the correct Kubernetes
context.

Then:

kubectl create namespace webapps

Deploy the application:

kubectl apply -f deployment-service.yml -n webapps

Check the Pods:

kubectl get pods -n webapps

Check Services:

kubectl get svc -n webapps

Check all resources:

kubectl get all -n webapps

🔁 Jenkins Pipeline

The Jenkins pipeline automates the Kubernetes deployment.

A simplified pipeline flow is:

GitHub Branch
     │
     ▼
Jenkins
     │
     ├── Checkout
     ├── Install Dependencies
     ├── Build & Test
     ├── Docker Build
     ├── Deploy to EKS
     └── Verify Deployment

The use of a Multibranch Pipeline allows Jenkins to discover and
build multiple GitHub branches independently.

🌐 Application Access

After deployment, retrieve the external LoadBalancer address:

kubectl get svc frontend-external -n webapps

Example:

NAME                TYPE           EXTERNAL-IP
frontend-external   LoadBalancer   <AWS-LOAD-BALANCER-DNS>

Open the LoadBalancer DNS name in a browser to access the application.

📊 Monitoring and Verification

Useful Kubernetes commands:

kubectl get pods -n webapps
kubectl get deployments -n webapps
kubectl get services -n webapps
kubectl get all -n webapps

To troubleshoot a Pod:

kubectl describe pod <pod-name> -n webapps

To view application logs:

kubectl logs <pod-name> -n webapps

🎯 Project Objectives

This project was built to demonstrate practical experience with:

Microservices architecture

Docker containerization

Kubernetes deployment

Amazon EKS

Jenkins CI/CD

GitHub branch-based development

Kubernetes Services

AWS Load Balancer integration

Redis caching

Automated deployment and verification

💡 Key DevOps Concepts Demonstrated

CI/CD: Automated application deployment through Jenkins

Infrastructure Platform: Amazon EKS

Containerization: Docker

Orchestration: Kubernetes

Source Control: GitHub

Service Discovery: Kubernetes Services

External Access: AWS Load Balancer

Caching: Redis

Deployment Verification: kubectl

👨‍💻 Author

Muhammad Essa

DevOps / Cloud & Kubernetes Project

Connect with me



⭐ Support

If you find this project useful, consider giving the repository a ⭐ on
GitHub.
