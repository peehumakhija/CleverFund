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
│   ├── static/
│   └── tests/
│
├── data/
│   ├── ekdum_final_industry_fixed (1).xlsx
│   ├── predictions/
│   ├── shared_reports/
│   └── training_report.json
│
├── models/
│   ├── startup_model.pkl
│   └── preprocessing_info.pkl
│
├── static/
│   ├── css/
│   └── js/
│
├── templates/
│   ├── base.html
│   ├── login.html
│   ├── index.html
│   ├── reports.html
│   ├── analytics.html
│   ├── predictions.html
│   └── compare.html
│
└── tests/
```

---

## Prerequisites

Install the following:

- Python 3.9 or later
- pip
- Git
- A modern web browser
- Ollama (for local AI support)
- OpenAI API key (for OpenAI support)
- MongoDB (for optional database features)

Check Python:

```bash
python --version
```

Check pip:

```bash
pip --version
```

---

## Installation

### 1. Navigate to the project directory

Windows Command Prompt:

```bat
cd "D:\capstone front"
```

Windows PowerShell:

```powershell
Set-Location "D:\capstone front"
```

### 2. Create a virtual environment

```bash
python -m venv .venv
```

### 3. Activate the virtual environment

Windows Command Prompt:

```bat
.venv\Scripts\activate.bat
```

Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

### 4. Upgrade pip

```bash
python -m pip install --upgrade pip
```

### 5. Install project dependencies

```bash
pip install -r requirements.txt
```

### 6. Install modular backend dependencies

```bash
cd cleverfund_backend
pip install -r requirements.txt
cd ..
```

---

## Environment Configuration

Copy the example environment file.

Windows Command Prompt:

```bat
copy .env.example .env
```

Windows PowerShell:

```powershell
Copy-Item .env.example .env
```

Example `.env` configuration:

```env
SESSION_SECRET=replace-this-with-a-long-random-secret
OPENAI_API_KEY=
OPENAI_MODEL=gpt-4o-mini
LLM_PROVIDER=ollama
OLLAMA_BASE_URL=http://127.0.0.1:11434
OLLAMA_MODEL=llama3.2:3b
OLLAMA_TIMEOUT=60
STARTUP_DATASET_PATH=data/combined_dataset.xlsx
PORT=5000
DB_PATH=data/cleverfund.db
MONGO_URI=mongodb://localhost:27017
MONGO_DB=cleverfund
```

Generate a secure Flask session secret:

```bash
python -c "import secrets; print(secrets.token_hex(32))"
```

Copy the generated value into the `SESSION_SECRET` variable.

### Environment Variables

| Variable | Description |
|---|---|
| `SESSION_SECRET` | Secret key used to sign Flask session cookies |
| `OPENAI_API_KEY` | API key for OpenAI or an OpenAI-compatible provider |
| `OPENAI_MODEL` | The OpenAI model used for AI features |
| `LLM_PROVIDER` | The AI provider used by the application (`openai` or `ollama`) |
| `OLLAMA_BASE_URL` | Base URL of the local Ollama server |
| `OLLAMA_MODEL` | Name of the Ollama model |
| `OLLAMA_TIMEOUT` | Maximum time in seconds for an Ollama request |
| `STARTUP_DATASET_PATH` | Path to the startup dataset |
| `PORT` | Port used by the Flask server |
| `DB_PATH` | SQLite database file path |
| `MONGO_URI` | MongoDB connection URI |
| `MONGO_DB` | MongoDB database name |

---

## Running the Application

Start the main application:

```bash
python app.py
```

Open the application at <http://127.0.0.1:5000>

Start the modular backend:

```bash
cd cleverfund_backend
python app.py
```

Open <http://127.0.0.1:5000>

### Run with a custom port

Windows Command Prompt:

```bat
set PORT=8080
python app.py
```

Windows PowerShell:

```powershell
$env:PORT="8080"
python app.py
```

### Run using the Flask CLI

```bat
set FLASK_APP=app.py
set FLASK_ENV=development
flask run
```

### Run using Gunicorn

```bash
gunicorn app:app --bind 0.0.0.0:5000 --workers 2
```

---

## Machine Learning Model

Verify the environment:

```bash
python quickstart.py
```

Train the model:

```bash
python train.py
```

The training process creates or updates:

- `models/startup_model.pkl`
- `models/preprocessing_info.pkl`
- `data/training_report.json`
- `static/charts/`

Training features include:

- Dataset loading
- Data cleaning
- Feature preprocessing
- SMOTE balancing
- Random Forest training
- Train/test evaluation
- Feature importance calculation
- Training visualization
- Cold-start handling
- Training report generation

SMOTE helps balance datasets that contain an unequal number of successful and failed startups.

---

## Available Pages

| Page | URL | Purpose |
|---|---|---|
| Login | `/login` | User login |
| Dashboard | `/` | Prediction form and dashboard charts |
| Reports | `/reports` | Dataset reports and exports |
| Analytics | `/analytics` | Charts and startup analytics |
| Predictions | `/predictions` | Prediction history |
| Compare | `/compare` | Side-by-side startup comparison |

Most pages require an authenticated session.

---

## API Endpoints

### Register User

`POST /api/register`
Content-Type: `application/json`

Windows Command Prompt:

```bat
curl -X POST http://127.0.0.1:5000/api/register ^
  -H "Content-Type: application/json" ^
  -d "{\"email\":\"user@example.com\",\"password\":\"StrongPassword123\"}"
