# 🤖 3-Tier MERN Chatbot

A full-stack AI-powered chatbot built with the **MERN** stack (MongoDB, Express, React, Node.js), containerized with Docker, deployed on **AWS** (S3 + EC2 + ECR), and powered by the **Groq / Gemini AI API**. CI/CD is fully automated via **GitHub Actions**.

🌐 **Live Demo:** [mern-chatbot-sigma.vercel.app](https://mern-chatbot-sigma.vercel.app)

---

## 📐 Architecture Overview

```
┌─────────────────────────────────────────────────────┐
│                   3-Tier Architecture                │
│                                                     │
│  ┌──────────────┐    ┌──────────────┐    ┌────────┐ │
│  │   Frontend   │───▶│   Backend    │───▶│  AI    │ │
│  │   (React)    │    │  (Node/Express)│  │  API   │ │
│  │  AWS S3 /    │    │  AWS EC2 +   │   │(Groq / │ │
│  │  Vercel      │    │  Docker/ECR  │   │Gemini) │ │
│  └──────────────┘    └──────────────┘   └────────┘ │
└─────────────────────────────────────────────────────┘
```

| Tier | Technology | Hosting |
|------|-----------|---------|
| Frontend | React | AWS S3 / Vercel |
| Backend | Node.js + Express | AWS EC2 (Docker container via ECR) |
| AI Layer | Groq API / Gemini API | External API |

---

## 🗂️ Project Structure

```
3-Tier-MERN-Chatbot/
├── frontend/                  # React application
├── backend/                   # Express API server
├── .github/
│   └── workflows/             # GitHub Actions CI/CD pipelines
├── gitchatbot.yml             # Main CI/CD workflow (EC2 + S3 deploy)
├── docker-compose.yml         # Local development with Docker Compose
├── dockerfilebackend          # Dockerfile for the backend service
├── dockerfilefrontend         # Dockerfile for the frontend service
├── server.js                  # Entry point for the Node.js backend
├── .env.example               # Sample environment variables
└── package.json
```

---

## ✨ Features

- 💬 Real-time AI chat powered by **Groq** or **Gemini** APIs
- ⚛️ Responsive React frontend
- 🚀 RESTful Express backend API
- 🐳 Fully containerized with **Docker** and **Docker Compose**
- ☁️ Cloud deployment to **AWS S3** (frontend) and **AWS EC2** (backend)
- 🔄 Automated CI/CD pipeline via **GitHub Actions**
- 🔐 AWS authentication via **OIDC** (no long-lived credentials)

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) v18+
- [Docker](https://www.docker.com/) & Docker Compose
- A **Groq API key** (get one at [console.groq.com](https://console.groq.com)) or **Gemini API key**

### 1. Clone the Repository

```bash
git clone https://github.com/Damanpreet1313/3-Tier-MERN-Chatbot.git
cd 3-Tier-MERN-Chatbot
```

### 2. Set Up Environment Variables

```bash
cp .env.example .env
```

Edit `.env` and fill in your keys:

```env
GROQ_API_KEY=your_groq_api_key_here
# or
GEMINI_API_KEY=your_gemini_api_key_here
PORT=5000
```

---

## 🐳 Running with Docker Compose (Recommended)

The easiest way to run the full stack locally:

```bash
docker-compose up --build
```

| Service | URL |
|---------|-----|
| Frontend | http://localhost:3000 |
| Backend | http://localhost:5000 |

To stop:

```bash
docker-compose down
```

---

## 🛠️ Running Manually (Without Docker)

### Backend

```bash
npm install
node server.js
# Backend runs on http://localhost:5000
```

### Frontend

```bash
cd frontend
npm install
npm start
# Frontend runs on http://localhost:3000
```

---

## ☁️ CI/CD & AWS Deployment

The project uses **GitHub Actions** (`gitchatbot.yml`) for automated deployments triggered on every push to `main`.

### Pipeline Overview

```
Push to main
     │
     ├──▶ deploy-frontend
     │       ├─ Build React app
     │       └─ Sync build/ to AWS S3 bucket
     │
     └──▶ deploy-backend  (runs after frontend)
             ├─ Build Docker image
             ├─ Push to Amazon ECR
             └─ Deploy container on EC2 via SSM Run Command
```

### Required GitHub Secrets

| Secret | Description |
|--------|-------------|
| `AWS_IAM_ROLE_ARN` | IAM role ARN for OIDC authentication |
| `AWS_REGION` | AWS region (e.g. `us-east-1`) |
| `AWS_S3_BUCKET_NAME` | S3 bucket for frontend hosting |
| `AWS_ECR_REPOSITORY_NAME` | ECR repository name for backend image |
| `AWS_EC2_INSTANCE_ID` | EC2 instance ID for backend deployment |

> **Note:** Authentication is handled via **AWS OIDC** — no static IAM credentials are stored in GitHub secrets.

---

## 🔧 Environment Variables Reference

| Variable | Required | Description |
|----------|----------|-------------|
| `GROQ_API_KEY` | Yes* | API key for Groq LLM inference |
| `GEMINI_API_KEY` | Yes* | API key for Google Gemini |
| `PORT` | No | Backend server port (default: `5000`) |

*Use either Groq or Gemini depending on your configuration.

---

## 🧰 Tech Stack

| Category | Technology |
|----------|-----------|
| Frontend | React, CSS, HTML |
| Backend | Node.js, Express.js |
| AI APIs | Groq API, Google Gemini API |
| Containerization | Docker, Docker Compose |
| CI/CD | GitHub Actions |
| Cloud | AWS S3, AWS EC2, AWS ECR, AWS SSM |
| Auth | AWS OIDC (for GitHub Actions) |

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

This project is open source. Feel free to use and adapt it for your own projects.

---

## 👤 Author

**Damanpreet** — [GitHub](https://github.com/Damanpreet1313)