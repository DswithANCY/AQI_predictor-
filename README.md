# 🌍 Air Quality Index (AQI) Prediction

## 📌 Project Overview
Air pollution is a critical environmental issue, and predicting air quality is essential for public health and policymaking.
This project leverages **Machine Learning (ML) techniques** to forecast the **Air Quality Index (AQI)** based on key environmental pollutants.
Three regression models are implemented and compared — **Linear Regression, Random Forest, and XGBoost** — with **XGBoost** selected as the final model and tuned further via hyperparameter search.

---

## 📂 Project Resources
🔹 **Dataset (CSV File)**: `city_day.csv` (place in the project root before running)
🔹 **Dataset (Kaggle Link)**: [View on Kaggle](https://www.kaggle.com/code/anjusunilkumar/air-quality-index-prediction?select=city_day.csv)
🔹 **Project Code (.ipynb)**: `main.ipynb`
🔹 **Saved Models**: `aqi_predictor_best.pkl`, `optimized_xgb_model.pkl`
🔹 **Predictions Output**: `aqi_predictions.csv`

---

## 📊 Dataset Overview
The dataset contains daily city-level air quality records, including:
- **Pollutants**: PM2.5, PM10, NO₂, SO₂, CO, O₃, Benzene, etc.
- **Date & City**: identifying the location and time of recording.
- **AQI (Target Variable)**: measures pollution severity, with an associated category bucket (Good, Moderate, Poor, etc.).

---

## 🛠 Data Preprocessing
✔️ **Handling Missing Values**
- Removed rows with missing `AQI` values (the prediction target).
- Imputed missing pollutant values using **mean imputation**.

✔️ **Feature Selection**
- Dropped `City`, `Date` (non-numeric) and `AQI_Bucket` (redundant with `AQI`).
- Analyzed feature correlation with `AQI` using a heatmap to identify the most influential pollutants.

✔️ **Feature Scaling**
- Used **StandardScaler** to standardize numerical features (zero mean, unit variance), fit on the training split only.

✔️ **Train/Test Split**
- 80/20 split with `random_state=42` for reproducibility.

---

## 🤖 Models Used

### 1️⃣ Linear Regression
🔹 Simple, interpretable baseline; struggles with non-linear pollutant–AQI relationships.

### 2️⃣ Random Forest Regressor
🔹 Ensemble of decision trees; captures non-linearity better than linear regression.

### 3️⃣ XGBoost Regressor (🏆 Selected Model)
✅ Gradient boosting typically outperforms Random Forest on tabular data like this.
✅ Captures complex pollutant interactions effectively.
✅ Selected as the model to carry forward into hyperparameter tuning.

---

## 📈 Model Evaluation
Each model is evaluated with:

📌 **MAE (Mean Absolute Error)** – lower is better
📌 **RMSE (Root Mean Squared Error)** – penalizes large errors more heavily
📌 **R² Score** – variance in AQI explained by the model

Results are printed per model when the notebook runs, and plotted as a bar chart comparing all three side by side.

---

## 🔧 Hyperparameter Tuning
`GridSearchCV` (5-fold CV, scored on R²) was used to tune XGBoost over:
- `n_estimators`: [50, 100, 200]
- `learning_rate`: [0.01, 0.1, 0.2]
- `max_depth`: [3, 5, 7]

✅ **Best configuration found:**
`learning_rate = 0.2, max_depth = 5, n_estimators = 100`

The final tuned model is retrained on these parameters and saved with `joblib`.

---

## 📌 Results & Predictions
- The tuned **XGBoost Regressor** is used to predict AQI on held-out test samples.
- A line plot of **Actual vs. Predicted AQI** is generated to visually check prediction accuracy.
- Sample predictions are exported to `aqi_predictions.csv`.

---

## 📁 Output Files
| File | Description |
|---|---|
| `aqi_predictor_best.pkl` | Serialized baseline XGBoost model |
| `optimized_xgb_model.pkl` | Serialized XGBoost model after hyperparameter tuning |
| `aqi_predictions.csv` | Sample AQI predictions on held-out test data |

---

## ▶️ How to Run
1. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib seaborn scikit-learn xgboost joblib
   ```
2. Place `city_day.csv` in the same directory as `main.ipynb`.
3. Run the notebook top to bottom in Jupyter.

---

## 🚀 Future Scope
🔹 Improve accuracy using **Deep Learning (LSTMs, CNNs)** for time-dependent AQI patterns.
🔹 Integrate real-time AQI data & meteorological features (temperature, humidity, wind speed).
🔹 Re-encode `City` and extract seasonal features from `Date` instead of dropping them, since AQI is strongly seasonal.
🔹 Develop an AI-powered dashboard or mobile app for real-time AQI tracking.

---