```

PowerShell:

```powershell
curl.exe -X POST "http://127.0.0.1:5000/api/register" `
  -H "Content-Type: application/json" `
  -d '{"email":"user@example.com","password":"StrongPassword123"}'
```

Example request:

```json
{
  "email": "user@example.com",
  "password": "StrongPassword123"
}
```

Example response:

```json
{
  "ok": true,
  "email": "user@example.com"
}
```

### Login

`POST /login`
Content-Type: `application/x-www-form-urlencoded`

Form fields:

- `email`
- `password`

### Logout

`GET /logout`

### Rule-Based Prediction

`POST /predict`
Content-Type: `application/json`

```bat
curl -X POST http://127.0.0.1:5000/predict ^
  -H "Content-Type: application/json" ^
  -d "{\"startup_name\":\"Velocity AI\",\"funding_amount\":5000000,\"employees\":50,\"industry\":\"Technology / Software\",\"revenue\":2000000,\"location\":\"Bangalore\",\"funding_round\":\"Seed\",\"years_operation\":2.5}"
```

Example response:

```json
{
  "probability": 72,
  "result": "Success",
  "scores": {
    "funding": 25,
    "team": 5,
    "revenue": 5,
    "industry": 20,
    "location": 10,
    "total": 65
  },
  "prediction_id": "example-id"
}
```

### Machine Learning Prediction

`POST /api/ml-predict`
Content-Type: `application/json`

```bat
curl -X POST http://127.0.0.1:5000/api/ml-predict ^
  -H "Content-Type: application/json" ^
  -d "{\"startup_name\":\"Velocity AI\",\"funding_amount\":5000000,\"employees\":50,\"industry\":\"Technology / Software\",\"revenue\":2000000,\"location\":\"Bangalore\"}"
```

Example response:

```json
{
  "prediction": "Success",
  "confidence": "High",
  "success_probability": 78,
  "failure_probability": 22,
  "model_type": "ML-RandomForest-SMOTE"
}
```

### Batch ML Prediction

`POST /api/ml-batch-predict`
Content-Type: `application/json`

```bat
curl -X POST http://127.0.0.1:5000/api/ml-batch-predict ^
  -H "Content-Type: application/json" ^
  -d "{\"startups\":[{\"funding_amount\":5000000,\"employees\":50,\"industry\":\"Technology / Software\",\"revenue\":2000000,\"location\":\"Bangalore\"},{\"funding_amount\":500000,\"employees\":8,\"industry\":\"Retail\",\"revenue\":100000,\"location\":\"Unknown\"}]}"
```

### Dashboard Data

`GET /api/dashboard-data`

Returns:

- Summary statistics
- Growth chart data
- Success/failure distribution
- Industry distribution
- Funding and revenue data
- Recent activity

### Analytics Data

`GET /api/analytics-data`

Returns:

- KPI values
- Volume chart
- Radar chart
- Regional success rates

### Dataset Export

`GET /api/dataset/export`

Downloads the loaded dataset as CSV.

### Prediction History

- `GET /api/prediction-history`
- `GET /api/predictions`
- `DELETE /api/prediction-history/<prediction_id>`

### PDF Export

`POST /api/export-pdf`
Content-Type: `application/json`

### Share Report

`POST /api/share-report`
Content-Type: `application/json`

### Open Shared Report

`GET /api/shared-report/<report_id>`

### AI Analysis

`POST /api/ai-analysis`
Content-Type: `application/json`

```bat
curl -X POST http://127.0.0.1:5000/api/ai-analysis ^
  -H "Content-Type: application/json" ^
  -d "{\"startup_name\":\"Velocity AI\",\"industry\":\"Technology\",\"location\":\"Bangalore\",\"funding_amount\":5000000,\"employees\":50,\"revenue\":2000000}"
