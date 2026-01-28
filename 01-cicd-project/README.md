# CI/CD Pipeline: Jenkins – SonarQube – Docker – AWS ECS

## Introduction
This project demonstrates a production-ready CI/CD pipeline for containerized applications using Jenkins, SonarQube, Docker, and AWS ECS.
The pipeline automatically:
- Fetches source code from GitHub
- Runs unit tests and static code checks
- Enforces code quality via SonarQube Quality Gate
- Builds Docker images
- Pushes images to AWS ECR
- Deploys applications to AWS ECS
- Sends build notifications to Slack
The goal of this project is to showcase DevOps best practices including automation, code quality enforcement, containerization, and cloud-native deployment.

## Architecture
<img width="2522" height="1372" alt="image" src="https://github.com/user-attachments/assets/a54fa588-6122-43fa-b5d0-85ab3925157c" />

# Workflow details
```mermaid
sequenceDiagram
    participant Dev as Developer
    participant GH as GitHub
    participant JK as Jenkins
    participant SQ as SonarQube
    participant ECR as AWS ECR
    participant ECS as AWS ECS
    participant SL as Slack

    Dev->>GH: Push code
    GH->>JK: Webhook trigger
    JK->>JK: Fetch source code
    JK->>JK: Run unit tests
    JK->>JK: Run Checkstyle
    JK->>SQ: Send code for analysis
    SQ-->>JK: Quality Gate result
    alt Quality Gate PASSED
        JK->>JK: Build Docker image
        JK->>ECR: Push image
        ECR-->>ECS: New image available
        JK->>ECS: Deploy updated service
        JK->>SL: Notify success
    else Quality Gate FAILED
        JK->>SL: Notify failure
    end
```

## Tech Stack
CICD & Devops
- Jenkins
- GitHub
- SonarQube
- Docker
Cloud & Container
- AWS ECS
- AWS ECR
- AWS IAM
Other
- sonarQube Quality Gate
- Slack Integration
