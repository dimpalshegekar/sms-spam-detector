# 📱 SMS Spam Detector

A machine learning web application that classifies SMS messages as **spam** or **ham (safe)** in real time using Naive Bayes + TF-IDF, wrapped in a Flask Web UI.

![Python](https://img.shields.io/badge/Python-3.10+-blue?style=flat-square&logo=python)
![Flask](https://img.shields.io/badge/Flask-3.x-black?style=flat-square&logo=flask)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.7+-orange?style=flat-square&logo=scikit-learn)
![License](https://img.shields.io/badge/License-MIT-green?style=flat-square)
![Accuracy](https://img.shields.io/badge/Accuracy-98.4%25-brightgreen?style=flat-square)

---

## 🖥️ Web UI

A dark-themed interactive web interface where you can type any SMS and instantly see:
- Spam or Ham verdict with confidence score
- Animated probability bars
- Feature breakdown cards
- Session history panel

---

## ✨ Features

- 🔍 **Real-time detection** — classify any SMS message instantly
- 📊 **Probability bars** — visual spam vs ham confidence scores
- 🧩 **Feature breakdown** — length, uppercase ratio, phone numbers, URLs
- 📜 **Session history** — last 10 messages, click any to re-analyze
- 📈 **Live counter** — total checked, spam detected, ham safe
- 🌐 **REST API** — /predict and /batch endpoints
- 💡 **Example chips** — 4 spam + 4 ham quick-test buttons
- 🤖 **3 models compared** — Naive Bayes, Logistic Regression, Linear SVM

---

## 📊 Model Performance

| Metric | Score |
|--------|-------|
| Accuracy | 98.4% |
| Precision | 99.1% |
| Recall | 97.3% |
| F1 Score | 98.2% |
| AUC-ROC | 0.9987 |

> Trained on 5,574 SMS messages — 747 spam (13.4%) and 4,827 ham (86.6%)

---

## 🧠 How It Works
```
Raw SMS
   ↓
Text Cleaning
(lowercase → remove URLs → tokenize phone numbers → strip stopwords → stem)
   ↓
TF-IDF Vectorization
(unigrams + bigrams, 8,000 features, sublinear TF scaling)
   ↓
Multinomial Naive Bayes
(Laplace smoothing α=1)
   ↓
Spam / Ham + Probability Score
```

---

## 🗂️ Project Structure
```
sms-spam-detector/
│
├── app.py                  ← Flask server + REST API
├── spam_model.pkl          ← Trained Naive Bayes pipeline
├── requirements.txt        ← All dependencies
├── LICENSE                 ← MIT License
├── README.md               ← You are here
│
└── templates/
    └── index.html          ← Full Web UI (dark theme)
```

---

## 🚀 Run Locally

**1. Clone the repo**
```bash
git clone https://github.com/dimpalshegekar/sms-spam-detector.git
cd sms-spam-detector
```

**2. Create virtual environment**
```bash
# Windows
python -m venv venv
venv\Scripts\activate

# macOS / Linux
python3 -m venv venv
source venv/bin/activate
```

**3. Install dependencies**
```bash
pip install -r requirements.txt
```

**4. Run the app**
```bash
python app.py
```

**5. Open in browser**
```
http://127.0.0.1:5000
```

---

## 🌐 REST API Endpoints

### Health Check
```http
GET /health
```
**Response:**
```json
{
  "status": "ok",
  "model": "Naive Bayes + TF-IDF"
}
```

---

### Single Message Prediction
```http
POST /predict
Content-Type: application/json
```
**Request:**
```json
{
  "message": "WIN a FREE prize! Call 09061701461 NOW!"
}
```
**Response:**
```json
{
  "label": "spam",
  "spam_probability": 0.9999,
  "ham_probability": 0.0001,
  "confidence": "99.9%",
  "message": "WIN a FREE prize! Call 09061701461 NOW!"
}
```

---

### Batch Prediction
```http
POST /batch
Content-Type: application/json
```
**Request:**
```json
{
  "messages": [
    "Free prize call now!",
    "Hey are you coming tonight?",
    "URGENT you won 2000 pounds!"
  ]
}
```
**Response:**
```json
{
  "total": 3,
  "results": [
    { "label": "spam", "spam_probability": 0.9998, "message": "Free prize call now!" },
    { "label": "ham",  "spam_probability": 0.0001, "message": "Hey are you coming tonight?" },
    { "label": "spam", "spam_probability": 0.9995, "message": "URGENT you won 2000 pounds!" }
  ]
}
```

---

## 🛠️ Tech Stack

| Technology | Purpose |
|------------|---------|
| Python 3.10+ | Core programming language |
| scikit-learn | TF-IDF vectorizer + Naive Bayes model |
| pandas | Data loading and manipulation |
| numpy | Numerical computations |
| matplotlib + seaborn | EDA and evaluation charts |
| Flask | Web server and REST API |
| HTML + CSS + JavaScript | Frontend Web UI |

---

## 📈 Training Pipeline

If you want to retrain the model from scratch:
```bash
python step1_dataset.py      # Generate 5,574 SMS messages
python step2_preprocess.py   # Clean text and engineer features
python step3_eda.py          # Generate EDA plots
python step4_train.py        # Train and compare 3 models
python step5_evaluate.py     # Confusion matrix, ROC curve
python step6_predict.py      # Test predictions on new messages
```

---

## 📉 EDA Insights

| Feature | Spam avg | Ham avg |
|---------|----------|---------|
| Message length | 84 chars | 73 chars |
| Uppercase ratio | 17.5% | 3.5% |
| Has phone number | 85.7% | 0.0% |
| Has exclamation | 72.7% | 39.6% |
| Has URL | 5.4% | 0.0% |

---

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Open an issue for bugs or feature requests
- Fork the repo and submit a pull request
- Star the repo if you found it helpful ⭐

---

## 👩‍💻 Author

**Dimpal Shegekar**
- GitHub: [@dimpalshegekar](https://github.com/dimpalshegekar)
- LinkedIn: [Dimpal Shegekar](https://linkedin.com/in/dimpalshegekar)

---

## 📄 License

This project is licensed under the **MIT License** — see the [LICENSE](LICENSE) file for details.

---

## ⭐ If you found this helpful, give it a star!

```
git clone https://github.com/dimpalshegekar/sms-spam-detector.git
```
