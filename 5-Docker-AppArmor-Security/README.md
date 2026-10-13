# Docker Container Security Using AppArmor

## Overview

This project demonstrates containerizing a Python Flask application using Docker and explores how AppArmor can improve container security by restricting access to sensitive files and limiting potentially dangerous operations.

The Flask application is packaged as a Docker image and run inside a container. The assignment also explores loading an AppArmor profile, applying it to a container, and testing restricted actions.

## Objectives

- Build and run a Flask application inside a Docker container.
- Understand AppArmor profiles and their role in Linux security.
- Explore restricting access to sensitive files and system resources.
- Use the Docker SDK for Python to manage containers and inspect security options.
- Test whether restricted operations are blocked by an enforced security profile.

## Technologies Used

- Python
- Flask
- Docker Desktop
- Docker SDK for Python
- Ubuntu on WSL2
- AppArmor utilities

## Project Structure

```text
5-Docker-AppArmor-Security/
├── app.py
├── Dockerfile
├── requirements.txt
├── apply_apparmor.py
├── test_restricted_actions.py
├── README.md
└── Screenshots/
    ├── docker-build.png
    ├── flask-app-test.png
    ├── container-running.png
    ├── apparmor-status.png
    ├── profile-loaded.png
    ├── docker-sdk-verification.png
    └── restricted-actions.png
```

## Implementation

### 1. Create the Flask Application

The Flask application returns a message confirming that it is running inside a Docker container.

The application listens on port `5000` and binds to `0.0.0.0` so that it can be accessed through Docker port mapping.

### 2. Create the Docker Image

The Dockerfile uses a Python base image, installs Flask, copies the application into the image, and starts the application when the container launches.

Build the image using:

```bash
docker build -t flask-apparmor .
```

### 3. Run the Container

Start the container and map port `5000`:

```bash
docker run -d --name flask-secure -p 5000:5000 flask-apparmor
```

Verify the running container:

```bash
docker ps
```

### 4. Test the Flask Application

Test the application from Windows PowerShell:

```powershell
curl.exe http://localhost:5000
```

The application returned the following response:

```text
Hello, this is a secure Flask application running inside a Docker container!
```

The successful response confirms that the container is running and that the port mapping works.

### 5. Install AppArmor Utilities

Installed the AppArmor utilities in Ubuntu WSL2:

```bash
sudo apt-get update
sudo apt-get install -y apparmor-utils
```

Checked the AppArmor status:

```bash
sudo aa-status
```

The environment reported that the AppArmor module was loaded, but the AppArmor filesystem was not mounted. The AppArmor service also reported that its startup condition was not met.

### 6. AppArmor Profile and Enforcement

The intended next step is to create a custom AppArmor profile that restricts selected file accesses and system capabilities, load the profile, and run the Flask container with the profile applied.

The current Docker Desktop engine did not list AppArmor among its reported security options. Therefore, custom AppArmor enforcement has not yet been verified in this environment.

Actual profile loading, Docker SDK verification, and restricted-action testing must be completed in a Linux environment where AppArmor is enabled and supported by the container runtime.

### 7. Docker SDK for Python

The assignment includes a Python script named `apply_apparmor.py` to build the image, launch a container with a specified AppArmor profile, and inspect the container's security configuration.

The `test_restricted_actions.py` script is intended to test selected operations, such as reading `/etc/passwd` and executing a shell, under the enforced profile.

These tests should only be reported as successful after confirming that the custom profile is active and that the denials are caused by the profile rather than unrelated errors.

## Screenshots

The following screenshots document the Docker build, Flask application, running container, and AppArmor status.

1. **Docker Image Build** — [View Screenshot](Screenshots/docker-build-output.png)
2. **Flask Application Test** — [View Screenshot](Screenshots/flask-app-test-output.png)
3. **Flask Output** — [View Screenshot](Screenshots/flask-output.png)
4. **Running Container** — [View Screenshot](Screenshots/container-running-output.png)
5. **AppArmor Status** — [View Screenshot](Screenshots/apparmor-status.png)



Only add screenshots for steps that have actually been performed. Update filenames if your saved screenshots use different names.

## Key Learnings

- Building and running containerized Flask applications.
- Exposing container ports using Docker port mapping.
- Understanding the purpose of Linux AppArmor profiles.
- Exploring how mandatory access control can restrict container operations.
- Using the Docker SDK to manage containers and inspect configuration.
- Distinguishing between installing security tools and successfully enforcing a security profile.

## Conclusion

The Flask application was successfully containerized and tested using Docker Desktop. The project also explored AppArmor installation and status checks in Ubuntu WSL2, revealing that the current environment does not expose the AppArmor filesystem interface and that the Docker Desktop engine does not report AppArmor support.

The remaining enforcement and restricted-action tests require an environment with AppArmor enabled. This distinction is important for accurately evaluating container security.
