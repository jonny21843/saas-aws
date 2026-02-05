# SaaS Consultation App (AWS Container Edition)

![Next.js](https://img.shields.io/badge/Next.js-16.1.6-black?style=for-the-badge&logo=next.js)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white)

A robust, production-grade SaaS template designed for containerized environments. This version is optimized for AWS (App Runner, ECS, or Fargate) where you want a single unified container handling both your frontend and backend.

## 🧠 How It Works: The Unified Container
Unlike traditional deployments that host the frontend and backend separately, this repo uses a Multi-Stage Docker build:
1. Stage 1 (Build): The Next.js app is compiled into static HTML/JS/CSS assets (SSG).
2. Stage 2 (Runtime): A Python/FastAPI server is initialized. It is configured to serve those static files at the root (/) while simultaneously handling dynamic API logic at (/api).
3. Result: One single URL, one single container, and zero Cross-Origin (CORS) issues.

## ✨ Key Features
- High-Performance Frontend: Built with Next.js 16 and Tailwind CSS for a modern, responsive UI.
- Secure Authentication: Integrated with Clerk for user management and protected routes.
- Python Backend: FastAPI handles heavy lifting, database interactions, and business logic.
- Cloud Ready: Platform-agnostic Docker configuration optimized for the linux/amd64 architecture.

## 📂 Project Structure
- /api: Python FastAPI source code (routes, models, schemas).
- /pages: Next.js frontend pages and components.
- /public: Static assets (images, fonts).
- Dockerfile: The automated build instructions for AWS deployment.

## 🚀 Local Setup & Build

1. Setup Environment Variables:
Create a .env file with your Clerk keys:
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_...
CLERK_SECRET_KEY=sk_test_...

2. Build the Docker Image:
docker build --platform linux/amd64 --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY="your_key" -t saas-aws .

3. Run the Container:
docker run -p 8000:8000 saas-aws

## ☁️ Deployment Path
1. Push the built image to AWS ECR (Elastic Container Registry).
2. Deploy via AWS App Runner for a managed experience, or AWS ECS for full control.
3. Ensure the PORT environment variable is set to 8000 in your AWS console.

---
Created by Jonathan Feagans