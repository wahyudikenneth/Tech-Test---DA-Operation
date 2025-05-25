
# 🍷 MLOps Wine Quality Prediction - Technical Test

## Overview

This project demonstrates a complete MLOps pipeline for deploying a **Linear Regression** model that predicts wine quality based on physicochemical properties of wine samples. It covers:

- Model training & packaging using `scikit-learn` and `joblib` (Task 1)
- REST API deployment using `FastAPI` (Task 2)
- Logging & monitoring using `logging`, `Prometheus`, and `docker-compose` (Task 4)

---

## 🔧 Setup Instructions

### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd <your-repo-folder>
```

### 2. Environment Setup

Create and activate a virtual environment:

```bash
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`
pip install -r requirements.txt
```

Or build the image with Docker:

```bash
docker build -t wine-quality-api .
```

To run with monitoring (Task 4):

```bash
docker-compose up --build
```

---

## 🚀 How to Run the Model & API

### 🧠 Model Training (Task 1)

A **Linear Regression** model was trained on a cleaned version of the Wine Quality dataset using selected features that showed strong linear correlation with the target variable.

To retrain the model:

```bash
python task_1.py
```

This generates `model.joblib`.

### 📦 Local Prediction Script

You can use the CLI-based script to test predictions:

```bash
python predict.py
```

### 🌐 Run the REST API (Task 2)

To run the API locally:

```bash
uvicorn app:app --host 0.0.0.0 --port 8000
```

To run via Docker:

```bash
docker run -p 8000:8000 wine-quality-api
```

### 🧪 Test the API

Using `curl`:

```bash
curl -X POST http://localhost:8000/predict -H "Content-Type: application/json" -d '{"features": [7.4, 0.7, 0.0, 1.9, 0.076, 11.0, 34.0, 0.9978, 3.51, 0.56, 9.4]}'
```

Or import the included Postman collection.

---

## 📊 Monitoring & Logging (Task 4)

### 🗂 Logging

Implemented using Python’s `logging` module. Logs API access and prediction outcomes.

### 📈 Monitoring with Prometheus

Monitoring includes:

- Request latency
- Prediction success/failure count

Steps:

1. Use `docker-compose up` to start services.
2. Prometheus configuration is in `prometheus.yml`.
3. Access Prometheus at `http://localhost:9090`.

Metrics are available at `http://localhost:8000/metrics`.

---

## 📁 Deliverables Summary

- `model.joblib` — Trained Linear Regression model
- `predict.py` — Local test script
- `app.py` — REST API implementation
- `Dockerfile` — For API containerization
- `docker-compose.yml` — For Task 4 services
- `prometheus.yml` — Prometheus configuration
- `curl.txt` — Example curl command for testing
- `requirements.txt` — Python dependencies

---

## 💡 Assumptions

- **Model**: The final model is Linear Regression (chosen for generalizability over more complex overfitting models).
- **Input Format**: Features must be passed as a list of 11 float values in order.
- **Security**: Authentication/authorization is out of scope.
- **Cloud**: No cloud deployment included, but containerization supports portability.
