# Assignment 01: Deploy Nginx on Kubernetes using Minikube

## Objective
Deploy an Nginx Pod on a local Kubernetes cluster using Minikube and expose it through a NodePort Service.

## Tools Used
- Minikube
- Kubernetes
- kubectl
- Docker Desktop

## Steps Performed

### 1. Start Minikube
```bash
minikube start --driver=docker
```

### 2. Create the Nginx Pod
```bash
kubectl run hello-k8s --image=nginx --port=80
```

### 3. Verify the Pod
```bash
kubectl get pods
```

### 4. Expose the Pod
```bash
kubectl expose pod hello-k8s --type=NodePort --port=80
```

### 5. Access the Application
```bash
minikube service hello-k8s
```

## Expected Result
The Nginx welcome page should open in the browser, and the Pod should reach the Running state.

## Screenshots
See the `screenshots/` folder for execution evidence.