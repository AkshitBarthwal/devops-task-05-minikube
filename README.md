# DevOps Task 05 --- Kubernetes Deployment with Minikube

A hands-on Kubernetes project demonstrating how to deploy, expose,
scale, inspect, and verify a containerized NGINX application using a
local Minikube cluster.

## 📌 Project Overview

This project was developed as part of a DevOps practical task focused on
understanding Kubernetes fundamentals.

The implementation uses Minikube to create a local Kubernetes cluster
and deploys an NGINX application using Kubernetes Deployment and Service
resources.

The project demonstrates:

-   Local Kubernetes cluster creation
-   Kubernetes Deployment configuration
-   Pod management
-   Kubernetes Service configuration
-   NodePort exposure
-   Deployment scaling
-   Pod inspection with `kubectl describe`
-   Container log inspection with `kubectl logs`
-   Application connectivity verification
-   Git-based version control

## 🎯 Objective

Deploy and manage an application in a local Kubernetes environment using
Minikube and kubectl.

The project focuses on understanding the basic Kubernetes workflow:

``` text
Kubernetes Manifest
        ↓
Deployment
        ↓
ReplicaSet
        ↓
Pods
        ↓
Service
        ↓
Application Access
```

## 🛠️ Technologies Used

  Technology     Purpose
  -------------- --------------------------
  Kubernetes     Container orchestration
  Minikube       Local Kubernetes cluster
  kubectl        Kubernetes CLI
  Docker         Container runtime
  NGINX          Sample application
  Git            Version control
  GitHub         Source code hosting
  Ubuntu Linux   Development environment

## 🏗️ Architecture

``` text
                    Minikube Cluster
                           |
                    +------v------+
                    | Deployment  |
                    | devops-nginx|
                    | Replicas: 4 |
                    +------+------+
                           |
              +------------+------------+
              |            |            |
           +--v--+       +--v--+      +--v--+
           | Pod |       | Pod |      | Pod | ...
           |NGINX|       |NGINX|      |NGINX|
           +-----+       +-----+      +-----+
              \             |             /
               \            |            /
                +-----------v-----------+
                | Kubernetes Service    |
                | devops-nginx-service  |
                | Type: NodePort        |
                | Port: 80              |
                | NodePort: 30080       |
                +-----------------------+
```

## 📁 Project Structure

``` text
devops-task-05-minikube/
│
├── deployment.yaml
├── service.yaml
├── README.md
├── .gitignore
│
└── screenshots/
    ├── 01-minikube-cluster-running.png
    ├── 02-deployment-yaml.png
    ├── 03-deployment-created.png
    ├── 04-service-yaml.png
    ├── 05-service-created.png
    ├── 06-scaled-deployment.png
    ├── 07-kubectl-describe.png
    └── 08-final-kubernetes-status.png
```

## ⚙️ Prerequisites

The following tools are required:

-   Docker
-   Minikube
-   kubectl
-   Git

Verify the installations:

``` bash
docker --version
minikube version
kubectl version --client
git --version
```

# 🚀 Implementation

## 1. Start Minikube

Start the local Kubernetes cluster using Docker as the driver:

``` bash
minikube start --driver=docker
```

Verify the cluster:

``` bash
minikube status
kubectl get nodes
kubectl get pods -A
```

Expected node status:

``` text
minikube   Ready   control-plane
```

## 2. Create the Deployment

The `deployment.yaml` file defines an NGINX Deployment with two initial
replicas.

``` yaml
replicas: 2
```

Apply the Deployment:

``` bash
kubectl apply -f deployment.yaml
```

Verify:

``` bash
kubectl get deployment devops-nginx
kubectl get pods -l app=devops-nginx
```

## 3. Create the Service

The `service.yaml` exposes the NGINX application through a NodePort
Service.

Configuration:

``` text
Service Type: NodePort
Port: 80
Target Port: 80
Node Port: 30080
```

Apply the Service:

``` bash
kubectl apply -f service.yaml
```

Verify:

``` bash
kubectl get service devops-nginx-service
```

Check the endpoints:

``` bash
kubectl get endpoints devops-nginx-service
```

## 4. Scale the Deployment

The Deployment was initially configured with two replicas.

Kubernetes scaling was demonstrated by increasing the replicas from 2 to
4:

``` bash
kubectl scale deployment devops-nginx --replicas=4
```

Verify:

``` bash
kubectl get deployment devops-nginx
kubectl get pods -l app=devops-nginx
```

Final state:

``` text
Desired:   4
Current:   4
Available: 4
```

## 5. Inspect the Pod

A running NGINX Pod was inspected using:

``` bash
kubectl describe pod <pod-name>
```

This provides information about:

-   Pod state
-   Container configuration
-   Image
-   Conditions
-   Node assignment
-   Events
-   Restart information

## 6. View Container Logs

Container logs were checked using:

``` bash
kubectl logs <pod-name>
```

This verifies that the NGINX container started successfully.

## 7. Verify the Complete Deployment

The final Kubernetes resources were verified using:

``` bash
kubectl get deployment
kubectl get pods -o wide
kubectl get service
kubectl get endpoints devops-nginx-service
kubectl get all
```

The final state showed:

-   1 Deployment
-   1 ReplicaSet
-   4 running Pods
-   1 NodePort Service
-   4 available replicas

## 🔍 Useful Kubernetes Commands

### Cluster

``` bash
minikube status
kubectl get nodes
kubectl get pods -A
```

### Deployments

``` bash
kubectl get deployments
kubectl describe deployment devops-nginx
```

### Pods

``` bash
kubectl get pods
kubectl get pods -o wide
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

### Services

``` bash
kubectl get services
kubectl get endpoints devops-nginx-service
```

### Scaling

``` bash
kubectl scale deployment devops-nginx --replicas=4
```

### Complete status

``` bash
kubectl get all
```

# 📸 Evidence

The `screenshots/` directory contains evidence of the complete
implementation.

  Evidence   Description
  ---------- ---------------------------------------
  01         Minikube cluster running
  02         Kubernetes Deployment manifest
  03         Deployment and Pods created
  04         Kubernetes Service manifest
  05         Service created and connected to Pods
  06         Deployment scaled to four replicas
  07         Pod inspection and container logs
  08         Final Kubernetes resource status

# 📚 Key Learnings

Through this project, I learned:

-   How Minikube provides a local Kubernetes environment
-   How Kubernetes Deployments manage Pods
-   How labels and selectors connect Kubernetes resources
-   How Services provide stable access to Pods
-   How NodePort exposes a Service
-   How to scale a Deployment using kubectl
-   How to inspect Pods using `kubectl describe`
-   How to troubleshoot applications using container logs
-   How to verify Kubernetes resources using `kubectl`
-   How to manage DevOps projects using Git and GitHub

# 🔐 Cleanup

When the project is no longer required, Kubernetes resources can be
removed using:

``` bash
kubectl delete -f service.yaml
kubectl delete -f deployment.yaml
```

The entire Minikube cluster can be removed using:

``` bash
minikube delete
```

## 👨‍💻 Project Information

**Project:** DevOps Task 05 --- Kubernetes with Minikube

**Focus:** Kubernetes Fundamentals

**Environment:** Ubuntu Linux

**Container Runtime:** Docker

**Orchestration:** Kubernetes / Minikube

**Application:** NGINX

**Version Control:** Git / GitHub


## Author

**Akshit Barthwal**

BCA Student | Aspiring DevOps Engineer
