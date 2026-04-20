# Calculation Service API

## Overview
This is a FastAPI-based application that supports user authentication and calculation operations.
The application allows users to register, log in, and perform calculations such as addition, subtraction,
multiplication, and division. Results are computed dynamically instead of being stored in the database.

---

## Tech Stack
- FastAPI
- SQLAlchemy
- PostgreSQL
- Pydantic
- Pytest
- Docker
- GitHub Actions (CI/CD)

---

## Running the Application

### 1. Navigate to the project directory
```bash
cd assignment-12
```

### 2. Install dependencies
```bash
pip install -r requirements.txt
```

### 3. Run the server
```bash
uvicorn app.main:app --reload
```

### 4. Open in browser
```
http://127.0.0.1:8000/docs
```

---

## Running Tests

### Run all tests
```bash
pytest
```

### Run unit tests
```bash
pytest tests/unit/
```

### Run integration tests
```bash
pytest tests/integration/
```

### Run e2e tests
```bash
pytest tests/e2e/
```

---

## Manual Testing via OpenAPI (Swagger)

1. Open Swagger UI:
```
http://127.0.0.1:8000/docs
```

### Step 1: Register a User
Use POST `/auth/register`

Example:
```json
{
  "first_name": "Mostafa",
  "last_name": "Salah",
  "email": "mostafa.test@example.com",
  "username": "mostafa_test",
  "password": "SecurePass123!",
  "confirm_password": "SecurePass123!"
}
```

---

### Step 2: Login
Use POST `/auth/login`

```json
{
  "username": "mostafa_test",
  "password": "SecurePass123!"
}
```

Copy the access token.

---

### Step 3: Authorize
Click **Authorize** and paste:
```
Bearer YOUR_ACCESS_TOKEN
```

---

### Step 4: Create Calculation
POST `/calculations`

```json
{
  "type": "addition",
  "inputs": [10, 5],
  "user_id": "ignored"
}
```

Response:
```json
{
  "result": 15
}
```

---

## Notes
- Results are NOT stored in the database.
- Calculations are computed dynamically.
- CI/CD pipeline runs tests, security scan, and deploys Docker image.

---

## CI/CD Pipeline
- Runs unit, integration, and e2e tests
- Scans Docker image using Trivy
- Pushes image to Docker Hub on successful runs