# 🌪️ Adversarial Forecasting with LSTM vs GAN-LSTM

### A Comparative Analysis for Wind-Speed Prediction

---

## 📌 Overview

This project explores the limitations of traditional **LSTM-based time-series forecasting** and introduces a **lightweight adversarial refinement strategy** to improve long-horizon predictions.

Instead of building a full GAN model, this work enhances a pretrained LSTM using a discriminator that evaluates the realism of predictions — resulting in more stable and structurally consistent forecasts.

---

## 🚀 Key Idea

Standard LSTMs perform well for short-term forecasting but struggle with:

* ❌ Error accumulation in multi-step predictions
* ❌ Loss of temporal structure
* ❌ Overly smooth or unstable long-term outputs

💡 **Solution:**
A **GAN-inspired refinement**, where:

* LSTM acts as the **generator (forecaster)**
* A discriminator evaluates **real vs predicted next-step values**
* Training combines **prediction accuracy + adversarial realism**

---

## 🧠 Methodology

### 1. Data Processing

* Multivariate weather dataset (wind, temperature, rainfall, etc.)
* Feature engineering:

  * Cyclical encoding (day of week, yearly patterns)
* Standardization using `StandardScaler`
* Chronological split (Train / Validation / Test)

---

### 2. Baseline Model (LSTM)

* Single-layer LSTM (64 units)
* Dropout for regularization
* Predicts **next-day weather features**
* Trained using weighted MSE loss

---

### 3. Adversarial Refinement (GAN-LSTM)

Instead of full GAN training:

* ✔️ Pretrained LSTM reused
* ✔️ Discriminator evaluates next-step realism
* ✔️ Combined loss:

[
L = L_{MSE} + \lambda L_{GAN}
]

* ✔️ Alternating training:

  * Train discriminator
  * Train forecaster

---

### 4. Evaluation Strategy

Multi-step forecasting via **autoregressive rollout**:

* Predict next step → feed back → repeat

Evaluated on:

* 3-day horizon
* 5-day horizon
* 10-day horizon

---

## 📊 Metrics Used

Beyond standard accuracy, this project emphasizes **temporal realism**:

* 📉 **MAE / RMSE** – prediction accuracy
* 📆 **Day-wise MAE** – error accumulation
* ⚡ **Rare-event MAE** – extreme wind prediction
* 📈 **Sharpness** – variability of predictions
* 🔁 **ACF Cosine Similarity** – temporal structure preservation

---

## 🏆 Results Summary

### ✅ Short-Term (3 Days)

* Significant MAE reduction (~65% on Day 1)
* Better rare-event prediction
* Similar temporal structure

### ✅ Medium-Term (5 Days)

* Strong improvement in **temporal coherence**
* ACF similarity improved from ~0 → ~0.97
* More stable predictions

### ✅ Long-Term (10 Days)

* Slower error accumulation
* Smoother and more realistic forecasts
* Better structural consistency

---

## 🔍 Key Takeaways

* Lightweight adversarial refinement **works surprisingly well**
* Improves **long-horizon stability** without complex GAN training
* Structural metrics (like ACF) are **crucial** for time-series evaluation
* Simple improvements can outperform heavier architectures

---

## 🛠️ Tech Stack

* Python
* TensorFlow / Keras
* NumPy / Pandas
* Scikit-learn

---

## 🔮 Future Work

* Multi-step discriminators (sequence-level realism)
* Transformer-based forecasting models
* Physics-informed constraints
* Real-world deployment (e.g., wind energy systems)

---

## 📄 Author

**Ananto Nayan Bala**
CSE, AUST

---

## ⭐ Final Note

This project was developed as part of an academic term project and focuses on improving **practical time-series forecasting** using a simple yet effective adversarial approach.

If you found this interesting, feel free to ⭐ the repo or reach out!

---