```

### AI Question

`POST /api/ai-question`
Content-Type: `application/json`

### AI Dataset Insights

`GET /api/ai-dataset-insights`

### AI Feature Explanation

`POST /api/ai-explain-features`
Content-Type: `application/json`

### Clear Conversation

- `POST /api/conversation/clear`
- `POST /api/conversation/clear-all`

---

## Dataset Format

CleverFund supports CSV and Excel datasets.

Recommended columns:

| Column | Accepted Aliases | Required |
|---|---|---|
| Name | `startup_name`, `startup`, `company` | No |
| Industry | `sector` | Yes |
| Funding Amount | `funding`, `investmentamount_usd` | Yes |
| Number of Employees | `employees`, `employees_count`, `team_size` | Yes |
| Revenue | `annual_revenue` | Yes |
| Location | `city`, `region` | No |
| Success | `startup_status`, `label`, `target`, `status` | No |

Example CSV:

```csv
name,industry,funding_amount,num_employees,revenue,location,success
Velocity AI,Technology / Software,5000000,50,2000000,Bangalore,1
HealthNow,Healthcare,2500000,30,900000,Mumbai,1
RetailHub,Retail,500000,8,100000,Delhi,0
```

Set the dataset path in `.env`:

```env
STARTUP_DATASET_PATH=data/combined_dataset.xlsx
```

---

## Prediction Methods

### Rule-Based Prediction

The rule-based prediction uses:

- Funding amount
- Number of employees
- Revenue
- Industry
- Location

**Funding score:**

```text
min(funding_amount / 5,000,000, 1) × 25
```

**Team score:**

```text
min(num_employees / 200, 1) × 20
```

**Revenue score:**

```text
min(revenue / 10,000,000, 1) × 25
```

**Industry score:**

- Technology: 20
- Healthcare or Finance: 15
- Retail: 8
- Other industries: 10

**Location score:**

- Major startup location: 10
- Other locations: 5

**Final result:**

- Probability ≥ 50: Success
- Probability < 50: Failure

### Machine Learning Prediction

The machine learning prediction uses:

- Random Forest
- SMOTE
- Data preprocessing
- Missing-value handling
- Unknown-category handling
- Batch prediction
- Feature importance

---

## AI Features

### Ollama Setup

Start Ollama:

```bash
ollama serve
```

Download a model:

```bash
ollama pull llama3.2:3b
```

Configure `.env`:

```env
LLM_PROVIDER=ollama
OLLAMA_BASE_URL=http://127.0.0.1:11434
OLLAMA_MODEL=llama3.2:3b
OLLAMA_TIMEOUT=60
```

### OpenAI Setup

Configure `.env`:

```env
LLM_PROVIDER=openai
OPENAI_API_KEY=your-api-key
OPENAI_MODEL=gpt-4o-mini
```

If the AI provider is unavailable, the application may use a local fallback response or rule-based analysis.

---

## Testing

Run all tests:

```bash
pytest
```

Run tests with detailed output:

```bash
pytest -v
```

Run a specific test file:

```bash
pytest tests/test_ai_context_service.py -v
```

Run a specific test:

```bash
pytest tests/test_api_endpoints_context.py::test_name -v
```

Run smoke tests:

```bash
python test_smoke.py
```

Run prediction tests:

```bash
python test_prediction.py
```

Verify implementation:

```bash
python verify_implementation.py
```

---

## Troubleshooting

### Module Not Found

Activate the virtual environment:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
pip install -r requirements.txt
```

### Dataset Not Found

Set the dataset path in `.env`:

```env
STARTUP_DATASET_PATH=data/your-dataset.xlsx
```

Verify dataset loading:

```bash
python tools/check_dataset_load.py
```

### Machine Learning Model Not Found

Train the model:

```bash
python train.py
```

Ensure these files exist:

- `models/startup_model.pkl`
- `models/preprocessing_info.pkl`

### Port Already in Use

Change the port:

```powershell
$env:PORT="8080"
python app.py
```

### Ollama Connection Failed

Start Ollama:

```bash
ollama serve
```

Check available models:

```bash
ollama list
```

Download the configured model:

```bash
ollama pull llama3.2:3b
```

### OpenAI API Errors

Check:

- API key
- API quota
- Model name
- Internet connection
- `LLM_PROVIDER` value

### Login or Session Problems

Clear browser cookies, or generate a new session secret:

```bash
python -c "import secrets; print(secrets.token_hex(32))"
```

Update `.env`:

```env
SESSION_SECRET=new-generated-secret
```

Restart the server.

---

## Security

Before deploying publicly:

- Change `SESSION_SECRET`
- Disable Flask debug mode
- Use HTTPS
- Do not commit `.env`
- Do not commit API keys
- Restrict file uploads
- Validate API inputs
- Add rate limiting
- Add CSRF protection
- Restrict database access
- Use a production WSGI server
- Use strong passwords
- Rotate API keys
- Enable firewall rules
- Avoid exposing internal database ports
- Use environment variables for secrets

---

## Contributing

1. Fork the repository.
2. Create a feature branch:

   ```bash
   git checkout -b feature/new-feature
   ```

3. Make your changes.
4. Run tests:

   ```bash
   pytest
   ```

5. Commit your changes:

   ```bash
   git add .
   git commit -m "Add new feature"
   ```

6. Push the branch:

   ```bash
   git push origin feature/new-feature
   ```

7. Create a pull request.

---

## License

Specify the project license here, such as MIT, Apache-2.0, GPL-3.0, or Proprietary.
