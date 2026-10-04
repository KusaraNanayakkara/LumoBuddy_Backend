# LumoBuddy ML API 🚀

An intelligent Machine Learning REST API for the **LumoBuddy** platform, built with **FastAPI** and **scikit-learn**. This service processes child screening and assessment survey scores to provide predictions, confidence scores, and personalized game level recommendations.

---

## 📋 Features

- **Fast & Lightweight:** Built using FastAPI with asynchronous request handling and minimal latency.
- **ML-Powered Screening:** Uses a pre-trained scikit-learn model (`autism_model.pkl`) to evaluate survey inputs.
- **Dynamic Level Recommendation:** Translates survey metrics into suggested interactive game difficulty levels (Level 1, Level 2, Level 3).
- **Interactive Documentation:** Automatic Swagger UI (`/docs`) and ReDoc (`/redoc`) generation.
- **Containerized & Deployment-Ready:** Includes a multi-stage `Dockerfile`, Render configuration (`render.yaml`), and Vercel configuration (`vercel.json`).

---

## 🛠️ Tech Stack

- **Framework:** [FastAPI](https://fastapi.tiangolo.com/)
- **Server:** [Uvicorn](https://www.uvicorn.org/)
- **Machine Learning:** [scikit-learn](https://scikit-learn.org/), [joblib](https://joblib.readthedocs.io/)
- **Data Processing:** [Pandas](https://pandas.pydata.org/)
- **Containerization:** [Docker](https://www.docker.com/)

---

## 📁 Project Structure

```text
lumo_buddy_ml_api/
├── model/
│   └── autism_model.pkl      # Pre-trained ML model and feature definitions
├── Dockerfile                # Container definition for production deployment
├── main.py                   # FastAPI application & ML inference endpoints
├── render.yaml               # Infrastructure-as-code for Render deployment
├── requirements.txt          # Python dependencies
├── vercel.json               # Serverless deployment configuration
└── README.md                 # Project documentation
```

---

## 🚀 Getting Started

### Prerequisites

- Python 3.10+
- Git

### 1. Clone the Repository

```bash
git clone https://github.com/KusaraNanayakkara/LumoBuddy_Backend.git
cd LumoBuddy_Backend
```

### 2. Create a Virtual Environment

```bash
# Windows (PowerShell)
python -m venv venv
.\venv\Scripts\Activate.ps1

# Linux / macOS
python3 -m venv venv
source venv/bin/activate
```

### 3. Install Dependencies

```bash
pip install -r requirements.txt
```

### 4. Run the Development Server

```bash
uvicorn main:app --reload --host 0.0.0.0 --port 8000
```

Once running, access:
- **API Base:** `http://127.0.0.1:8000`
- **Interactive Swagger Docs:** `http://127.0.0.1:8000/docs`
- **ReDoc Documentation:** `http://127.0.0.1:8000/redoc`

---

## 📡 API Endpoints

### 1. Health Check

Verifies the service status.

- **URL:** `/`
- **Method:** `GET`
- **Response:**
  ```json
  {
    "status": "running",
    "message": "LUMO BUDDY ML API is working"
  }
  ```

---

### 2. Predict Screening & Game Level

Evaluates survey scores and returns screening predictions and level recommendations.

- **URL:** `/predict`
- **Method:** `POST`
- **Content-Type:** `application/json`

#### Request Body Example:
```json
{
  "emotion_score": 12,
  "cognitive_score": 15,
  "self_awareness_score": 10,
  "math_score": 8,
  "total_score": 45
}
```

#### Response Example:
```json
{
  "screening_prediction": 1,
  "predicted_level": 2,
  "confidence": 0.88,
  "recommendation": "Suggested game level: Level 2"
}
```

#### Level Mapping Logic:
| Total Score Range | Recommended Level |
|-------------------|-------------------|
| `score <= 40`     | **Level 1**       |
| `41 <= score <= 85` | **Level 2**     |
| `score > 85`      | **Level 3**       |

---

## 🐳 Docker Setup

You can build and run the application locally using Docker:

```bash
# Build the Docker image
docker build -t lumobuddy-ml-api .

# Run the container on port 10000
docker run -p 10000:10000 lumobuddy-ml-api
```

The API will be accessible at `http://localhost:10000`.

---

## ☁️ Deployment

### Render
This repository includes a [`render.yaml`](./render.yaml) file for automatic web service deployment on [Render](https://render.com/). Simply connect the repository to Render as a Blueprint.

### Vercel
Configuration is provided via [`vercel.json`](./vercel.json) for serverless Python deployment on [Vercel](https://vercel.com/).

---

## 📄 License
This project is developed as part of the LumoBuddy Final Year Project. All rights reserved.