TelecomIQ — Enterprise Telecom Complaint Intelligence & Autonomous Triage Platform

TelecomIQ is an AI-powered telecom complaint intelligence and automated resolution platform designed to streamline subscriber complaint intake, classification, sentiment analysis, escalation-risk assessment, knowledge retrieval, and technical triage.

It combines machine learning, NLP, Retrieval-Augmented Generation (RAG), and a multi-agent workflow to transform unstructured customer complaints into structured, actionable resolution plans.

📌 Project Overview

Core Capabilities

Telecom complaint classification across 12 domain categories

PII masking for sensitive complaint information

Multilingual and Hinglish normalization

Sentiment polarity analysis

Dynamic priority and SLA-risk scoring

Historical complaint similarity search

Telecom SOP retrieval using RAG

Grounded GenAI-based technical triage

Customer, Support Agent, and Administrator workflows

Complaint queue and operational analytics

AI-assisted resolution recommendations

SQLite-based complaint and authentication persistence

Dataset

The project uses the Kaggle Telecom Complaints Monitoring System dataset containing more than 2,200 complaint records for training, evaluation, and historical complaint matching.

Core Architecture

React + Vite → FastAPI → ML/NLP → Priority & SLA Risk → RAG/Vector Search → Groq LLaMA → Structured Triage Result

🎭 Application Portals

TelecomIQ provides role-specific workflows for different operational use cases.

👤 Customer Portal

Customer registration and login

Smart complaint intake form

Preset telecom complaint scenarios

Live triage progress

Structured resolution summary

Category, sentiment, priority, and risk indicators

AI assistant for telecom guidance

🛡️ Support Agent Workspace

Real-time complaint queue

Filtering by priority, status, and category

Complete complaint inspection

Historical complaint similarity

Sentiment and escalation-risk information

AI-generated resolution drafts

Complaint status management

Customer response dispatch

👑 Administrator & NOC Dashboard

Total complaint volume

Open and resolved complaint statistics

Priority distribution

Escalation-risk monitoring

SLA-breach monitoring

Category and sentiment analytics

Complaint database inspection

CSV/data export

🔄 Autonomous 7-Stage AI Pipeline

[ Customer Complaint ]
        │
        ▼
┌─────────────────────────┐
│ 1. Ingestion & PII Mask │
│ Phone, account & IP mask │
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│ 2. Language Detection   │
│ Multilingual/Hinglish   │
│ normalization           │
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│ 3. ML Classification    │
│ TF-IDF + Logistic       │
│ Regression              │
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│ 4. Sentiment Analysis   │
│ VADER polarity scoring  │
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│ 5. Priority & SLA Risk  │
│ Multi-factor scoring    │
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│ 6. RAG & Vector Search  │
│ Historical tickets +    │
│ Telecom SOP knowledge   │
└──────────┬──────────────┘
           ▼
┌─────────────────────────┐
│ 7. GenAI Triage LLM     │
│ Grounded resolution plan│
└──────────┬──────────────┘
           ▼
[ Structured Triage Result ]

🧠 AI & ML Components

Complaint Classification

Uses TF-IDF vectorization + Logistic Regression to classify complaints into telecom-related categories.

Sentiment Analysis

Uses VADER to calculate sentiment polarity on a scale from negative to positive.

Priority & SLA Risk

Complaint priority and escalation risk are calculated using multiple complaint attributes to identify cases requiring faster intervention.

RAG & Historical Matching

TelecomIQ uses vector similarity to retrieve relevant historical complaints and telecom SOP information. This provides contextual information to the resolution pipeline.

Generative AI

When configured with a Groq API key, LLaMA-3.3-70B generates grounded technical resolution plans using the retrieved operational context.

A local/fallback SOP engine is available when live LLM generation is not configured.

🧪 Model Performance

The original project evaluation reports results on a held-out test split of 331 samples.

Category

Precision

Recall

F1-Score

Billing Dispute

0.987

0.802

0.885

Broadband Performance

0.902

0.974

0.937

Call Drops

0.667

1.000

0.800

Cancellation

0.750

1.000

0.857

Customer Service

0.889

0.889

0.889

Data / Usage Issue

0.944

0.971

0.958

Equipment / Router

0.500

1.000

0.667

Installation

1.000

0.333

0.500

Service Outage

0.539

0.778

0.636

Service Request

0.872

0.932

0.901

Weighted Average

0.902

0.891

0.890

Reported overall classification accuracy: 89.12%

🛠️ Technology Stack

Layer

Technology

Frontend

React 19, Vite, Framer Motion

Styling

Vanilla CSS

Backend

FastAPI, Python

ML & NLP

Scikit-learn, VADER, TextBlob

Classification

TF-IDF + Logistic Regression

Generative AI

Groq SDK, LLaMA-3.3-70B

RAG

Scikit-learn Cosine Similarity

Database

SQLAlchemy + SQLite

API

FastAPI REST

Deployment

Vercel

🚀 Getting Started Locally

Prerequisites

Python 3.10+

Node.js 18+

npm

Optional: GROQ_API_KEY for live LLaMA-3.3 generation

1. Clone the Repository

git clone https://github.com/rsingh001-coder/TelecomIQ.git
cd TelecomIQ

2. Backend Setup

cd backend
pip install -r requirements.txt
python start_backend.py

Backend:

http://localhost:8000

Swagger/OpenAPI documentation:

http://localhost:8000/docs

3. Frontend Setup

Open a new terminal:

cd frontend
npm install
npm run dev

Frontend:

http://localhost:5173

🔐 Environment Variables

For live Groq LLM generation, configure:

GROQ_API_KEY=your_groq_api_key

Keep API keys in a local .env file and never commit secrets to GitHub.

📁 Repository Structure

TelecomIQ/
├── backend/
│   ├── app/
│   │   ├── agents/             # Classification, sentiment, priority, Groq, etc.
│   │   ├── api/                # REST API endpoints
│   │   ├── db/                 # Database models and seed logic
│   │   ├── knowledge_base/     # Telecom SOP and policy knowledge
│   │   ├── routes/             # Authentication and agent routes
│   │   ├── schemas/            # Pydantic schemas
│   │   └── services/           # RAG, validation and auto-resolution
│   ├── data/                   # Telecom complaint dataset
│   ├── models/                 # Trained ML/vector artifacts
│   ├── scripts/                # Training and evaluation scripts
│   ├── requirements.txt
│   └── start_backend.py
├── frontend/
│   ├── src/
│   │   ├── components/         # Application components
│   │   ├── styles/             # Component styles
│   │   ├── api.js              # API client
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
├── docs/
├── loadtest/
├── reports/
├── README.md
└── vercel.json

🔮 Future Improvements

Real-time telecom network event integration

More multilingual NLP support

Advanced transformer-based complaint classification

Production-grade authentication and authorization

Distributed vector database integration

Real-time monitoring and alerting

Automated CRM/ticketing-system integration

Expanded telecom SOP knowledge base

📄 License

This project is licensed under the MIT License.
