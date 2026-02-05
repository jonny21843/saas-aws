Markdown
# SaaS Consultation App (AWS Edition)

![Next.js](https://img.shields.io/badge/Next.js-16.1.6-black?style=flat-square&logo=next.js)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![Docker](https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white)
![AWS](https://img.shields.io/badge/AWS-232F3E?style=flat-square&logo=amazon-aws&logoColor=white)

A high-performance SaaS application featuring a **Next.js** frontend served through a **FastAPI** backend, fully containerized for deployment on AWS (App Runner, ECS, or EC2).

## 🏗️ Architecture
This project uses a multi-stage Docker build to optimize image size and security:
- **Build Stage**: Compiles the Next.js frontend into a static export.
- **Runtime Stage**: A slim Python environment that serves the static frontend and handles API requests.

## 🚀 Getting Started

### Prerequisites
- Docker Desktop
- AWS CLI & AWS Tools for PowerShell
- Clerk Account (for Authentication)

### Environment Variables
Create a `.env` file in the root:
```env
NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY=pk_test_xxxxxxxx
CLERK_SECRET_KEY=sk_test_xxxxxxxx
Local Build & Run
To build the image (using build arguments for Clerk keys):

PowerShell
docker build `
  --platform linux/amd64 `
  --build-arg NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY="your_key_here" `
  -t consultation-app .

docker run -p 8000:8000 consultation-app
☁️ Deployment to AWS ECR
Login to ECR:

PowerShell
(Get-ECRLoginCommand).Password | docker login --username AWS --password-stdin <aws_account_id>.dkr.ecr.us-east-1.amazonaws.com
Tag the image:

PowerShell
docker tag consultation-app:latest <aws_account_id>[.dkr.ecr.us-east-1.amazonaws.com/consultation-app:latest](https://.dkr.ecr.us-east-1.amazonaws.com/consultation-app:latest)
Push to ECR:

PowerShell
docker push <aws_account_id>[.dkr.ecr.us-east-1.amazonaws.com/consultation-app:latest](https://.dkr.ecr.us-east-1.amazonaws.com/consultation-app:latest)

---

### 2. For your `saas-vercel` repository
```markdown
# SaaS Consultation App (Vercel Edition)

![Next.js](https://img.shields.io/badge/Next.js-16.1.6-black?style=flat-square&logo=next.js)
![Vercel](https://img.shields.io/badge/Vercel-000000?style=flat-square&logo=vercel&logoColor=white)
![Clerk](https://img.shields.io/badge/Clerk-6C47FF?style=flat-square&logo=clerk&logoColor=white)

An optimized version of the SaaS Consultation App designed for serverless deployment. This version leverages Vercel's native support for Next.js and integrated Python API functions.

## 🛠️ Tech Stack
- **Frontend**: Next.js 16 (App Router), TypeScript, Tailwind CSS.
- **Backend**: Python/FastAPI (Integrated via the `/api` directory).
- **Auth**: Clerk Authentication.

## ⚡ Development

1. **Install Dependencies**:
   ```bash
   npm install
   pip install -r requirements.txt
Run the Development Server:

Bash
npm run dev
The Python API will be automatically proxied via Vercel's dev environment.

🚀 Deployment
Deploying to Vercel is seamless:

Push your code to GitHub.

Connect the repository in the Vercel Dashboard.

Set your NEXT_PUBLIC_CLERK_PUBLISHABLE_KEY and CLERK_SECRET_KEY in the Environment Variables section.

Vercel handles the rest, deploying your frontend as a global application and your Python files as Serverless Functions.

Created by Jonathan Feagans