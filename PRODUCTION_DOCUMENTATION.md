# ScoreSight - Production Documentation

**Version:** 1.0.0  
**Last Updated:** November 16, 2025  
**Author:** Amit Kumar

---

## Table of Contents

1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Technology Stack](#technology-stack)
4. [Features](#features)
5. [Prerequisites](#prerequisites)
6. [Local Development Setup](#local-development-setup)
7. [Production Deployment](#production-deployment)
8. [API Documentation](#api-documentation)
9. [Frontend Routes](#frontend-routes)
10. [Database Schema](#database-schema)
11. [Machine Learning Models](#machine-learning-models)
12. [Environment Variables](#environment-variables)
13. [Custom Domain Setup](#custom-domain-setup)
14. [Monitoring & Logging](#monitoring--logging)
15. [Troubleshooting](#troubleshooting)
16. [Security Best Practices](#security-best-practices)
17. [Performance Optimization](#performance-optimization)
18. [Backup & Recovery](#backup--recovery)
19. [CI/CD Pipeline](#cicd-pipeline)
20. [Contributing](#contributing)
21. [License](#license)

---

## Project Overview

**ScoreSight** is a full-stack web application that uses machine learning to predict English Premier League (EPL) match outcomes. The system analyzes historical match statistics and provides real-time predictions with confidence scores.

### Key Capabilities
- **Match Outcome Prediction**: Predicts Home Win, Draw, or Away Win
- **Score Prediction**: Suggests likely goal scores for both teams
- **Confidence Analysis**: Provides probability distribution across all outcomes
- **User Management**: Secure authentication and personalized dashboards
- **AI Chatbot**: Interactive conversational assistant for user support
- **Prediction History**: Track and analyze past predictions

---

## Architecture

### System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────┐
│                         CLIENT LAYER                        │
│  ┌──────────────────────────────────────────────────────┐  │
│  │   Browser (Chrome, Firefox, Safari, Edge)            │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────┬───────────────────────────────────────┘
                      │ HTTPS
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                   PRESENTATION LAYER                        │
│  ┌──────────────────────────────────────────────────────┐  │
│  │         Vercel Static Hosting (CDN)                  │  │
│  │  - HTML5, CSS3, JavaScript ES6+                      │  │
│  │  - Bootstrap 5 UI Framework                          │  │
│  │  - Responsive Design (Mobile-First)                  │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────┬───────────────────────────────────────┘
                      │ REST API (JSON)
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                    APPLICATION LAYER                        │
│  ┌──────────────────────────────────────────────────────┐  │
│  │         Render Web Service (Python)                  │  │
│  │  - Django 4.2+ Framework                             │  │
│  │  - Django REST Framework (DRF)                       │  │
│  │  - Gunicorn WSGI Server                              │  │
│  │  - WhiteNoise (Static Files)                         │  │
│  └──────────────────────────────────────────────────────┘  │
└─────────────────────┬───────────────────────────────────────┘
                      │
                      ▼
┌─────────────────────────────────────────────────────────────┐
│                      DATA LAYER                             │
│  ┌────────────────────┐  ┌──────────────────────────────┐  │
│  │   SQLite Database  │  │   ML Models (scikit-learn)   │  │
│  │  - User Profiles   │  │  - Classifier (Outcome)      │  │
│  │  - Predictions     │  │  - Regressor (Goal Diff)     │  │
│  │  - History         │  │  - Feature Scaler            │  │
│  └────────────────────┘  └──────────────────────────────┘  │
└─────────────────────────────────────────────────────────────┘
```

### Data Flow

```
User Input → Frontend Validation → API Request → Backend Processing
                                                         ↓
                                              Feature Engineering
                                                         ↓
                                              Model Prediction
                                                         ↓
                                              Response Formatting
                                                         ↓
                                              JSON Response
                                                         ↓
User Interface ← Result Display ← Frontend Processing ←
```

---

## Technology Stack

### Frontend
| Technology | Version | Purpose |
|------------|---------|---------|
| HTML5 | Latest | Structure and semantic markup |
| CSS3 | Latest | Styling with glassmorphism effects |
| JavaScript | ES6+ | Client-side logic and interactivity |
| Bootstrap | 5.3+ | Responsive UI components |
| Font Awesome | 6.0+ | Icons and visual elements |
| Google Fonts | - | Poppins font family |

### Backend
| Technology | Version | Purpose |
|------------|---------|---------|
| Python | 3.12.0 | Core programming language |
| Django | 4.2+ | Web framework |
| Django REST Framework | 3.14+ | API development |
| Gunicorn | 21.2+ | WSGI HTTP server |
| WhiteNoise | 6.5+ | Static file serving |
| CORS Headers | 4.0+ | Cross-origin resource sharing |

### Machine Learning
| Library | Version | Purpose |
|---------|---------|---------|
| scikit-learn | 1.3+ | ML algorithms and preprocessing |
| pandas | 2.0+ | Data manipulation |
| numpy | 1.24+ | Numerical computing |
| joblib | 1.3+ | Model serialization |

### Deployment & Infrastructure
| Service | Purpose |
|---------|---------|
| Vercel | Frontend hosting with CDN |
| Render | Backend hosting (Python) |
| GitHub | Version control and CI/CD |
| SQLite | Database (production-ready for small-scale) |

---

## Features

### 1. User Authentication
- **Signup**: Create new account with name, email, password
- **Login**: Secure authentication with session management
- **Logout**: Clear session and redirect to login
- **Protected Routes**: Dashboard, Predict, AI Predictor pages require authentication

### 2. Match Prediction
- **Input Fields** (15+ statistics):
  - Half-Time Goals (Home/Away)
  - Shots (Home/Away)
  - Shots on Target (Home/Away)
  - Corners (Home/Away)
  - Fouls (Home/Away)
  - Yellow Cards (Home/Away)
  - Red Cards (Home/Away)
- **Output**:
  - Predicted Outcome (Home Win/Draw/Away Win)
  - Confidence Score (%)
  - Predicted Score (Home Goals - Away Goals)
  - Probability Distribution
  - Expected Points for each team

### 3. AI Chatbot
- **Conversational AI**: Human-like responses with greetings, small talk
- **Typing Simulation**: Realistic chat experience
- **Context-Aware**: Understands ScoreSight-specific queries
- **Persistent Chat**: Conversation history maintained in session

### 4. Dashboard
- **User Statistics**: Total predictions, accuracy rate
- **Quick Actions**: Navigate to Predict Match, AI Predictor
- **Personalized Greeting**: Display user name
- **Recent Activity**: View prediction history

### 5. Prediction History
- **Track Predictions**: All past match predictions stored
- **Accuracy Tracking**: Compare predictions with actual results
- **User Profile**: Predictions count, correct predictions, accuracy %

---

## Prerequisites

### For Local Development
- **Python**: 3.10 or higher
- **pip**: Latest version
- **Git**: For version control
- **Code Editor**: VS Code (recommended) or any IDE
- **Web Browser**: Chrome, Firefox, Safari, or Edge

### For Production Deployment
- **GitHub Account**: For version control
- **Vercel Account**: For frontend hosting (free tier available)
- **Render Account**: For backend hosting (free tier available)
- **Domain Name** (Optional): For custom domain setup

---

## Local Development Setup

### Backend Setup

1. **Clone the Repository**
```powershell
git clone https://github.com/ankit-kumarz/ScoreSight_backend.git
cd ScoreSight_backend
```

2. **Create Virtual Environment**
```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

3. **Install Dependencies**
```powershell
pip install -r requirements.txt
```

4. **Copy ML Models to Artifacts**
```powershell
# Ensure artifacts/ folder contains:
# - match_outcome_classifier.pkl
# - goal_diff_regressor.pkl
# - feature_scaler.pkl
# - model_meta.json
```

5. **Run Migrations**
```powershell
python manage.py migrate
```

6. **Create Superuser (Optional)**
```powershell
python manage.py createsuperuser
```

7. **Collect Static Files**
```powershell
python manage.py collectstatic --noinput
```

8. **Start Development Server**
```powershell
python manage.py runserver
```

Backend will be available at: `http://localhost:8000`

### Frontend Setup

1. **Clone the Repository**
```powershell
git clone https://github.com/ankit-kumarz/ScoreSight_frontend.git
cd ScoreSight_frontend
```

2. **Update API Configuration**
Edit `assets/script.js`:
```javascript
const API_BASE = 'http://localhost:8000';
```

3. **Open in Browser**
Simply open `login.html` in your browser or use a local server:
```powershell
# Using Python
python -m http.server 3000

# Using Node.js (if installed)
npx serve
```

Frontend will be available at: `http://localhost:3000`

---

## Production Deployment

### Backend Deployment (Render)

#### Step 1: Prepare Repository

1. **Ensure these files exist in your repo**:
   - `Procfile`
   - `runtime.txt`
   - `requirements.txt`
   - `.gitignore`
   - `artifacts/` folder with ML models

2. **Push to GitHub**:
```powershell
git add .
git commit -m "Prepare for production deployment"
git push origin main
```

#### Step 2: Create Render Web Service

1. Go to [Render Dashboard](https://dashboard.render.com)
2. Click **New +** → **Web Service**
3. Connect your GitHub repository: `ScoreSight_backend`
4. Configure settings:
   - **Name**: `scoresight-backend`
   - **Region**: Choose closest to your users
   - **Branch**: `main`
   - **Runtime**: `Python 3`
   - **Build Command**: `pip install -r requirements.txt`
   - **Start Command**: `gunicorn scoresight_backend.wsgi:application`
   - **Instance Type**: `Free` (or paid tier for better performance)

5. **Add Environment Variables**:
   - `SECRET_KEY`: Generate strong secret key
   - `DEBUG`: `False`
   - `PYTHON_VERSION`: `3.12.0`

6. Click **Create Web Service**

#### Step 3: Verify Deployment

1. Wait for build to complete (~2-3 minutes)
2. Visit: `https://your-service.onrender.com/`
3. You should see: `{"status": "online", "service": "ScoreSight Backend API"...}`
4. Test health endpoint: `https://your-service.onrender.com/api/health`

### Frontend Deployment (Vercel)

#### Step 1: Prepare Repository

1. **Update Backend URL in `assets/script.js`**:
```javascript
const API_BASE = window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1'
  ? 'http://localhost:8000'
  : 'https://scoresight-backend.onrender.com';  // Your Render URL
```

2. **Ensure `vercel.json` exists**:
```json
{
  "rewrites": [
    { "source": "/", "destination": "/login.html" },
    { "source": "/(.*)", "destination": "/$1" }
  ]
}
```

3. **Push to GitHub**:
```powershell
git add .
git commit -m "Configure for Vercel deployment"
git push origin main
```

#### Step 2: Deploy to Vercel

1. Go to [Vercel Dashboard](https://vercel.com/dashboard)
2. Click **Add New** → **Project**
3. Import `ScoreSight_frontend` repository
4. Configure settings:
   - **Framework Preset**: Other
   - **Root Directory**: `./`
   - **Build Command**: Leave empty
   - **Output Directory**: `./`
5. Click **Deploy**

#### Step 3: Update Backend CORS

1. **Edit `scoresight_backend/settings.py`**:
```python
CORS_ALLOWED_ORIGINS = [
    'http://localhost:3000',
    'http://127.0.0.1:3000',
    'https://your-vercel-app.vercel.app',  # Your Vercel URL
]
CORS_ALLOWED_ORIGIN_REGEXES = [
    r"^https://your-vercel-app.*\.vercel\.app$",
]
```

2. **Commit and push**:
```powershell
cd ScoreSight_backend
git add .
git commit -m "Update CORS for Vercel"
git push origin main
```

3. Wait for Render to auto-redeploy (~2 minutes)

#### Step 4: Verify Deployment

1. Visit your Vercel URL: `https://your-vercel-app.vercel.app`
2. You should see the login page
3. Create an account and test predictions

---

## API Documentation

### Base URL
- **Production**: `https://scoresight-backend.onrender.com/api`
- **Local**: `http://localhost:8000/api`

### Authentication
Most endpoints support anonymous access for demo purposes. User-specific features require authentication.

### Endpoints

#### 1. Health Check
```http
GET /api/health
```

**Response**:
```json
{
  "status": "ok",
  "model": "sklearn",
  "version": "v2"
}
```

#### 2. Get Teams List
```http
GET /api/teams
```

**Response**:
```json
{
  "teams": [
    "Arsenal", "Chelsea", "Liverpool", "Man United", 
    "Man City", "Tottenham", ...
  ]
}
```

#### 3. User Signup
```http
POST /api/signup
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Success Response** (201):
```json
{
  "status": "success",
  "name": "John Doe",
  "email": "john@example.com"
}
```

**Error Response** (400):
```json
{
  "status": "error",
  "message": "Email already registered."
}
```

#### 4. User Login
```http
POST /api/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "securePassword123"
}
```

**Success Response** (200):
```json
{
  "status": "success",
  "name": "John Doe",
  "email": "john@example.com"
}
```

**Error Response** (401):
```json
{
  "status": "error",
  "message": "Invalid email or password."
}
```

#### 5. Match Prediction
```http
POST /api/predict_v2
Content-Type: application/json

{
  "home_team": "Arsenal",
  "away_team": "Chelsea",
  "match_date": "2025-11-20",
  "HTHG": 1,
  "HTAG": 0,
  "HS": 12,
  "AS": 8,
  "HST": 5,
  "AST": 3,
  "HC": 6,
  "AC": 4,
  "HF": 10,
  "AF": 12,
  "HY": 2,
  "AY": 3,
  "HR": 0,
  "AR": 0
}
```

**Response** (200):
```json
{
  "outcome": "Home Win",
  "probabilities": {
    "home_win": 0.65,
    "draw": 0.25,
    "away_win": 0.10
  },
  "home_goals": 2,
  "away_goals": 1,
  "home_points": 3,
  "away_points": 0,
  "goal_difference": 1.2
}
```

#### 6. User Statistics
```http
GET /api/user/stats
Authorization: Required (session-based)
```

**Response** (200):
```json
{
  "total_predictions": 15,
  "accuracy": 73.3,
  "favorite_team": "Arsenal"
}
```

#### 7. Debug Input Format
```http
GET /api/debug_input
```

**Response**:
```json
{
  "features": [
    "H_goals_last3_mean", "H_shots_last3_mean", ...
  ],
  "sample_vector": [0, 0, 0, ...]
}
```

### Error Codes

| Code | Description |
|------|-------------|
| 200 | Success |
| 201 | Created (signup successful) |
| 400 | Bad Request (missing/invalid parameters) |
| 401 | Unauthorized (invalid credentials) |
| 404 | Not Found |
| 500 | Internal Server Error |

---

## Frontend Routes

### Public Routes (No Authentication Required)
- `/login.html` - User login page
- `/signup.html` - User registration page

### Protected Routes (Authentication Required)
- `/dashboard.html` - User dashboard with statistics
- `/predict.html` - Match prediction interface
- `/ai_predictor.html` - AI chatbot interface

### Navigation Flow
```
Login ──→ Dashboard ──→ Predict Match
  │                  ──→ AI Predictor
  │                  ──→ Logout → Login
  ↓
Signup → Login → Dashboard
```

---

## Database Schema

### User Model (Django Built-in)
```python
User {
  id: Integer (PK)
  username: String (unique)
  email: String (unique)
  password: String (hashed)
  first_name: String
  last_name: String
  is_active: Boolean
  date_joined: DateTime
}
```

### UserProfile Model
```python
UserProfile {
  id: Integer (PK)
  user: ForeignKey(User) (1-to-1)
  favorite_team: String
  predictions_count: Integer
  correct_predictions: Integer
  accuracy: Float (computed)
  created_at: DateTime
  updated_at: DateTime
}
```

### PredictionHistory Model
```python
PredictionHistory {
  id: Integer (PK)
  user: ForeignKey(User)
  home_team: String
  away_team: String
  predicted_outcome: String
  predicted_score: String
  confidence: Float
  actual_outcome: String (nullable)
  is_correct: Boolean (nullable)
  match_date: DateTime
  created_at: DateTime
}
```

### Database Relationships
```
User (1) ──── (1) UserProfile
 │
 └──── (Many) PredictionHistory
```

---

## Machine Learning Models

### Model Architecture

#### 1. Match Outcome Classifier
- **Algorithm**: Random Forest Classifier / Logistic Regression
- **Input Features**: 28 rolling average statistics
- **Output**: Predicted class (H, D, A)
- **Classes**:
  - `H` = Home Win
  - `D` = Draw
  - `A` = Away Win

#### 2. Goal Difference Regressor
- **Algorithm**: Random Forest Regressor / Linear Regression
- **Input Features**: Same 28 rolling averages
- **Output**: Predicted goal difference (float)

#### 3. Feature Scaler
- **Type**: StandardScaler
- **Purpose**: Normalize input features for consistent predictions

### Feature Engineering

**Input Features (28 total)**:

Rolling averages over last 3 matches for home team:
1. `H_goals_last3_mean` - Average goals scored
2. `H_goals_conceded_last3_mean` - Average goals conceded
3. `H_shots_last3_mean` - Average shots
4. `H_shots_on_target_last3_mean` - Average shots on target
5. `H_corners_last3_mean` - Average corners
6. `H_fouls_last3_mean` - Average fouls committed
7. `H_yellow_cards_last3_mean` - Average yellow cards
8. `H_red_cards_last3_mean` - Average red cards
9. `H_half_time_goals_last3_mean` - Average half-time goals
10. `H_win_streak` - Current winning streak
11. `H_draw_streak` - Current draw streak
12. `H_loss_streak` - Current loss streak
13. `H_points_last3` - Points from last 3 matches
14. `H_goals_per_match` - Season average goals per match

Same 14 features for away team with `A_` prefix.

### Model Files

Located in `scoresight_backend/artifacts/`:
- `match_outcome_classifier.pkl` - Trained classifier (~1-5 MB)
- `goal_diff_regressor.pkl` - Trained regressor (~1-5 MB)
- `feature_scaler.pkl` - Fitted scaler (~10 KB)
- `model_meta.json` - Model metadata and configuration

### Model Performance Metrics

**Typical Performance** (varies by training data):
- **Accuracy**: 50-60% (better than random ~33%)
- **Precision**: 0.55-0.65
- **Recall**: 0.50-0.60
- **F1-Score**: 0.52-0.62

### Prediction Pipeline

```python
# 1. Receive raw match statistics
raw_stats = {
  'HomeTeam': 'Arsenal',
  'AwayTeam': 'Chelsea',
  'HTHG': 1, 'HTAG': 0,
  'HS': 12, 'AS': 8,
  # ... more stats
}

# 2. Map to rolling average features
feature_vector = _build_vector(raw_stats)
# [1.2, 0.8, 12.5, 5.3, ...] (28 features)

# 3. Scale features
scaled_features = scaler.transform([feature_vector])

# 4. Predict outcome
outcome = classifier.predict(scaled_features)[0]  # 'H', 'D', or 'A'
probabilities = classifier.predict_proba(scaled_features)[0]

# 5. Predict goal difference
goal_diff = regressor.predict(scaled_features)[0]

# 6. Format response
response = {
  'outcome': 'Home Win',
  'probabilities': {
    'home_win': 0.65,
    'draw': 0.25,
    'away_win': 0.10
  },
  'goal_difference': 1.2
}
```

---

## Environment Variables

### Backend (Render)

| Variable | Description | Example | Required |
|----------|-------------|---------|----------|
| `SECRET_KEY` | Django secret key for security | `django-insecure-abc123...` | Yes |
| `DEBUG` | Enable debug mode (set to False in production) | `False` | Yes |
| `PYTHON_VERSION` | Python runtime version | `3.12.0` | Yes |
| `ALLOWED_HOSTS` | Comma-separated allowed hosts | `.onrender.com,.vercel.app` | Auto-configured |
| `DATABASE_URL` | Database connection string (if using PostgreSQL) | `postgres://...` | No (using SQLite) |

### Generating SECRET_KEY

```python
# Run in Python shell
from django.core.management.utils import get_random_secret_key
print(get_random_secret_key())
```

Or use online generator: https://djecrety.ir/

### Frontend (Vercel)

No environment variables required for static deployment. API URL is configured in `assets/script.js`.

---

## Custom Domain Setup

### Frontend Custom Domain (Vercel)

#### Step 1: Add Domain in Vercel

1. Go to Vercel Dashboard → Your Project
2. Navigate to **Settings** → **Domains**
3. Click **Add Domain**
4. Enter your domain: `scoresight.com` or `www.scoresight.com`

#### Step 2: Configure DNS Records

Add these records in your domain registrar (GoDaddy, Namecheap, Cloudflare, etc.):

**For root domain** (`scoresight.com`):
```
Type: A
Name: @
Value: 76.76.21.21
TTL: 3600
```

**For www subdomain** (`www.scoresight.com`):
```
Type: CNAME
Name: www
Value: cname.vercel-dns.com
TTL: 3600
```

#### Step 3: Verify Domain

1. Wait for DNS propagation (5-60 minutes)
2. Vercel will automatically issue SSL certificate
3. Your site will be live at `https://scoresight.com`

### Backend Custom Domain (Render)

#### Step 1: Add Custom Domain in Render

1. Go to Render Dashboard → Your Service
2. Navigate to **Settings** → **Custom Domain**
3. Click **Add Custom Domain**
4. Enter subdomain: `api.scoresight.com`

#### Step 2: Configure DNS Record

Add CNAME record in your domain registrar:

```
Type: CNAME
Name: api
Value: scoresight-backend.onrender.com
TTL: 3600
```

#### Step 3: Update Frontend API URL

Edit `frontend/assets/script.js`:

```javascript
const API_BASE = window.location.hostname === 'localhost' || window.location.hostname === '127.0.0.1'
  ? 'http://localhost:8000'
  : 'https://api.scoresight.com';  // Custom backend domain
```

Commit and push changes:
```powershell
git add .
git commit -m "Update API URL to custom domain"
git push origin main
```

#### Step 4: Update Backend CORS

Edit `scoresight_backend/settings.py`:

```python
CORS_ALLOWED_ORIGINS = [
    'http://localhost:3000',
    'http://127.0.0.1:3000',
    'https://scoresight.com',
    'https://www.scoresight.com',
]
```

Commit and push:
```powershell
git add .
git commit -m "Update CORS for custom domain"
git push origin main
```

Wait for Render auto-redeploy (~2 minutes).

---

## Monitoring & Logging

### Render Monitoring

#### View Logs

1. Go to Render Dashboard → Your Service
2. Click **Logs** tab
3. View real-time logs with filters:
   - All logs
   - Error logs
   - Custom search

#### Key Log Messages

```
✅ Your service is live 🎉
✅ Available at your primary URL https://scoresight-backend.onrender.com
✅ Loaded match outcome classifier
✅ Loaded goal difference regressor
⚠️ Free instance will spin down with inactivity (causes delays)
```

#### Metrics Dashboard

Monitor:
- **CPU Usage**: Should stay under 80%
- **Memory Usage**: Track RAM consumption
- **Request Count**: API call volume
- **Response Time**: Average latency
- **Error Rate**: 4xx and 5xx errors

### Vercel Monitoring

#### Analytics

1. Go to Vercel Dashboard → Your Project
2. Click **Analytics** tab
3. View metrics:
   - Page views
   - Top pages
   - Visitor geography
   - Device breakdown
   - Browser stats

#### Deployment Logs

1. Click **Deployments** tab
2. Select any deployment
3. View build logs and output

### Application Logging

#### Backend Logging

Django logs are visible in Render Logs tab. Add custom logging:

```python
# In views.py
import logging
logger = logging.getLogger(__name__)

class PredictV2View(APIView):
    def post(self, request):
        logger.info(f"Prediction request: {request.data}")
        # ... prediction logic
        logger.info(f"Prediction result: {response_data}")
```

#### Frontend Logging

Browser console logs are visible in DevTools (F12):

```javascript
console.log('📄 Current page:', currentPage);
console.log('🔐 Login status:', loginStatus);
console.error('❌ API Error:', error);
```

### Error Tracking

Consider integrating:
- **Sentry**: Real-time error tracking
- **LogRocket**: Session replay and monitoring
- **Google Analytics**: User behavior tracking

---

## Troubleshooting

### Common Issues and Solutions

#### 1. CORS Error: "Access blocked by CORS policy"

**Symptoms**:
```
Access to fetch at 'https://scoresight-backend.onrender.com/api/predict_v2' 
from origin 'https://your-app.vercel.app' has been blocked by CORS policy
```

**Solution**:
1. Add your Vercel URL to `CORS_ALLOWED_ORIGINS` in `settings.py`
2. Use regex pattern for all Vercel deployments:
```python
CORS_ALLOWED_ORIGIN_REGEXES = [
    r"^https://.*\.vercel\.app$",
]
```
3. Push changes and wait for Render redeploy

#### 2. 404 Not Found on Backend Root

**Symptoms**: Visiting backend URL shows 404 error

**Solution**: This is normal! API endpoints are at `/api/*`:
- Root endpoint: `/` (shows service info)
- Health: `/api/health`
- Predict: `/api/predict_v2`

#### 3. 404 Not Found on Frontend

**Symptoms**: Vercel shows "404: NOT_FOUND"

**Solution**: Ensure `vercel.json` has rewrites:
```json
{
  "rewrites": [
    { "source": "/", "destination": "/login.html" },
    { "source": "/(.*)", "destination": "/$1" }
  ]
}
```

#### 4. Model Not Loading

**Symptoms**: 
```
FileNotFoundError: [Errno 2] No such file or directory: 'artifacts/match_outcome_classifier.pkl'
```

**Solution**:
1. Verify `artifacts/` folder is in repository
2. Check file names match exactly
3. Run deployment script:
```powershell
.\setup-deployment.ps1
```

#### 5. Render Service Slow to Respond

**Symptoms**: First request takes 30-60 seconds

**Cause**: Free tier instances spin down after 15 minutes of inactivity

**Solutions**:
- **Accept delay**: Normal for free tier
- **Upgrade to paid tier**: Instances stay active 24/7
- **Use cron job**: Ping service every 10 minutes to keep alive

#### 6. Database Locked Error

**Symptoms**: `database is locked` error

**Cause**: SQLite doesn't handle concurrent writes well

**Solutions**:
- Use database connection pooling
- Upgrade to PostgreSQL for production
- Reduce concurrent write operations

#### 7. Static Files Not Loading

**Symptoms**: CSS/JS files return 404 or serve incorrectly

**Solution**:
1. Run collectstatic:
```powershell
python manage.py collectstatic --noinput
```
2. Verify `STATIC_ROOT` and `STATICFILES_STORAGE` in settings
3. Check WhiteNoise middleware is installed

#### 8. Login Redirect Loop

**Symptoms**: Login successful but redirects back to login

**Cause**: localStorage not being set or read correctly

**Solution**:
1. Check browser console for errors
2. Verify `localStorage.setItem()` calls
3. Clear browser cache and localStorage
4. Ensure HTTPS (mixed content issues)

#### 9. Predictions Always Same Value

**Symptoms**: All predictions show similar probabilities

**Cause**: Model not properly loaded or feature engineering issue

**Solution**:
1. Check Render logs for model loading confirmation
2. Verify `_build_vector()` function maps features correctly
3. Test with `/api/debug_input` endpoint
4. Retrain model with more diverse data

#### 10. Free Tier Limitations

**Render Free Tier**:
- ⚠️ Spins down after 15 min inactivity
- ⚠️ Limited to 512MB RAM
- ⚠️ Shared CPU
- ⚠️ 750 hours/month (not 24/7)

**Vercel Free Tier**:
- ✅ Unlimited bandwidth (fair use)
- ✅ 100GB bandwidth/month
- ⚠️ Limited build minutes

**Solutions**:
- Monitor usage in dashboards
- Upgrade to paid tiers for production
- Optimize code for performance

---

## Security Best Practices

### 1. Environment Variables
```python
# ✅ DO: Use environment variables
SECRET_KEY = os.environ.get('SECRET_KEY')

# ❌ DON'T: Hardcode secrets
SECRET_KEY = 'django-insecure-hardcoded-key-123'
```

### 2. Debug Mode
```python
# ✅ Production
DEBUG = False

# ❌ Never in production
DEBUG = True  # Exposes sensitive information!
```

### 3. ALLOWED_HOSTS
```python
# ✅ Specific hosts
ALLOWED_HOSTS = ['.onrender.com', '.vercel.app', 'scoresight.com']

# ❌ Too permissive
ALLOWED_HOSTS = ['*']  # Security risk!
```

### 4. CORS Configuration
```python
# ✅ Specific origins
CORS_ALLOWED_ORIGINS = ['https://scoresight.com']

# ❌ Allow all (only for development!)
CORS_ALLOW_ALL_ORIGINS = True  # Vulnerable to CSRF!
```

### 5. Password Security
- Use Django's built-in password hashing (PBKDF2)
- Require strong passwords (8+ characters)
- Never store plain-text passwords
- Implement rate limiting on login attempts

### 6. HTTPS Only
```python
# Force HTTPS in production
SECURE_SSL_REDIRECT = True
SESSION_COOKIE_SECURE = True
CSRF_COOKIE_SECURE = True
```

### 7. SQL Injection Prevention
```python
# ✅ Use Django ORM (parameterized queries)
User.objects.filter(email=email)

# ❌ Never use raw SQL with user input
cursor.execute(f"SELECT * FROM users WHERE email = '{email}'")
```

### 8. XSS Prevention
```javascript
// ✅ Escape user input
element.textContent = userInput;

// ❌ Direct HTML injection
element.innerHTML = userInput;  // XSS vulnerability!
```

### 9. CSRF Protection
- Django CSRF middleware enabled by default
- Include CSRF token in forms
- Use `@csrf_exempt` sparingly

### 10. Rate Limiting
```python
# Install: pip install django-ratelimit
from django_ratelimit.decorators import ratelimit

@ratelimit(key='ip', rate='5/m')
def login_view(request):
    # Limit to 5 login attempts per minute
    pass
```

---

## Performance Optimization

### Frontend Optimization

#### 1. Minify Assets
```javascript
// Use minified versions
<script src="bootstrap.min.js"></script>
<link href="bootstrap.min.css" rel="stylesheet">
```

#### 2. Lazy Load Images
```html
<img src="placeholder.jpg" data-src="actual-image.jpg" loading="lazy">
```

#### 3. Cache Static Files
```html
<meta http-equiv="Cache-Control" content="max-age=31536000">
```

#### 4. Compress Assets
Vercel automatically compresses files with Brotli/Gzip

#### 5. Reduce API Calls
```javascript
// ✅ Cache results
const cachedTeams = localStorage.getItem('teams');
if (!cachedTeams) {
  fetchTeams();
}

// ❌ Fetch every time
fetchTeams();
```

### Backend Optimization

#### 1. Database Indexing
```python
class UserProfile(models.Model):
    user = models.OneToOneField(User, on_delete=models.CASCADE, db_index=True)
    favorite_team = models.CharField(max_length=50, db_index=True)
```

#### 2. Query Optimization
```python
# ✅ Use select_related to reduce queries
profile = UserProfile.objects.select_related('user').get(id=1)

# ❌ Causes N+1 query problem
for profile in UserProfile.objects.all():
    print(profile.user.email)  # Separate query each time!
```

#### 3. Caching
```python
from django.core.cache import cache

def get_teams():
    teams = cache.get('teams_list')
    if not teams:
        teams = load_teams_from_db()
        cache.set('teams_list', teams, 3600)  # Cache 1 hour
    return teams
```

#### 4. Model Caching
```python
# Cache loaded models in memory
_classifier_cache = None

def get_classifier():
    global _classifier_cache
    if _classifier_cache is None:
        _classifier_cache = joblib.load('artifacts/classifier.pkl')
    return _classifier_cache
```

#### 5. Pagination
```python
from rest_framework.pagination import PageNumberPagination

class PredictionPagination(PageNumberPagination):
    page_size = 20
    
class PredictionHistoryView(APIView):
    pagination_class = PredictionPagination
```

#### 6. Async Processing
```python
# For heavy tasks, use Celery or background jobs
from celery import shared_task

@shared_task
def retrain_model():
    # Long-running task
    pass
```

### Server Configuration

#### Gunicorn Workers
```
# Procfile
web: gunicorn scoresight_backend.wsgi:application --workers 4 --threads 2
```

Calculate workers:
```
workers = (2 x CPU cores) + 1
```

#### Database Connection Pool
```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'CONN_MAX_AGE': 600,  # Persistent connections
    }
}
```

---

## Backup & Recovery

### Database Backup

#### Manual Backup (SQLite)
```powershell
# Backup database
cp scoresight_backend/db.sqlite3 backups/db_backup_2025-11-16.sqlite3

# Restore database
cp backups/db_backup_2025-11-16.sqlite3 scoresight_backend/db.sqlite3
```

#### Automated Backup Script
```powershell
# backup.ps1
$date = Get-Date -Format "yyyy-MM-dd_HH-mm"
$backupPath = "backups/db_backup_$date.sqlite3"
Copy-Item "db.sqlite3" $backupPath
Write-Host "Backup created: $backupPath"

# Keep only last 7 backups
Get-ChildItem "backups/" -Filter "db_backup_*.sqlite3" | 
    Sort-Object CreationTime -Descending | 
    Select-Object -Skip 7 | 
    Remove-Item
```

Schedule with Task Scheduler (Windows) or cron (Linux/Mac)

#### PostgreSQL Backup (Recommended for Production)
```bash
# Backup
pg_dump DATABASE_URL > backup.sql

# Restore
psql DATABASE_URL < backup.sql
```

### Code Backup

#### Git Version Control
```powershell
# Always commit and push regularly
git add .
git commit -m "Daily backup"
git push origin main
```

#### GitHub Automated Backups
- GitHub automatically backs up repositories
- Enable branch protection rules
- Use GitHub Actions for automated testing

### ML Models Backup

```powershell
# Backup artifacts folder
Compress-Archive -Path artifacts/ -DestinationPath "backups/models_$(Get-Date -Format 'yyyy-MM-dd').zip"
```

### Disaster Recovery Plan

1. **Code**: Restore from GitHub repository
2. **Database**: Restore from latest backup
3. **ML Models**: Restore from artifacts backup
4. **Environment Variables**: Document in secure location (1Password, etc.)
5. **DNS**: Keep DNS records documented

**Recovery Time Objective (RTO)**: < 1 hour  
**Recovery Point Objective (RPO)**: Last backup (daily recommended)

---

## CI/CD Pipeline

### GitHub Actions Workflow

Create `.github/workflows/deploy.yml`:

```yaml
name: Deploy to Production

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  test:
    runs-on: ubuntu-latest
    
    steps:
    - uses: actions/checkout@v3
    
    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.12'
    
    - name: Install dependencies
      run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    
    - name: Run tests
      run: |
        python manage.py test
    
    - name: Check for migrations
      run: |
        python manage.py makemigrations --check --dry-run
  
  deploy:
    needs: test
    runs-on: ubuntu-latest
    if: github.ref == 'refs/heads/main'
    
    steps:
    - name: Deploy to Render
      run: |
        echo "Render auto-deploys from GitHub"
    
    - name: Deploy to Vercel
      run: |
        echo "Vercel auto-deploys from GitHub"
```

### Automated Testing

#### Backend Tests
```python
# api/tests.py
from django.test import TestCase
from rest_framework.test import APIClient

class PredictionAPITest(TestCase):
    def setUp(self):
        self.client = APIClient()
    
    def test_health_endpoint(self):
        response = self.client.get('/api/health')
        self.assertEqual(response.status_code, 200)
        self.assertEqual(response.json()['status'], 'ok')
    
    def test_prediction_endpoint(self):
        data = {
            'home_team': 'Arsenal',
            'away_team': 'Chelsea',
            'HTHG': 1, 'HTAG': 0,
            'HS': 12, 'AS': 8,
            # ... other fields
        }
        response = self.client.post('/api/predict_v2', data, format='json')
        self.assertEqual(response.status_code, 200)
        self.assertIn('outcome', response.json())
```

Run tests:
```powershell
python manage.py test
```

#### Frontend Tests (Optional)
Use Jest or similar for JavaScript testing:

```javascript
// tests/script.test.js
test('API URL configuration', () => {
  expect(API_BASE).toBeDefined();
  expect(API_BASE).toMatch(/^https?:\/\//);
});
```

---

## Contributing

### Development Workflow

1. **Fork the repository**
2. **Create feature branch**
   ```powershell
   git checkout -b feature/amazing-feature
   ```
3. **Make changes and test**
4. **Commit with descriptive message**
   ```powershell
   git commit -m "Add amazing feature that does XYZ"
   ```
5. **Push to your fork**
   ```powershell
   git push origin feature/amazing-feature
   ```
6. **Open Pull Request**

### Code Style Guidelines

#### Python (Backend)
- Follow PEP 8 style guide
- Use 4 spaces for indentation
- Maximum line length: 120 characters
- Use docstrings for functions/classes
- Type hints recommended

```python
def predict_match(home_team: str, away_team: str) -> dict:
    """
    Predict match outcome using ML models.
    
    Args:
        home_team: Name of home team
        away_team: Name of away team
    
    Returns:
        Dictionary containing prediction results
    """
    pass
```

#### JavaScript (Frontend)
- Use camelCase for variables
- Use const/let (not var)
- Use template literals
- Add JSDoc comments for functions

```javascript
/**
 * Predict match outcome via API
 * @param {Object} matchData - Match statistics
 * @returns {Promise<Object>} Prediction results
 */
async function predictMatch(matchData) {
  // Implementation
}
```

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types**:
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting changes
- `refactor`: Code restructuring
- `test`: Adding tests
- `chore`: Maintenance

**Example**:
```
feat(prediction): Add goal difference prediction

- Implemented regressor model
- Updated API response format
- Added tests for new feature

Closes #123
```

---

## License

This project is licensed under the MIT License.

```
MIT License

Copyright (c) 2025 Amit Kumar

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```

---

## Support & Contact

### Get Help

- **Documentation**: This file
- **Issues**: Open issue on GitHub
- **Email**: your-email@example.com
- **Website**: https://scoresight.com

### Useful Links

- **Frontend Repository**: https://github.com/ankit-kumarz/ScoreSight_frontend
- **Backend Repository**: https://github.com/ankit-kumarz/ScoreSight_backend
- **Live Demo**: https://score-sight-frontend.vercel.app
- **API Docs**: https://scoresight-backend.onrender.com/

---

## Changelog

### Version 1.0.0 (November 16, 2025)
- ✅ Initial production release
- ✅ Full-stack application deployed
- ✅ ML-powered match predictions
- ✅ User authentication system
- ✅ AI chatbot integration
- ✅ Responsive design for all devices
- ✅ Production-ready backend API
- ✅ Comprehensive documentation

---

## Acknowledgments

- **Django**: Web framework for Python
- **scikit-learn**: Machine learning library
- **Bootstrap**: Frontend UI framework
- **Vercel**: Frontend hosting platform
- **Render**: Backend hosting platform
- **GitHub**: Version control and CI/CD

---

**Built with ❤️ by Amit Kumar**

*Last Updated: November 16, 2025*
