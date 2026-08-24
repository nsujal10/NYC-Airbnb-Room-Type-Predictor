# 🏙️ NYC Airbnb Room Type Predictor

A machine learning-powered web application that predicts whether an Airbnb listing is an **entire home/apt**, **private room**, or **shared room** based on listing characteristics. Features a beautiful, interactive UI with real-time predictions.

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Project Structure](#project-structure)
- [Tech Stack](#tech-stack)
- [Installation & Setup](#installation--setup)
- [How to Run](#how-to-run)
- [API Documentation](#api-documentation)
- [Using the Web Interface](#using-the-web-interface)
- [Model Details](#model-details)
- [Deployment](#deployment)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Overview

This project combines **machine learning** and **modern web design** to create an intelligent room-type classifier for NYC Airbnb listings. The backend uses a scikit-learn model served via FastAPI, while the frontend provides an engaging, animated interface.

### What It Does
- Takes listing details (price, location, reviews, availability, etc.)
- Runs them through a trained ML model
- Returns the predicted room type with confidence probabilities
- Visualizes results with animated "buildings" showing prediction confidence

---

## ✨ Features

### 🤖 Machine Learning
- **Pre-trained classification model** optimized for NYC Airbnb data
- Supports three room types: Entire home/apt, Private room, Shared room
- Returns probability scores for each class
- Fast inference powered by scikit-learn pipelines

### 🎨 User Interface
- **Elegant dark theme** with NYC skyline aesthetic
- **Real-time form validation** with helpful error messages
- **Interactive visualizations**: Building animations show prediction confidence
- **Example data loader**: Try predictions with realistic sample listings
- **Live API status indicator**: Shows connection health to backend
- **Fully responsive**: Works on desktop, tablet, and mobile devices
- **Accessibility features**: WCAG compliant, respects motion preferences

### 🔄 Backend
- **FastAPI server** for high performance
- **CORS enabled** for cross-origin requests
- **Input validation** using Pydantic models
- **Model serialization** with joblib for fast loading

---

## 📁 Project Structure

```
NYC-Airbnb-Room-Type-Predictor/
├── main.py                          # FastAPI backend server
├── index.html                       # Web interface (HTML)
├── style.css                        # Styling (dark theme, animations)
├── script.js                        # Frontend logic & API calls
├── requirements.txt                 # Python dependencies
├── runtime.txt                      # Python version specification
├── README.md                        # Project documentation
├── nyc_airbnb_room_type_classification.ipynb  # Model training notebook
├── Model_Pipeline.pkl               # Trained model (binary file)
└── __pycache__/                     # Python cache files
```

---

## 🛠️ Tech Stack

### Backend
- **FastAPI** (0.115.6) - Modern async web framework
- **Uvicorn** (0.34.0) - ASGI server
- **Pydantic** (2.10.4) - Data validation
- **pandas** (2.2.3) - Data manipulation
- **scikit-learn** (1.6.1) - Machine learning
- **joblib** (1.4.2) - Model persistence

### Frontend
- **HTML5** - Semantic markup
- **CSS3** - Modern styling with CSS Grid, custom properties, animations
- **Vanilla JavaScript** - No frameworks, lightweight and fast

### Runtime
- **Python 3.14.3** - Latest stable Python

---

## 📦 Installation & Setup

### Prerequisites
- Python 3.14.3 installed on your system
- Git (optional, for cloning)
- A modern web browser (Chrome, Firefox, Safari, Edge)

### Step 1: Clone or Download the Project

```bash
# Using Git
git clone https://github.com/yourusername/NYC-Airbnb-Room-Type-Predictor.git
cd NYC-Airbnb-Room-Type-Predictor

# Or download the ZIP and extract it
```

### Step 2: Create a Virtual Environment (Recommended)

```bash
# On Windows
python -m venv venv
venv\Scripts\activate

# On macOS/Linux
python3 -m venv venv
source venv/bin/activate
```

### Step 3: Install Dependencies

```bash
pip install -r requirements.txt
```

This installs:
- FastAPI web framework
- Uvicorn ASGI server
- Pydantic for validation
- pandas for data processing
- scikit-learn for ML inference
- joblib for model loading

### Step 4: Verify Installation

```bash
pip list
```

You should see all packages listed above.

---

## 🚀 How to Run

### Running the Backend Server

```bash
# From the project directory
uvicorn main:app --reload

# Or with custom port
uvicorn main:app --reload --port 8000
```

Expected output:
```
INFO:     Uvicorn running on http://127.0.0.1:8000
INFO:     Application startup complete
```

### Running the Frontend

**Option 1: Local Python Server** (Recommended for local testing)
```bash
# Open a new terminal in the project directory
python -m http.server 3000
```

Then open: `http://localhost:3000`

**Option 2: VS Code Live Server**
- Install "Live Server" extension in VS Code
- Right-click `index.html` → "Open with Live Server"

**Option 3: Direct File Opening**
Simply double-click `index.html` to open in your browser (limited CORS support).

### Accessing the Application

Once both backend and frontend are running:
- **Frontend**: `http://localhost:3000` (or the configured port)
- **API Health Check**: `http://localhost:8000/`
- **Swagger Docs**: `http://localhost:8000/docs`
- **ReDoc Docs**: `http://localhost:8000/redoc`

---

## 📡 API Documentation

### Health Check Endpoint

```http
GET /
```

**Response:**
```json
"Hello Guyss"
```

### Prediction Endpoint

```http
POST /predict
Content-Type: application/json
```

**Request Body:**
```json
{
  "latitude": 40.7128,
  "longitude": -74.0060,
  "price": 120,
  "minimum_nights": 2,
  "number_of_reviews": 84,
  "reviews_per_month": 2.3,
  "calculated_host_listings_count": 1,
  "availability_365": 210,
  "neighbourhood_group": "Manhattan",
  "neighbourhood": "Midtown"
}
```

**Response:**
```json
{
  "Predicted_room_type": "Entire home/apt",
  "Probability": [0.92, 0.07, 0.01]
}
```

### Input Validation

All fields are validated:

| Field | Type | Constraints | Example |
|-------|------|-------------|---------|
| `latitude` | float | -90 to 90 | 40.7128 |
| `longitude` | float | -180 to 180 | -74.0060 |
| `price` | float | > 0 | 120 |
| `minimum_nights` | int | 1 to 365 | 2 |
| `number_of_reviews` | int | ≥ 0 | 84 |
| `reviews_per_month` | float | ≥ 0 | 2.3 |
| `calculated_host_listings_count` | int | ≥ 0 | 1 |
| `availability_365` | int | 0 to 365 | 210 |
| `neighbourhood_group` | string | Non-empty | "Manhattan" |
| `neighbourhood` | string | Non-empty | "Midtown" |

---

## 🎮 Using the Web Interface

### Step-by-Step Usage

1. **Enter Location Details**
   - Latitude & Longitude (use GPS or maps)
   - Select Borough (Manhattan, Brooklyn, Queens, Bronx, Staten Island)
   - Enter Neighbourhood name

2. **Input Pricing & Availability**
   - Price per night (USD)
   - Minimum nights required
   - Days available per year (use the slider)

3. **Add Review Information**
   - Total number of reviews
   - Reviews per month (average)
   - Number of listings by this host

4. **Make Prediction**
   - Click "Predict room type" button
   - Wait for the model to process
   - View results instantly!

### Example Data

Click "Try an example" to load realistic sample listings:

**Example 1: Manhattan Midtown Luxury**
- High price, frequent reviews, low availability
- Expected: Entire home/apt

**Example 2: Brooklyn Budget**
- Lower price, moderate reviews, high availability
- Expected: Private room

**Example 3: Queens Economy**
- Low price, few reviews, very low availability
- Expected: Shared room

---

## 🧠 Model Details

### How the Model Works

The ML pipeline:
1. **Data Input**: 10 features from listing details
2. **Preprocessing**: Feature scaling, encoding
3. **Classification**: Trained classifier predicts room type
4. **Probability**: Returns confidence for each class

### Room Type Classes

- **Entire home/apt**: Full property (apartment, house, etc.)
- **Private room**: Single room in shared property
- **Shared room**: Shared dormitory or common space

### Training Data

- Trained on NYC Airbnb listing dataset
- Features: Location, pricing, reviews, host info
- Target: Room type classification
- See `nyc_airbnb_room_type_classification.ipynb` for training details

### Model Performance

The model achieves high accuracy on the test set by:
- Leveraging location features (latitude, longitude, neighbourhood)
- Using pricing as a strong indicator
- Analyzing review patterns and host behavior
- Considering availability and minimum stay requirements

---

## 🌐 Deployment

### Deploy to Render (Recommended)

1. **Push code to GitHub**
   ```bash
   git init
   git add .
   git commit -m "Initial commit"
   git push origin main
   ```

2. **Create Render account** at https://render.com

3. **Create Web Service**
   - Connect GitHub repository
   - Set build command: `pip install -r requirements.txt`
   - Set start command: `uvicorn main:app --host 0.0.0.0`
   - Verify `runtime.txt` contains: `python-3.14.3`

4. **Update API_BASE_URL in script.js**
   ```javascript
   const API_BASE_URL = "https://your-render-app.onrender.com";
   ```

5. **Deploy frontend** to:
   - Vercel (Recommended)
   - Netlify
   - GitHub Pages

### Deploy to Heroku

```bash
# Login to Heroku
heroku login

# Create app
heroku create your-app-name

# Deploy
git push heroku main
```

---

## 🐛 Troubleshooting

### Issue: "API unreachable" Error

**Solution:**
- Ensure FastAPI server is running: `uvicorn main:app --reload`
- Check that `API_BASE_URL` in `script.js` matches your server URL
- Verify CORS is enabled (it is in `main.py`)
- Check browser console (F12) for detailed error messages

### Issue: "Model file not found" Error

**Solution:**
- Ensure `Model_Pipeline.pkl` is in the same directory as `main.py`
- If missing, train the model using `nyc_airbnb_room_type_classification.ipynb`

### Issue: Port Already in Use

**Solution:**
```bash
# Use a different port
uvicorn main:app --reload --port 8001
```

### Issue: Module Import Errors

**Solution:**
```bash
# Reinstall dependencies
pip install --upgrade -r requirements.txt

# Or reinstall individual package
pip install --upgrade fastapi uvicorn
```

### Issue: Python Version Mismatch

**Solution:**
- Install Python 3.14.3 or compatible version
- Verify: `python --version`
- Update `runtime.txt` with your Python version format: `python-X.Y.Z`

---

## 📊 Understanding the Visualization

### Building Animation

The results panel shows three buildings:
- **Height** = Model confidence
- **Lit Windows** = Probability percentage
- **Glow** = Predicted class (highlighted in amber)

### Probability Bar Chart

Shows prediction confidence for each room type:
- Sorted by probability (highest first)
- Top prediction highlighted in amber
- Smooth animation reveals confidence

---

## 🔐 Security

- ✅ **Input Validation**: Pydantic ensures safe data
- ✅ **CORS Enabled**: Controls API access
- ✅ **No Sensitive Data**: Model handles public listings only
- ⚠️ **Note**: In production, add authentication if needed

---

## 📚 Learning Resources

- [FastAPI Documentation](https://fastapi.tiangolo.com/)
- [scikit-learn Classification](https://scikit-learn.org/stable/modules/classification.html)
- [Pydantic Validation](https://docs.pydantic.dev/)
- [MDN Web Docs](https://developer.mozilla.org/)

<img width="1566" height="1273" alt="image" src="https://github.com/user-attachments/assets/cc712fca-289b-4acd-b01b-98507154d903" />

---

