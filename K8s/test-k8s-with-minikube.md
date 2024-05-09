# Minikube Deployment and Nginx Configuration on Ubuntu

This document outlines the steps to deploy Minikube on Ubuntu and configure Nginx as a test application with a NodePort service. 
Minikube is a great platform for beginers looking to learn Kubernetes.

## Overview:

### 1. Installing Minikube and Starting the Cluster
   - Install Docker and Minikube.
   - Start the Minikube cluster using Docker as the driver.

### 2. Installing and Configuring `kubectl`
   - Download and configure `kubectl` from the Kubernetes official source.

### 3. Deploying Nginx Pod
   - Deploy an Nginx pod and verify its status.

### 4. Exposing Nginx Pod via a NodePort Service
   - Expose the Nginx pod through a NodePort service and retrieve the service URL.
   - Run some tests to ensure everything's working.

### 5. Cleaning Up
   - Delete the Nginx pod and service as needed.

## Detailed Steps:

### 1. Installing Minikube and Starting the Cluster
- **Ensure Docker installation**
  ```bash
  docker --version
  ```
- **If you need to install Docker, install Docker engine (No UI) using the easy [official guide](https://docs.docker.com/engine/install/)**
- **Give your user the required permissions**
  ```bash
  sudo usermod -aG docker $USER
  ```
- **Logout and login from your Linux OS (or reboot)**
  
- **Install Minikube**:
  ```bash
  curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && sudo install minikube /usr/local/bin/
  ```
- **Start Minikube**:
  ```bash
  minikube start
  ```

### 2. Installing and Configuring `kubectl`
- **Download `kubectl`**:
  ```bash
  curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
  ```
- **Move and set executable**:
  ```bash
  sudo mv kubectl /usr/local/bin/
  sudo chmod +x /usr/local/bin/kubectl
  ```

### 3. Deploying Nginx Pod
- **Run Nginx pod**:
  ```bash
  kubectl run nginx --image=nginx
  ```
- **Check pod status**:
  ```bash
  kubectl get pods
  ```

### 4. Exposing Nginx Pod via a NodePort Service

- **Expose Nginx**:
  ```bash
  kubectl expose pod nginx --type=NodePort --port=80 --name=nginx-service
  ```
- **Get service URL**:
  ```bash
  minikube service nginx-service --url
  ```
- **Save this. You will get the URL (Minikube IP) and port (NodePort) number that is needed to access the application.

#### Testing the Nginx Service

Once the service is exposed, you can test its accessibility using several methods:

- **Directly Access the Service URL**:
  Use the output URL from the `minikube service nginx-service --url` command to directly access the Nginx homepage. This URL includes the Minikube IP and the NodePort:
  ```bash
  curl $(minikube service nginx-service --url)
  ```

- **Access Through Minikube IP**:
  Manually construct the URL using the Minikube IP and the NodePort displayed after exposing the service:
  ```bash
  curl http://$(minikube ip):<NodePort>
  ```
  Replace `<NodePort>` with the actual port number provided by the `kubectl get svc` command.

- **Browser Access**:
  Simply paste the service URL into a web browser. This method confirms that the Nginx service is serving the default page over the web.

- **Using `minikube service` Command for Automatic Browser Opening**:
  Minikube can automatically open the service in your default web browser:
  ```bash
  minikube service nginx-service
  ```

These methods provide a straightforward way to confirm that the Nginx pod is correctly set up and responding to HTTP requests via the configured NodePort service.

### 5. Cleaning Up
- **Delete Nginx pod**:
  ```bash
  kubectl delete pod nginx
  ```
- **Delete Nginx service**:
  ```bash
  kubectl delete service nginx-service
  ```
