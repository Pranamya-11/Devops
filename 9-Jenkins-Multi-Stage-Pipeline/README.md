# Assignment 9: Jenkins Multi-Stage Pipeline

## Objective
To create and execute a multi-stage Jenkins pipeline for a Python Flask application, demonstrating source code checkout, build verification, test-file verification, and deployment preparation.

## Technologies Used
- **Jenkins** – CI/CD pipeline automation
- **Git & GitHub** – Source code management
- **Python** – Application language
- **Flask** – Web framework
- **Groovy** – Jenkins Pipeline syntax

## Project Structure

```text
9-Jenkins-Multi-Stage-Pipeline/
├── app.py
├── requirements.txt
├── test_app.py
├── Jenkinsfile
├── Dockerfile
├── Screenshots/
└── README.md
```

## Pipeline Stages

### 1. Checkout
Checks out the source code from the GitHub repository's `main` branch.

### 2. Build
Verifies that the Python application file (`app.py`) and dependency file (`requirements.txt`) exist.

### 3. Test
Verifies that the unit test file (`test_app.py`) is present in the repository.

### 4. Deploy
Creates a deployment directory and copies `app.py` and `requirements.txt` into it.

## Execution Steps
1. Open Jenkins at `http://localhost:8080`.
2. Create a new item named `Python-MultiStage-Pipeline`.
3. Select **Pipeline** as the job type.
4. Choose **Pipeline script** in the Pipeline configuration.
5. Enter the pipeline script and save the configuration.
6. Click **Build Now** to execute the pipeline.
7. Open **Console Output** to inspect the build logs and result.

## Expected Result
The pipeline should execute the Checkout, Build, Test, and Deploy stages successfully and display:

```text
Pipeline completed successfully!
Finished: SUCCESS
```

## Screenshots
Add screenshots of the successful pipeline execution and console output in the `Screenshots/` directory.

## Conclusion
This assignment demonstrates the basic implementation of a multi-stage Jenkins pipeline for automating source checkout, application file verification, and deployment preparation.

**Note:** This simplified pipeline verifies the presence of the test file but does not execute the Python unit tests or deploy a running Flask application.
