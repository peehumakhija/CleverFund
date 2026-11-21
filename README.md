# CleverFund

CleverFund is a full-stack startup success prediction platform built with Flask. It combines rule-based predictions, machine learning predictions, startup analytics, AI-generated insights, report exports, document analysis, authentication, and prediction history.

## Table of Contents

- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation](#installation)
- [Environment Configuration](#environment-configuration)
- [Running the Application](#running-the-application)
- [Machine Learning Model](#machine-learning-model)
- [Available Pages](#available-pages)
- [API Endpoints](#api-endpoints)
- [Dataset Format](#dataset-format)
- [Prediction Methods](#prediction-methods)
- [AI Features](#ai-features)
- [Testing](#testing)
- [Troubleshooting](#troubleshooting)
- [Security](#security)
- [Contributing](#contributing)
- [License](#license)

---

## Features

- Startup success prediction
- Rule-based prediction scoring
- Random Forest machine learning prediction
- SMOTE handling for imbalanced datasets
- Cold-start handling for incomplete startup data
- Batch startup prediction
- Interactive dashboard
- Startup reports and analytics
- Prediction history
- PDF report generation
- Shareable reports
- CSV dataset export
- Startup document upload
- AI-generated startup analysis
- AI dataset insights
- AI feature explanations
- Multi-turn AI questions
- User registration and login
- Responsive HTML, CSS, and JavaScript interface
- SQLite database support
- Optional MongoDB support

---

## Technology Stack

**Backend**

- Python
- Flask
- SQLite
- Pandas
- NumPy
- Scikit-learn
- Imbalanced-learn
- XGBoost
- Joblib
- OpenAI API
- Ollama
- PyMongo
- ReportLab
- OpenPyXL
- PyPDF

**Frontend**

- HTML5
- CSS3
- JavaScript
- Jinja2
- Chart.js

---

## Project Structure

```text
capstone front/
├── app.py
├── dataset.py
├── document_input.py
├── export_utils.py
├── generate_dataset.py
├── predict_startup_success.py
├── train.py
├── quickstart.py
├── requirements.txt
├── .env
├── .env.example
├── README.md
│
├── cleverfund_backend/
│   ├── app.py
│   ├── requirements.txt
│   ├── check_mongo.py
│   ├── models/
│   │   ├── __init__.py
│   │   └── database.py
│   ├── routes/
│   │   ├── __init__.py
│   │   ├── auth.py
│   │   ├── pages.py
│   │   └── api.py
│   ├── services/
│   │   ├── __init__.py
│   │   ├── auth_service.py
│   │   ├── prediction_service.py
│   │   ├── dataset_service.py
│   │   ├── llm_service.py
│   │   ├── ai_context_service.py
│   │   └── conversation_service.py
│   ├── templates/
│
