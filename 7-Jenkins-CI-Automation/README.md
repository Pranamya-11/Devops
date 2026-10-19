# Assignment 7: Jenkins CI Automation

## Overview

This assignment demonstrates the installation and configuration of Jenkins using Docker. Jenkins is an open-source automation server used to automate software development tasks, including building, testing, and deploying applications.

## Objectives

- Install and run Jenkins using Docker.
- Access the Jenkins web interface.
- Configure Jenkins and install suggested plugins.
- Create an administrator account.
- Create and execute a basic Jenkins pipeline.

## Technologies Used

- Jenkins
- Docker
- Git and GitHub
- Pipeline (Groovy)

## Jenkins Installation

Jenkins was installed using the official Jenkins Docker image.

```bash
docker run -d --name jenkins-assignment7 \
  -p 8081:8080 \
  -p 50001:50000 \
  -v jenkins7_home:/var/jenkins_home \
  jenkins/jenkins:lts
```

### Port Configuration

- **8081:** Host port used to access the Jenkins web interface.
- **50001:** Host port mapped to the Jenkins agent communication port.
- **jenkins7_home:** Persistent Docker volume used to store Jenkins configuration, plugins, and jobs.

## Accessing Jenkins

Open the following URL in a browser:

http://localhost:8081

During the initial setup, the suggested plugins were installed and an administrator account was configured.

## Jenkins Pipeline

A basic Jenkins pipeline was created and executed successfully to demonstrate pipeline stages and job execution.

The pipeline included stages to display startup messages, describe the monitoring project, and report completion status.

The pipeline execution was verified through the Jenkins console output.

**Note:** Automated Docker image building and deployment directly through Jenkins remain incomplete because Docker daemon access from the Jenkins container has not yet been configured.

## Result

Successfully installed and configured a separate Jenkins instance using Docker and executed a basic Jenkins pipeline.

## Conclusion

This assignment provided practical experience with Jenkins installation, initial configuration, plugin setup, and pipeline execution. It also introduced the role of Jenkins in automating software development workflows.
