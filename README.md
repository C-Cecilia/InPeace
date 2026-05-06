# 🕊️ InPeace — NYC Venue Busyness Prediction Platform

A full-stack web application that predicts the busyness of streets and venues across Manhattan, helping users discover quieter spots in New York City. Built with a microservices architecture, machine learning pipeline, and an interactive community board for sharing recommendations.

Developed as a group project for **COMP30830 Software Engineering** at University College Dublin.

---

## 🎯 What It Does

Users can search for peaceful locations in Manhattan based on real-time busyness predictions powered by NYC taxi data. The platform provides:

- **Busyness Prediction** — Classifies any location into one of four levels: *Very Busy / Busy / Quiet / Very Quiet*, based on time of day and historical taxi patterns
- **Interactive Map** — Visualises predictions across Manhattan with clustering and dynamic updates via Leaflet and Google Maps API
- **Quiet Place Recommendations** — Suggests locations based on user preferences and current predicted busyness
- **Community Board** — Allows users to post reviews, share recommendations, and comment on locations
- **User Accounts** — Registration, login, and personal profile management

---

## 🤖 Machine Learning Pipeline

The busyness prediction model was trained on **470,000+ rows** of NYC taxi trip data combined with weather signals.

### Model Selection
Two classifiers were trained and benchmarked:

| Model | Accuracy | Inference Latency | Selected |
|-------|----------|-------------------|---------|
| K-Nearest Neighbours (KNN) | ~96% | Too slow for production | ❌ |
| Random Forest | ~94% | Acceptable | ✅ |

KNN achieved higher accuracy but was ruled out due to unacceptable inference latency at scale. **Random Forest was selected for production deployment.**

### Model Optimisation
The trained Random Forest model was approximately **500MB**, exceeding deployment constraints. Model distillation was applied to compress the model to **under 100MB** without meaningful accuracy loss, enabling successful containerised deployment.

### Prediction Classes
```
0 → Very Quiet
1 → Quiet  
2 → Busy
3 → Very Busy
```

---

## 🏗️ Architecture

The application is built on a **Docker-based microservices architecture** deployed on Google Cloud.

```
Frontend (React)
      ↓
Node.js API Gateway
      ↓
┌─────────────────────────────────────┐
│  Spring Boot Microservices          │
│  ├── Authentication Service         │
│  ├── User Service                   │
│  └── Community Service              │
└─────────────────────────────────────┘
      ↓
Flask ML Service (Busyness Prediction API)
      ↓
PostgreSQL + PostGIS (Spatial Database)
```

---

## 🛠️ Tech Stack

| Layer | Technologies |
|-------|-------------|
| Frontend | React, Leaflet, Google Maps API, Axios |
| API Gateway | Node.js |
| Backend Services | Spring Boot (Java) |
| ML Service | Flask (Python) |
| Database | PostgreSQL with PostGIS |
| ML Libraries | scikit-learn (Random Forest, KNN) |
| Deployment | Docker, Google Cloud |

---

## 👤 My Contributions

**Data & Machine Learning**
- Processed and engineered features from 470,000+ rows of NYC taxi and weather data
- Trained, evaluated, and benchmarked KNN vs Random Forest classifiers
- Made the production model selection decision based on latency benchmarking
- Applied model distillation to reduce model size from ~500MB to under 100MB for deployment

**Frontend**
- Implemented user registration and login system in React
- Built user profile pages
- Restructured and improved the homepage layout and user flow

---

## 👥 Team

| Member | Role |
|--------|------|
| Yalun Chen | Data & ML, Frontend (auth, profile, homepage) |
| Chenwei Xie | Data & ML |
| Shuya Ikeo | Frontend |
| Yang Zhao | Frontend |
| Tania Lopes | Backend |
| Caryn Su Li Ooi | Backend |

Supervised with domain guidance from the COMP30830 teaching team at University College Dublin.

---

## 🚀 Running Locally

### Prerequisites
- Docker and Docker Compose
- Google Cloud credentials (for Maps API)
- Python 3.9+
- Java 17+
- Node.js 18+

### Steps

```bash
# Clone the repository
git clone https://github.com/C-Cecilia/InPeace.git
cd InPeace

# Start all services with Docker Compose
docker-compose up --build
```

The application will be available at `http://localhost:3000`

---

## 📜 Academic Integrity

This project was developed as original coursework for COMP30830 at University College Dublin. All code was written by the team members listed above. No external code was reused beyond the documented libraries and APIs. Redistribution is not permitted without consent of all team members.
