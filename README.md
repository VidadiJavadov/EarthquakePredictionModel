# 🌋 LANL Earthquake Prediction - Acoustic Signal Analysis

This repository contains a Machine Learning solution for the **LANL Earthquake Prediction** challenge. The goal is to predict the time remaining before a laboratory earthquake occurs based on real-time seismic acoustic data.

## 📌 Project Overview
Predicting earthquakes is one of the "Holy Grails" of geophysics. This project uses data from a laboratory experiment where a machine simulates rock slippage (earthquakes). 

**The Challenge:** The input data is a massive continuous stream of acoustic signals (over 600 million rows). The model must listen to a short segment of this sound and predict exactly how many seconds remain until the next failure.

## 📊 Performance
- **Model Used:** Random Forest Regressor
- **Validation Score (MAE):** `2.2247` seconds
- **Baseline (Mean Guess):** ~3.5 seconds
- **Improvement:** The model successfully captures the signal patterns, significantly outperforming random guessing.

## 🧠 Methodology

### 1. Data Handling (Chunking)
The raw dataset is too large (9GB+) to load into RAM at once.
- **Strategy:** The data is processed in chunks of **150,000 rows** (representing approx 0.0375 seconds of high-frequency audio).
- **Total Chunks:** ~4,194 segments processed.

### 2. Feature Engineering
Since raw audio waves are noisy, we extract statistical features to capture the "texture" of the sound. For every 150,000 rows, we calculate:
- **Mean & Std Dev:** To capture average intensity and vibration variance.
- **Min & Max:** To detect the loudest "pops" or signal spikes.
- **Absolute Extremes:** `abs_max`, `abs_mean`.
- **Quantiles (95% & 99%):** To capture the distribution of the loudest top % of signals (outliers).

### 3. Machine Learning Model
- **Algorithm:** Random Forest Regressor (`sklearn`).
- **Parameters:** `n_estimators=100`.
- **Why Random Forest?** It is robust against overfitting and handles the non-linear relationship between acoustic spikes and time-to-failure effectively.



[Image of random forest architecture]


## 🛠️ How to Run

### Prerequisites
You need Python 3.x and the following libraries:
```bash
pip install pandas numpy scikit-learn matplotlib tqdm
