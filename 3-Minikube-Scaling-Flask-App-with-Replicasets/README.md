# Scaling Flask App Using Kubernetes ReplicaSets

## Overview

This project demonstrates how to deploy and scale a Flask web application on a single-node Kubernetes cluster using Minikube and ReplicaSets. The application simulates a flash sale in an e-commerce store, where users can view a welcome message and make sample purchases.

The main objective is to understand horizontal scaling, Pod management, self-healing, and exposing an application through a Kubernetes Service.

## Technologies Used

- Python and Flask
- Docker
- Kubernetes
- Minikube
- kubectl
- Windows CMD

## Application Features

- **Home endpoint (`/`)** – Displays a welcome message, the serving Pod's hostname, and a timestamp.
- **Purchase endpoint (`/buy`)** – Simulates a purchase by returning a randomly selected product and user information.
- **Health endpoint (`/health`)** – Checks the application's health and returns the serving Pod's hostname.

## Project Structure

```text
3-Minikube-Scaling-Flask-App-with-Replicasets/
├── app.py
├── Dockerfile
├── flashsale-replicaset.yaml
├── README.md
└── Screenshots/
```

## Implementation Steps

### 1. Build the Docker Image

Built the Flask application image using Docker:

```bash
docker build -t flashsale:1.0 .
```

### 2. Load the Image into Minikube

Loaded the locally built image into the Minikube cluster:

```bash
minikube image load flashsale:1.0
```

### 3. Deploy the Application

Applied the Kubernetes configuration containing the ReplicaSet and Service:

```bash
kubectl apply -f flashsale-replicaset.yaml
```

### 4. Verify the Deployment

Checked the ReplicaSet, Pods, and Service:

```bash
kubectl get rs
kubectl get pods
kubectl get services
```

The ReplicaSet initially maintains three application replicas.

### 5. Test the Application

Forwarded the Service port to access the Flask application locally:

```bash
kubectl port-forward service/flashsale-svc 8080:80
```

In another terminal, tested the endpoints:

```bash
curl http://127.0.0.1:8080/
curl "http://127.0.0.1:8080/buy?user=123"
curl http://127.0.0.1:8080/health
```

### 6. Scale the Application

Increased the number of replicas from three to five:

```bash
kubectl scale rs flashsale-rs --replicas=5
kubectl get rs
kubectl get pods
```

Kubernetes creates additional Pods to reach the requested replica count.

### 7. Test Self-Healing

Deleted one of the running Pods:

```bash
kubectl delete pod <pod-name>
```

The ReplicaSet automatically creates a replacement Pod to maintain the desired number of replicas.

Verify the result using:

```bash
kubectl get pods
kubectl get rs
```

## Screenshots

Add your screenshots to the `Screenshots` folder and use the links below. Update the filenames if yours are different.

- [Docker Image Build](Screenshots/docker-build.png)
- [Initial ReplicaSet and Pods](Screenshots/initial-pods.png)
- [Application Endpoint Testing](Screenshots/flask-test.png)
- [Scaling to Five Replicas](Screenshots/replicaset-scaled.png)
- [Self-Healing Demonstration](Screenshots/self-healing.png)

## Key Learnings

- Building container images using Docker.
- Deploying containerized applications on Kubernetes.
- Using ReplicaSets to maintain a desired number of Pods.
- Scaling applications by increasing the replica count.
- Understanding Kubernetes self-healing behavior.
- Exposing an application using a Kubernetes Service and port forwarding.

## Conclusion

This assignment demonstrates how Kubernetes ReplicaSets help maintain application availability by managing Pod replicas. Scaling the Flask application from three to five replicas and observing automatic Pod replacement provided practical experience with horizontal scaling and self-healing in a single-node Minikube environment.
