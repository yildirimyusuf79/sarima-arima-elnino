<div align="center">

# 🌊 ENSO Phase & Intensity Forecasting
### El Niño / La Niña Prediction with ARIMA & SARIMA

[![Python](https://img.shields.io/badge/Python-3.9%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://python.org)
[![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org)
[![statsmodels](https://img.shields.io/badge/statsmodels-Time%20Series-4B8BBE?style=for-the-badge)](https://www.statsmodels.org)
[![License](https://img.shields.io/badge/License-MIT-green?style=for-the-badge)](LICENSE)

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/5/55/ENSO_-_Pacific_SST_anomaly.jpg/1200px-ENSO_-_Pacific_SST_anomaly.jpg" width="700" alt="ENSO SST Anomaly Map"/>

> **Graduation Project** — Time series analysis and forecasting of the El Niño-Southern Oscillation (ENSO) using classical statistical models (ARIMA, SARIMA) on historical climate data spanning 1950–2023.

</div>

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Methodology](#-methodology)
- [Models & Results](#-models--results)
- [Key Findings](#-key-findings)
- [Installation](#-installation)
- [Usage](#-usage)
- [Technologies](#-technologies)

---

## 🌐 Overview

**ENSO (El Niño-Southern Oscillation)** is one of the most influential climate patterns on Earth. It alternates between three phases:

| Phase | SST Anomaly | Global Impact |
|-------|-------------|---------------|
| 🔴 **El Niño** | > +0.5°C | Droughts in Amazon & NE Brazil; flooding in southern Brazil |
| 🔵 **La Niña** | < −0.5°C | Heavy rains in NE Brazil; droughts in southern Brazil |
| ⚪ **Neutral** | −0.5°C to +0.5°C | Near-normal conditions worldwide |

This project builds a **time series forecasting pipeline** to predict Niño 3.4 SST Anomalies up to **24 months ahead**, with phase classification and scenario-based risk analysis.

---

## 📊 Dataset

**Source:** ENSO Climate Dataset (`ENSO.csv`)  
**Coverage:** 1950 – 2023 (monthly frequency)

### Key Features

| Variable | Description |
|----------|-------------|
| `Nino 3.4 SST Anomalies` | Sea surface temperature anomaly in Niño 3.4 region — primary target |
| `Nino 1+2 / 3 / 4 SST Anomalies` | SST anomalies across different Pacific regions |
| `ONI` | Oceanic Niño Index |
| `SOI` | Southern Oscillation Index |
| `MEI.v2` | Multivariate ENSO Index v2 |
| `OLR` | Outgoing Longwave Radiation |
| `TNI` | Trans-Niño Index |
| `PNA` | Pacific–North American pattern |
| `Global Temperature Anomalies` | Global mean surface temperature anomaly |
| `Global Precipitation` | Monthly global precipitation |

---

## 📁 Project Structure

```
📦 Bitirme Projesi
 ┣ 📓 proje.ipynb                                          # Main project notebook
 ┃   ├── 🔍 EDA & Data Preprocessing
 ┃   ├── 📉 Anomaly Detection (Z-Score)
 ┃   ├── 📈 Time Series Decomposition (ACF / PACF)
 ┃   ├── 🧪 Stationarity Testing (ADF Test)
 ┃   ├── 🤖 ARIMA & SARIMA Modeling
 ┃   ├── 📊 Model Comparison
 ┃   ├── 🔮 12 & 24-Month Forecasting
 ┃   ├── ⚠️  Risk Scenario Analysis
 ┃   └── 🏷️  ENSO Phase Classification (ML)
 ┣ 📓 time-series-sarima-arima-forecast-elnino-lanina.ipynb # Reference analysis notebook
 ┣ 📄 ENSO.csv                                             # Dataset
 ┗ 📄 socrata_metadata.json                                # Dataset metadata
```

---

## 🔬 Methodology

### 1. Exploratory Data Analysis
- Statistical summary and missing value detection
- Temporal distribution of ENSO phases over 70+ years
- Rolling Z-score anomaly detection on SST Anomaly series
- Correlation analysis between climate indicators

### 2. Time Series Decomposition
- **Seasonal Decompose** (additive model, period=12)
- **ACF / PACF** plots for parameter identification
- **ADF (Augmented Dickey-Fuller) Test** for stationarity verification

### 3. Forecasting Models

```
SARIMA(1,0,1)(1,0,1)[12]  ←  Seasonal ARIMA for monthly climate cycles
ARIMA(1,1,1)               ←  First-differenced model for trend removal
ARIMA(2,0,1)               ←  Higher-order AR for autocorrelation capture
Naïve Baseline             ←  Last observed value
Moving Average (MA-12)     ←  12-month rolling mean baseline
```

### 4. Evaluation & Validation
- **80/20 train-test split** (maintaining temporal order — no data leakage)
- Metrics: **MAE** (Mean Absolute Error) and **RMSE** (Root Mean Squared Error)
- Confidence interval estimation for probabilistic forecasts

### 5. Phase Classification
- Rule-based labeling: El Niño (>0.5°C) / La Niña (<-0.5°C) / Normal
- Feature engineering with multi-region SST, SOI, OLR, MEI.v2
- Machine learning classification on labeled ENSO phases

---

## 📈 Models & Results

### Forecast Comparison (Test Period)

| Model | MAE | RMSE |
|-------|-----|------|
| **SARIMA(1,0,1)(1,0,1,12)** | — | Best seasonal fit |
| ARIMA(2,0,1) | — | Good short-term accuracy |
| ARIMA(1,1,1) | — | Stable trend modeling |
| Naïve Baseline | Higher | Benchmark |
| Moving Average (12) | Higher | Benchmark |

> Exact metrics are computed and displayed in `proje.ipynb` upon execution.

### Forecast Horizons

- **12-month ahead forecast** with 95% confidence intervals
- **24-month ahead forecast** with risk scenario bands (+0.1°C / +0.2°C)

---

## 🔑 Key Findings

- The **Niño 3.4 SST Anomaly** series shows strong **annual seasonality** (period = 12 months), making SARIMA the most appropriate model.
- The **ADF test** confirms stationarity of the raw series, allowing ARIMA models without heavy differencing.
- **SARIMA** outperforms naive baselines by capturing both trend and seasonal components simultaneously.
- Historical El Niño events (1997–98, 2015–16) and La Niña events (2010–11, 2020–21) are clearly visible as anomalous spikes/dips in the SST anomaly series.
- Risk scenario analysis shows potential for moderate El Niño conditions in the 24-month forecast window.

---

## ⚙️ Installation

### Prerequisites
- Python 3.9 or higher
- Jupyter Notebook / JupyterLab

### Setup

```bash
# Clone the repository
git clone https://github.com/yildirimyusuf79/sarima-arima-elnino.git
cd sarima-arima-elnino

# Create and activate virtual environment (recommended)
python -m venv venv
venv\Scripts\activate        # Windows
# source venv/bin/activate   # macOS/Linux

# Install dependencies
pip install pandas numpy matplotlib statsmodels scikit-learn jupyter
```

---

## 🚀 Usage

```bash
# Launch Jupyter Notebook
jupyter notebook

# Open the main notebook
# → proje.ipynb
```

Run the cells sequentially. The notebook is self-contained and will automatically detect `ENSO.csv` in the working directory.

---

## 🛠️ Technologies

<div align="center">

| Library | Purpose |
|---------|---------|
| `pandas` | Data manipulation & time series indexing |
| `numpy` | Numerical operations & Z-score anomaly detection |
| `matplotlib` | Visualization (time series plots, forecast charts) |
| `statsmodels` | ARIMA, SARIMA, ADF test, seasonal decomposition, ACF/PACF |
| `scikit-learn` | MAE/RMSE evaluation metrics, ML classification |

</div>

---

## 👤 Author

**Yusuf Yıldırım**  
Graduation Project — 2026  
📧 yusufyildirim846@gmail.com  
🔗 [github.com/yildirimyusuf79](https://github.com/yildirimyusuf79)

---

<div align="center">

*"Climate is what we expect, weather is what we get."*  
— Mark Twain

</div>
