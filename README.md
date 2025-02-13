# 🚀 README: Jenkins Production Pipeline for ECS Deployment 🚀

## 📋 Overview
This repository contains the Jenkins pipeline configuration (`Jenkinsfile`) to deploy an application to AWS ECS (Elastic Container Service) in a **production environment**. The pipeline uses AWS credentials, Slack notifications, and ECS service updates to ensure seamless deployment. ✨

---

## Architecture Images 🖼️

### 1. ECS Deployment Architecture 🚢
![ECS Deployment Architecture](https://github.com/abdoelwaly/cicd-jenkins-aws-ecr-docker/blob/d2eeb8ca1ef65824fcace33bddc9b1da2e594761/arch/Screenshot%202025-02-11%20151140.png)


---
## 📑 Table of Contents
1. [Prerequisites 🛠️](#prerequisites-)
2. [Pipeline Description 🏗️](#pipeline-description-)
3. [Environment Variables 🌍](#environment-variables-)
4. [AWS ECS and ECR Details ☁️](#aws-ecs-and-ecr-details-)
5. [References 🔗](#references-)

---

## Prerequisites 🛠️

### 1. Jenkins Setup ⚙️
- Ensure Jenkins is installed and configured.
- Install the following Jenkins plugins:
  - **Pipeline** 🔄
  - **AWS Steps** (for AWS integration) 🌐
  - **Slack Notification** (for sending build notifications) 💬

### 2. AWS Configuration 🌐
- Create an IAM user with the following permissions:
  - `ecs:UpdateService` 🔄
  - `ecs:DescribeServices` 📋
  - `ecs:ListServices` 📊
  - `ecr:*` (if using ECR for container images) 📦
- Store the AWS credentials in Jenkins as a secret named `awscreds`.

### 3. Slack Integration 💬
- Configure Slack notifications in Jenkins by installing the **Slack Notification Plugin**.
- Set up a Slack webhook URL and configure it in Jenkins under "Manage Jenkins > Configure System > Slack".

### 4. Docker and ECR 🐳
- Ensure Docker is installed on the Jenkins agent.
- Push your Docker images to AWS ECR (Elastic Container Registry). Refer to the [CI Project](#references-) for details on building and pushing images.

---

## Pipeline Description 🏗️

### Stages 🎯
1. **Deploy to ECS Prod** 🚢
   - Updates the ECS service in the specified cluster (`jprostaging`) to force a new deployment.
   - Uses the AWS CLI command `update-service` to redeploy the service.

### Post-Build Actions ✅
- Sends a Slack notification with the build status (`SUCCESS` or `FAILURE`).
- Includes a link to the Jenkins build for more information.

---

## Environment Variables 🌍

| Variable Name | Description                          | Example Value       |
|---------------|--------------------------------------|---------------------|
| `cluster`     | Name of the ECS cluster              | `jprostaging`       |
| `service`     | Name of the ECS service              | `jproappprodsvc`    |

These variables are defined in the `environment` block of the Jenkinsfile.

---

## AWS ECS and ECR Details ☁️

### ECS Cluster and Service 🚢
- **Cluster Name**: `jprostaging`
- **Service Name**: `jproappprodsvc`

### ECR Repository 📦
- Ensure your Docker image is pushed to the ECR repository before running this pipeline.
- Example ECR repository URI: `123456789012.dkr.ecr.us-east-1.amazonaws.com/jproapp`

---

###  CI/CD Pipeline Flow 🔄
![CI/CD Pipeline Flow](https://github.com/abdoelwaly/cicd-jenkins-aws-ecr-docker/blob/d2eeb8ca1ef65824fcace33bddc9b1da2e594761/arch/Screenshot%202025-02-11%20151537.png)

---

## References 🔗

### Previous CI Project 📂
For details on the CI project:
- **Repository Link**: [CI Project Repository](https://github.com/abdoelwaly/ci-jenkins-nexus-sonarq)
