# 🚀 AI-Powered-Technical-Interview

An AI-driven full-stack web application designed to simulate real-world technical interviews.  
The system dynamically generates interview questions and evaluates user responses using a locally hosted Large Language Model (LLM).

This project demonstrates the integration of modern AI systems within a scalable MERN-based architecture.

---

## 🎯 Project Objective

Technical interviews require both conceptual clarity and problem-solving ability.  
This platform provides an interactive environment where users can:

- Practice coding interviews
- Attempt conceptual questions
- Submit voice-based answers
- Receive structured AI feedback
- Track performance analytics over time

The application is built using a microservice-inspired architecture to isolate AI computation from the core backend.

---

## 🏗️ System Architecture

The system is divided into three major layers:

### 1️⃣ Frontend (React + Vite)

Responsible for:
- Interview UI
- Code editor integration (Monaco)
- Audio recording
- Performance visualization
- Authentication handling

The frontend communicates with the Node.js backend via REST APIs.

---

### 2️⃣ Backend API (Node.js + Express)

Acts as the **API Gateway**.

Responsibilities:
- User authentication (JWT)
- Password hashing (bcrypt)
- Session storage in MongoDB
- Request validation
- Forwarding AI-related requests to the Python microservice

The backend does NOT perform heavy AI computation.

---

### 3️⃣ AI Microservice (FastAPI - Python)

Handles all AI-related operations:

- Dynamic question generation
- Evaluation of coding answers
- Analysis of conceptual responses
- Speech-to-text processing
- Interaction with the local LLM

This separation improves scalability and maintainability.

---

### 4️⃣ Local LLM Engine (Ollama - Mistral Model)

The system uses Ollama to run the Mistral model locally.

Why local LLM?

- No external API cost
- Offline capability
- Data privacy
- Full control over model usage

The AI microservice communicates with Ollama through REST calls.

---

## 🔄 Data Flow Overview

User → React Frontend  
⬇  
Node.js Backend (Authentication + DB)  
⬇  
Python FastAPI Service  
⬇  
Ollama (Mistral LLM)  
⬆  
AI Response → Stored in MongoDB → Displayed in UI  

---

## ✨ Core Features

### 🔹 Role-Based Interview Configuration
Users can select:
- Domain (MERN, Python, Data Science, etc.)
- Difficulty level
- Interview type (Coding / Conceptual / Mixed)

---

### 🔹 Coding Interview Mode
- Integrated Monaco Editor
- Users write and submit code
- AI evaluates logic and structure
- Generates detailed feedback

---

### 🔹 Conceptual Interview Mode
- Text-based answers supported
- Voice-based answers supported
- Speech converted using Whisper
- AI evaluates understanding and clarity

---

### 🔹 AI Evaluation Metrics
The system provides:
- Technical Score
- Confidence Score
- Improvement Suggestions
- Structured feedback output

---

### 🔹 Analytics Dashboard
- Interview session history
- Score breakdown per question
- Performance visualization using Chart.js
- Progress tracking

---

### 🔐 Secure Authentication
- JWT-based authentication
- Encrypted password storage (bcrypt)
- Protected routes
- Environment-based configuration

---

## 🛠️ Technology Stack

### Frontend
- React (Vite)
- Redux Toolkit
- Tailwind CSS
- Monaco Editor
- Chart.js

### Backend
- Node.js
- Express.js
- MongoDB
- Mongoose
- JWT Authentication

### AI Microservice
- Python 3.9+
- FastAPI
- Ollama (Mistral LLM)
- OpenAI Whisper
- FFmpeg (audio preprocessing)

---

## 🚀 Installation Guide

### 🔧 Prerequisites

Make sure you have:

- Node.js (v16+)
- Python (v3.9+)
- MongoDB (local or Atlas)
- Ollama installed locally
- FFmpeg added to system PATH

---

### 🧠 Step 1 — Start LLM

```bash
ollama pull mistral
ollama serve

## Step 2 — Start AI Microservice

cd ai-service
python -m venv venv
venv\Scripts\activate
pip install fastapi uvicorn ollama openai-whisper pydub python-dotenv python-multipart
uvicorn main:app --reload --port 8000

## Step 3 — Start Backend

cd backend
npm install
node server.js

## Step 4 — Start Frontend

cd frontend
npm install
npm run dev

## 🔐 Environment Variables Setup

This project requires environment variables for proper configuration.  
Create a `.env` file inside the respective folders as described below.

---

### 📁 Backend (.env inside `/backend` folder)

Create a file:
backend/.env


Add the following:

```env
PORT=5000
MONGO_URI=mongodb://127.0.0.1:27017/ai_interview_db
JWT_SECRET=your_super_secure_jwt_secret_key
NODE_ENV=development
AI_SERVICE_URL=http://127.0.0.1:8000
🔎 Variable Explanation

PORT → Port on which the backend server runs

MONGO_URI → MongoDB connection string (local or Atlas)

JWT_SECRET → Secret key used to sign authentication tokens

NODE_ENV → Environment mode (development / production)

AI_SERVICE_URL → URL of the Python AI microservice

## AI Microservice (.env inside /ai-service folder)

Create:

ai-service/.env

Add:

AI_SERVICE_PORT=8000
OLLAMA_MODEL_NAME=mistral
🔎 Variable Explanation

AI_SERVICE_PORT → Port for FastAPI service

OLLAMA_MODEL_NAME → Local LLM model name (default: mistral)

## Frontend (.env inside /frontend folder)

Create:

frontend/.env

Add:

VITE_API_URL=http://localhost:5000/api