# Docker Networking with Multiple Containers

## Overview

This assignment demonstrates Docker bridge networking by connecting three containers: a Python Flask web application, a MySQL database, and a Redis cache. All three containers are connected to a custom bridge network, allowing them to communicate using their container names.

## Objectives

- Create and inspect a custom Docker bridge network.
- Run multiple containers on the same network.
- Build and run a Flask REST API using Docker.
- Verify container-to-container connectivity using ping.
- Understand Docker's internal DNS and network isolation.

## Technologies Used

- Docker Desktop
- Python
- Flask
- MySQL
- Redis
- Docker Bridge Networking
- Windows CMD

## Project Structure

```text
4-Docker-Networking/
├── app.py
├── requirements.txt
├── Dockerfile
├── README.md
└── Screenshots/
    ├── network-list.png
    ├── network-inspect.png
    ├── containers-running.png
    ├── flask-api.png
    └── container-connectivity.png
```

## Implementation

### 1. Create a Custom Bridge Network

Created a Docker bridge network named `my-bridge-net`.

```bash
docker network create --driver bridge my-bridge-net
```

Verified the network:

```bash
docker network ls
docker network inspect my-bridge-net
```

### 2. Develop the Flask REST API

Created a Flask application in `app.py` with an `/about` endpoint that returns the API name, version, and description in JSON format.

The application listens on port `5001`.

### 3. Build the Docker Image

Built the Flask application image using the Dockerfile.

```bash
docker build -t flask-api .
```

### 4. Launch the Containers

Started MySQL, Redis, and Flask containers on the custom bridge network.

**MySQL:**

```bash
docker run -d --name mysql --network my-bridge-net -e MYSQL_ROOT_PASSWORD=DevopsRoot123! -e MYSQL_DATABASE=appdb mysql:8.0
```

**Redis:**

```bash
docker run -d --name redis --network my-bridge-net redis:7
```

**Flask:**

```bash
docker run -d --name flask --network my-bridge-net -p 5001:5001 flask-api
```

Verified the running containers:

```bash
docker ps
```

### 5. Test the Flask API

Accessed the Flask API using:

```bash
curl http://localhost:5001/about
```

The endpoint returned a JSON response containing the API name, version, and description.

### 6. Test Container Connectivity

Entered the Flask container:

```bash
docker exec -it flask sh
```

Tested connectivity to MySQL:

```bash
ping -c 4 mysql
```

Tested connectivity to Redis:

```bash
ping -c 4 redis
```

Both containers responded successfully to all four ping requests, demonstrating that Docker's internal DNS resolved their container names and that they were reachable over the shared bridge network.

### 7. Clean Up

After completing the tests, the containers and network can be removed using:

```bash
docker stop flask redis mysql
docker rm flask redis mysql
docker network rm my-bridge-net
```

Run these commands only after saving the required screenshots.

## Screenshots

The `Screenshots` folder contains evidence of the network configuration, running containers, API response, and connectivity tests.

- [Network List](Screenshots/network-list.png)
- [Network Inspection](Screenshots/network-inspect.png)
- [Running Containers](Screenshots/containers-running.png)
- [Flask API Response](Screenshots/flask-api.png)
- [MySQL and Redis Connectivity](Screenshots/container-connectivity.png)

## Key Learnings

- Creating and inspecting custom Docker bridge networks.
- Running multiple containers on a shared network.
- Accessing a Flask application through port mapping.
- Using Docker's internal DNS to resolve container names.
- Testing connectivity between containers.
- Managing container and network cleanup.

## Conclusion

This assignment provided practical experience with Docker bridge networking and multi-container environments. The successful Flask API response and ping tests confirmed that the application, MySQL, and Redis containers were reachable within the custom network.
