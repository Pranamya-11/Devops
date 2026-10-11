# Deploying a Flask Application on Kubernetes using Minikube

## Overview

In this assignment, I deployed a simple Flask web application on a local Kubernetes cluster using Minikube. I used Docker to build the application image and Kubernetes to manage the deployment and expose the application through a NodePort Service.

The application displays a simple message in the browser, confirming that Flask is running successfully inside a Kubernetes Pod.

## Technologies Used

- Python and Flask
- Docker
- Kubernetes
- Minikube
- kubectl

## Implementation Steps

### 1. Start the Minikube Cluster

I started a local Kubernetes cluster using Minikube with the Docker driver.

```bash
minikube start --driver=docker
```

### 2. Create the Flask Application

I created an `app.py` file containing a basic Flask application that returns a message when the home route is accessed.

```python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def home():
    return "Hello from Flask on Kubernetes!"

if __name__ == '__main__':
    app.run(host='0.0.0.0', port=15000)
```

### 3. Create the Docker Image

I created a Dockerfile to package the Flask application and its dependencies into a Docker image.

```dockerfile
FROM python:3.8-slim
WORKDIR /app
COPY . /app
RUN pip install flask
CMD ["python", "app.py"]
```

I built the image and loaded it into Minikube so that Kubernetes could use it locally.

```bash
docker build -t flask-app:latest .
minikube image load flask-app:latest
```

### 4. Create the Kubernetes Deployment

I created `flask-deployment.yaml` to define the Deployment. It specifies the container image, the number of replicas, and the port on which the Flask application runs.

I used `imagePullPolicy: Never` because the image was built locally and loaded into Minikube instead of being pulled from a remote registry.

### 5. Deploy the Application

I applied the Kubernetes configuration using:

```bash
kubectl apply -f flask-deployment.yaml
```

### 6. Verify the Deployment

I checked the Deployment, Pods, and Services to make sure the application was created correctly.

```bash
kubectl get deployments
kubectl get pods
kubectl get services
```

I also used the following commands to inspect the Deployment and check the Flask application logs.

```bash
kubectl describe deployment flask-app
kubectl logs <pod-name>
```

The logs confirmed that Flask was running and listening on port `15000`.

### 7. Expose the Application

I created a NodePort Service named `flask-app-service` to make the application accessible outside the Pod.

The Service forwards traffic from port `15000` to the container's target port `15000`.

### 8. Test the Application

Initially, accessing `127.0.0.1:15000` directly did not work because the application was running inside the Kubernetes cluster.

I used port forwarding to access it locally:

```bash
kubectl port-forward service/flask-app-service 15000:15000
```

In another terminal, I tested the application using:

```bash
curl http://127.0.0.1:15000
```

The application returned:

```text
Hello from Flask on Kubernetes!
```

## Screenshots

The `Screenshots` folder contains the terminal output showing the Deployment, Pod status, application logs, Service details, and Flask response.

## Outcome

Through this assignment, I learned how to containerize a Python application using Docker, deploy it on Kubernetes with Minikube, manage application resources using `kubectl`, and expose a running application through a Kubernetes Service. I also learned how port forwarding can be used to test an application running inside a local Kubernetes cluster.