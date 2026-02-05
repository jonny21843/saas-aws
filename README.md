# SaaS Consultation App (AWS Edition)

![Next.js](https://img.shields.io/badge/Next.js-16.1.6-black?style=flat-square&logo=next.js)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazon-aws&logoColor=white)

A production-ready SaaS application featuring a Next.js frontend and a FastAPI backend, fully containerized for scalable deployment on AWS infrastructure (App Runner, ECS, or EC2).

## Architecture
This project utilizes a multi-stage Docker build to optimize performance and security:
* Build Stage: Compiles the Next.js frontend into a high-performance static export.
* Runtime Stage: A slim Python environment running FastAPI that serves both the API logic and the static frontend assets.

## Getting Started

### Prerequisites
* Docker Desktop installed
* AWS CLI and AWS Tools for PowerShell configured
* A Clerk account for user authentication

### Environment Variables
Create a .env file in the root directory and add:
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_xxxxxxxx
CLERK_SECRET_KEY=sk_test_xxxxxxxx

### Local Build & Execution
To build the container (passing the public key as a build argument for the static export):

docker build --platform linux/amd64 --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY="your_clerk_key" -t consultation-app .

docker run -p 8000:8000 consultation-app

## AWS Deployment (ECR)
1. Login to ECR:
(Get-ECRLoginCommand).Password | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com

2. Tag and Push:
docker tag consultation-app:latest <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/consultation-app:latest
docker push <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com/consultation-app:latest

---
Created by Jonathan Feagans