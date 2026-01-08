# 🧠 MindMorph - AI-Powered Personality Analysis Platform

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![React](https://img.shields.io/badge/React-18.0+-61DAFB.svg)
![Flask](https://img.shields.io/badge/Flask-3.0+-000000.svg)
![MongoDB](https://img.shields.io/badge/MongoDB-Latest-47A248.svg)
![ML Accuracy](https://img.shields.io/badge/ML%20Accuracy-80.36%25-success.svg)

A comprehensive web application that predicts MBTI personality types using advanced machine learning techniques. Analyzes personality through questionnaires, text analysis, and social media profiles.

---

## 🎯 Key Features

### Three Analysis Modules

#### 1. Scenario-Based Questionnaire
- 20 carefully crafted real-life scenarios
- ML-enhanced scoring with Random Forest classifier
- Interactive UI with progress tracking
- **Accuracy: 75%+**

#### 2. Text Analysis
- Analyze any written text (journals, essays, blogs)
- Minimum 100 characters, 500+ recommended
- BERT + CountVectorizer + Linguistic feature extraction
- **Accuracy: 80.36%** ⭐

#### 3. Twitter/Social Media Analysis
- Analyze personality from tweets
- Hybrid system: Real Twitter API + Professional Mock API
- Stores analyzed tweets in database
- Same 80.36% ML model
- **Accuracy: 80.36%**

### Additional Features
- 📊 **History Tracking** - View all past analyses
- 📄 **PDF Export** - Download detailed reports
- 🔐 **Authentication** - Secure JWT-based login
- 🎨 **Modern UI** - Beautiful gradient design
- 🔄 **Real-time Analysis** - Instant results
- 💾 **Data Persistence** - MongoDB storage
- 🎭 **16 MBTI Types** - Complete personality profiles

---

## 🧠 Machine Learning Architecture

### Model Overview

Our system uses **4 binary ensemble classifiers** instead of a single 16-class classifier, significantly improving accuracy.

### Technical Details

**Feature Engineering:**
1. **BERT Embeddings (768 dimensions)**
   - Model: `all-MiniLM-L6-v2` (sentence-transformers)
   - Captures semantic meaning and context
   - Pre-trained on large text corpus

2. **CountVectorizer (5,000 dimensions)**
   - Unigrams and bigrams (n-gram range: 1-2)
   - Frequency-based word importance
   - Better than TF-IDF for personality text

3. **Linguistic Features (20 dimensions)**
   - Average word/sentence length
   - Punctuation patterns (!, ?, ..., ,)
   - Personal pronoun usage (I, we, you)
   - Emotional word ratios
   - Abstract vs concrete language

**Classification:**
- 4 separate binary classifiers (one per dimension)
- Each uses soft voting ensemble
- Algorithms: Logistic Regression + XGBoost + Random Forest
- Training: 5 epochs with early stopping

### Training Data

**Dataset Specifications:**
- **Source:** MBTI Personality Types Dataset (Kaggle)
- **Total Profiles:** 2,574 individuals
- **Data Type:** Aggregated Twitter posts per person
- **Average Text Length:** 7,989 characters per profile
- **Distribution:** Balanced across 16 MBTI types (~150-200 per type)

**Data Preprocessing:**
1. Collected 8,675 user profiles from Kaggle
2. Aggregated multiple posts per person (20-50 posts each)
3. Filtered short posts (<100 characters)
4. Balanced classes via undersampling
5. Split: 70% train, 15% validation, 15% test

**Training Environment:**
- Platform: Google Colab (Free GPU - T4)
- Training Time: 30-45 minutes
- Framework: scikit-learn, XGBoost, Transformers

### Accuracy Results

| Dimension | Accuracy | Precision | Recall | F1-Score |
|-----------|----------|-----------|--------|----------|
| I/E | **80.88%** | 0.81 | 0.81 | 0.81 |
| N/S | **83.98%** | 0.84 | 0.84 | 0.84 |
| T/F | **81.91%** | 0.82 | 0.82 | 0.82 |
| J/P | **74.68%** | 0.75 | 0.75 | 0.75 |
| **Overall** | **80.36%** | 0.81 | 0.80 | 0.80 |

**Performance Comparison:**
- Previous systems: 55-65% accuracy (16-class)
- Our approach: 80.36% accuracy (4 binary classifiers)
- Improvement: +15-25 percentage points



## 🛠️ Tech Stack

### Frontend
- **React** 18.2.0 - UI framework
- **React Router** v6 - Navigation
- **Axios** - HTTP client
- **Tailwind CSS** - Styling
- **jsPDF** - PDF generation
- **React Hot Toast** - Notifications

### Backend
- **Flask** 3.0 - Web framework
- **Python** 3.10+ - Programming language
- **Flask-JWT-Extended** - Authentication
- **Flask-CORS** - Cross-origin support
- **PyMongo** - MongoDB driver
- **Werkzeug** - Security utilities

### Machine Learning
- **scikit-learn** 1.3+ - ML algorithms
- **XGBoost** 2.0+ - Gradient boosting
- **Transformers** 4.30+ - BERT models
- **sentence-transformers** 2.2+ - Embeddings
- **pandas** - Data manipulation
- **numpy** - Numerical computing

### Database
- **MongoDB** 6.0+ - NoSQL database
- Collections: users, questionnaire_predictions, text_predictions, twitter_predictions

### APIs
- **Twitter API v2** - Real tweet fetching
- **Mock API** (Built-in) - Demo profiles

---

## 📦 Installation & Setup

### 🔧 Prerequisites

Ensure the following software is installed on your system:

* Python 3.10 or higher
* Node.js 16 or higher
* Git

Verify installations:
```bash
python --version
node --version
git --version
```

---

## 📂 Step 1: Clone the Repository
```bash
git clone https://github.com/yourusername/mindmorph.git
cd mindmorph
```

---

## ☁️ Step 2: MongoDB Atlas Setup

### 2.1 Create MongoDB Atlas Account

1. Visit: https://www.mongodb.com/cloud/atlas/register
2. Sign up for a free account
3. Choose **Shared (Free Tier)**
4. Select **AWS** as the cloud provider
5. Choose the nearest region
6. Create the cluster (takes 3–5 minutes)

### 2.2 Create Database User

1. Open **MongoDB Atlas Dashboard**
2. Navigate to **Database Access**
3. Click **Add New Database User**
4. Choose **Password authentication**
5. Set the following:
   * Username: `mindmorph_user`
   * Password: Auto-generate and save securely
6. Database privileges: **Read and write to any database**
7. Click **Add User**

### 2.3 Configure Network Access

1. Go to **Network Access**
2. Click **Add IP Address**
3. Select **Allow access from anywhere (0.0.0.0/0)**
4. Confirm

### 2.4 Get MongoDB Connection String

1. Go to **Database**
2. Click **Connect** on your cluster
3. Choose **Connect your application**
4. Copy the connection string:
```text
mongodb+srv://mindmorph_user:<password>@cluster0.xxxxx.mongodb.net/
```

Replace `<password>` with your database user password.

---

## 🧠 Step 3: Backend Setup (Flask)
```bash
cd backend
```

### Create Virtual Environment
```bash
python -m venv venv
```

**Activate it:**

**Windows:**
```bash
venv\Scripts\activate
```

**Mac/Linux:**
```bash
source venv/bin/activate
```

### Install Dependencies
```bash
pip install -r requirements.txt
```

### Create Environment Variables

Create a file named `.env` inside the `backend` folder:
```env
SECRET_KEY=dev-secret-key-change-in-production
JWT_SECRET_KEY=jwt-secret-key-change-in-production

MONGO_URI=mongodb+srv://mindmorph_user:<password>@cluster0.xxxxx.mongodb.net/mindmorph?retryWrites=true&w=majority

# Twitter API 
TWITTER_API_KEY=your_api_key
TWITTER_API_SECRET=your_api_secret
TWITTER_BEARER_TOKEN=your_bearer_token

# Toggle Twitter API
USE_REAL_TWITTER_API=true
```

⚠️ **Do not commit the `.env` file to GitHub.**

### Run Backend Server
```bash
python run.py
```

Backend runs at:
```
http://localhost:5000
```

---

## 🎨 Step 4: Frontend Setup (React)

Open a new terminal window:
```bash
cd frontend
npm install
npm start
```

Frontend runs at:
```
http://localhost:3000
```

---

## ✅ Step 5: Verify Installation

1. Open `http://localhost:3000` in your browser
2. Create a new account (Sign Up)
3. Log in with your credentials
4. Confirm that all application modules are accessible

---

📁 Project Structure
```
MindMorph/
├── backend/
│   ├── app/
│   │   ├── __init__.py
│   │   ├── ml_models/
│   │   │   ├── text_classifier.py
│   │   │   ├── questionnaire/
│   │   │   │   └── random_forest_model.pkl
│   │   │   └── text/
│   │   │       ├── IE_aggregated_ensemble.pkl
│   │   │       ├── IE_aggregated_vectorizer.pkl
│   │   │       ├── NS_aggregated_ensemble.pkl
│   │   │       ├── NS_aggregated_vectorizer.pkl
│   │   │       ├── TF_aggregated_ensemble.pkl
│   │   │       ├── TF_aggregated_vectorizer.pkl
│   │   │       ├── JP_aggregated_ensemble.pkl
│   │   │       └── JP_aggregated_vectorizer.pkl
│   │   ├── routes/
│   │   │   ├── auth.py
│   │   │   ├── questionnaire.py
│   │   │   ├── text.py
│   │   │   ├── twitter.py
│   │   │   └── twitter_mock_api.py
│   │   ├── services/
│   │   │   ├── mbti_service.py
│   │   │   ├── twitter_hybrid_service.py
│   │   │   ├── twitter_real_api_client.py
│   │   │   └── twitter_mock_api_client.py
│   │   └── models/
│   │       └── user.py
│   ├── data/
│   │   ├── mbti_insights.json
│   │   ├── mock_twitter_data.json
│   │   └── training/
│   │       ├── aggregated_binary/
│   │       └── analysis_plots/
│   ├── .env
│   ├── requirements.txt
│   └── run.py
│
├── frontend/
│   ├── public/
│   ├── src/
│   │   ├── components/
│   │   │   ├── auth/
│   │   │   ├── questionnaire/
│   │   │   └── shared/
│   │   ├── pages/
│   │   │   ├── Home.jsx
│   │   │   ├── questionnaire/
│   │   │   │   ├── Test.jsx
│   │   │   │   ├── Result.jsx
│   │   │   │   └── History.jsx
│   │   │   ├── text/
│   │   │   │   ├── Analyze.jsx
│   │   │   │   ├── Result.jsx
│   │   │   │   └── History.jsx
│   │   │   └── twitter/
│   │   │       ├── Analyze.jsx
│   │   │       ├── Result.jsx
│   │   │       └── History.jsx
│   │   ├── services/
│   │   │   ├── questionnaireService.js
│   │   │   ├── textService.js
│   │   │   └── twitterService.js
│   │   ├── utils/
│   │   │   └── pdfGenerator.js
│   │   ├── contexts/
│   │   │   └── AuthContext.jsx
│   │   └── App.jsx
│   └── package.json
│
└── README.md
```
---

## Learning Outcomes:

- Full-stack web development
- Machine learning deployment
- RESTful API design
- Database optimization
- UI/UX design


## 📚 References
#### Datasets

- MBTI Dataset: Kaggle - MBTI Personality Types 500
- 8,675 users with aggregated posts

#### Libraries

- React: https://react.dev/
- Flask: https://flask.palletsprojects.com/
- scikit-learn: https://scikit-learn.org/
- Transformers: https://huggingface.co/

#### MBTI Resources

- Myers & Briggs Foundation: https://www.myersbriggs.org/
- 16Personalities: https://www.16personalities.com/


## 🤝 Contributing
This is an academic project. Feedback welcome!

## Contact:
Email: [aishwarya.anand1125@gmail.com]



## 📝 License
Developed for academic purposes. Not licensed for commercial use.
