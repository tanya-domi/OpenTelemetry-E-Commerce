Note: This project is a fork of opentelemetry-demo. Thanks to the team and contributors for opensourcing this wonderful demo project. 

![Image](https://github.com/user-attachments/assets/bab2562d-d95c-4962-8e4b-bb0041e73639)

![Image](https://github.com/user-attachments/assets/5ac09287-d579-4382-8898-2ab7db9a3bb8)

# Introduction
In this project, we aim to containerize the Product Catalog microservice and deploy it to a Kubernetes cluster on AWS EKS. 
To ensure a modern and efficient software delivery pipeline, we will implement Continuous Integration (CI) using GitHub Actions, 
and Continuous Delivery (CD) using Argo CD, following a GitOps approach. This setup will enable automated, reliable, and scalable deployment of the microservice, 
aligned with industry best practices for cloud-native applications.

# Prerequisites
Before proceeding with this project, ensure the following tools and infrastructure are in place:

 - Helm: Installed and configured locally for managing Kubernetes applications via Helm charts.

 - kubectl: Installed locally and configured to interact with your Kubernetes cluster.

 - Kubernetes Cluster: A running Amazon EKS (Elastic Kubernetes Service) cluster with appropriate access and permissions.

# 1. Set up Kubernetes cluster.

We will provision the Elastic Kubernetes Service (EKS) using Terraform, enabling us to define and manage our infrastructure as code for consistency, scalability, and repeatability. Once the EKS cluster is successfully provisioned, we will install the Ingress Controller (e.g., AWS Load Balancer Controller) to manage external access to the services within the cluster.
This setup will facilitate routing, load balancing, and secure ingress traffic into the Kubernetes environment.

![Image](https://github.com/user-attachments/assets/840fa37a-39a7-4df1-9768-ad4a299a9173)

![Image](https://github.com/user-attachments/assets/29ceb29c-bb3a-4106-9238-eaf4e855ba77)

# 2. Set up ArgoCD
Install Argocd and connect argocd with github repo to watch and pull changes then deploy the application to EKS cluster
We will install Argo CD into the EKS cluster to enable declarative, GitOps-style continuous delivery. Argo CD will be configured to connect with a designated GitHub repository,allowing it to continuously monitor for changes in application manifests.Upon detecting changes, Argo CD will automatically synchronize and deploy the updated application to the EKS cluster,ensuring a streamlined and automated deployment process.

 ![Image](https://github.com/user-attachments/assets/89483733-611c-4dc7-baff-30b2f557a476)

 # Check to confirm ArgoCD is installed
 
 ![Image](https://github.com/user-attachments/assets/555a944c-b541-4e98-b83b-3bd7210a0068)

 # We exposed ArgoCD as Loadbalancer
We will modify the Argo CD service configuration to expose it externally using a LoadBalancer service type.  This will allow us to access the Argo CD web UI securely from outside the cluster. Through the UI, we will be able to configure, manage, and deploy our application to the EKS cluster seamlessly.

 ![Image](https://github.com/user-attachments/assets/612afe1f-bc67-4726-857b-03d6858c7b8d)

 
# 3. Set up Github Action pipeline  [![product-catalog-ci](https://github.com/tanya-domi/OpenTelemetry-E-Commerce/actions/workflows/ci.yaml/badge.svg)](https://github.com/tanya-domi/OpenTelemetry-E-Commerce/actions/workflows/ci.yaml)

We will configure GitHub Actions to automate the deployment of the Product Catalog microservice.
This CI pipeline will handle tasks such as building the Docker image, pushing it to a container registry, and updating the deployment manifests in the Git repository.Once changes are committed, GitHub Actions will trigger the workflow,enabling a seamless and automated deployment process via Argo CD to the EKS cluster.

# 4. GitHub–Slack API integration
We will configure GitHub–Slack API integration to enable real-time notifications in Slack.This integration will automatically notify team members whenever a CI build succeeds or fails, providing immediate feedback on the deployment pipeline.This ensures enhanced visibility, faster response times, and improved collaboration across the development team.

![Image](https://github.com/user-attachments/assets/763da148-4c42-4551-949f-3b1b9b3c3647)

We will deploy our application using a combination of GitHub Actions for Continuous Integration and Argo CD for Continuous Delivery. 
Once the deployment is triggered and synchronized, we will monitor the Kubernetes cluster to ensure that all pods are running with a 1/1 status 
and that all application deployments are successfully up and running. This verification step ensures the health and stability of the deployed microservices within the EKS environment.

# Verify application pods 
![Image](https://github.com/user-attachments/assets/296eff04-35d8-4294-8bb7-7a83ee2c6195)

# Verify deployments
![Image](https://github.com/user-attachments/assets/90e75346-10ba-422e-b38c-263626a6f796)

# Verify ArgoCD deployment 
![Image](https://github.com/user-attachments/assets/36b1dfa2-e5ac-4f54-a40b-bc25c717e7e9)

# Amazon Route 53
We will set up a Hosted Zone in Amazon Route 53 and provision a TLS certificate using AWS Certificate Manager (ACM). 
This will allow us to configure a custom domain and associate it with the Application Load Balancer (ALB) endpoint of our application. 
By enabling HTTPS through TLS encryption, we ensure that all external traffic to the application is securely transmitted, protecting it from common threats and enhancing overall security.

![Image](https://github.com/user-attachments/assets/90184bae-ab46-44d2-a57b-7345b3b367d8)

# Conclusion
In this comprehensive microservices Kubernetes project, we successfully:

Provisioned IAM users and the required AWS infrastructure using Terraform, following infrastructure-as-code best practices.

Automated the deployment of infrastructure on AWS via GitHub Actions, integrating essential tools and configurations.

Set up and configured an Amazon EKS cluster, along with the AWS Load Balancer Controller to manage ingress traffic.

Installed and configured Argo CD, enabling a robust GitOps workflow for continuous delivery and environment synchronization.

Designed and implemented GitHub Actions pipelines for Continuous Integration and Continuous Deployment (CI/CD) of a microservices-based application.

Achieved automated and reliable application delivery through Argo CD, ensuring seamless synchronization and real-time deployment of updates to the EKS cluster.
