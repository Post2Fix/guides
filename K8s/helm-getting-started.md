### Deploying Nginx using Helm on Minikube

---

# Deploying Nginx on Minikube using Helm

This guide details the steps to deploy Nginx using Helm on Minikube. 
The purpose is to transition from a manual Kubernetes setup to a Helm-based deployment, providing a scalable and manageable approach to deploying applications like Nginx on Kubernetes.

## Overview

1. **Helm Installation**
   - Clean up resources from previous deployment methods.
   - Download and install Helm.
   - Verify the installation.

2. **Creating the Helm Chart**
   - Create a new Helm chart for Nginx.
   - Examine and modify the chart files.

3. **Deploying Nginx Using Helm**
   - Deploy the Helm chart.
   - Access Nginx using the provided service.

## Detailed Steps

### 1. Helm Installation
- **Clean up resources**:
  ```bash
  kubectl delete pod nginx
  kubectl delete service nginx-service
  ```
- **Download Helm**:
  ```bash
  wget https://get.helm.sh/helm-v3.15.0-rc.1-linux-amd64.tar.gz
  tar -xvf helm-v3.15.0-rc.1-linux-amd64.tar.gz
  sudo mv linux-amd64/helm /usr/local/bin/
  ```
- **Verify Helm installation**:
  ```bash
  helm version
  ```

### 2. Creating the Helm Chart
- **Generate the Helm chart for Nginx**:
  ```bash
  helm create nginx
  ```
- **Navigate to the chart directory**:
  ```bash
  cd nginx
  ```
- **Modify `values.yaml`** (showing only the section that needs to be updated):
  ```yaml
  service:
    type: NodePort
    port: 80
  ```

### 3. Deploying Nginx Using Helm
- **Deploy the chart**:
  ```bash
  helm install nginx .
  ```
- **Run the commands from the NOTES.txt instructions to view the full URL**:
  ```bash
  export NODE_PORT=$(kubectl get --namespace default -o jsonpath="{.spec.ports[0].nodePort}" services nginx)
  export NODE_IP=$(kubectl get nodes --namespace default -o jsonpath="{.items[0].status.addresses[0].address}")
  echo http://$NODE_IP:$NODE_PORT
  ```
- **Access Nginx using the full URL**:
  ```bash
  curl http://$NODE_IP:$NODE_PORT
  ```
