# Gait-Based Biometric Identification and Verification using Neural Networks

This repository contains my implementation for **CS 288 – Biometric Security with AI (Fall 2025)**.  
The project focuses on building a gait-based biometric system using smartphone accelerometer and gyroscope data.

---

## 📘 Overview
The goal of this project is to identify and verify users based on their walking patterns.  
I implemented two different neural network approaches:

- **Feedforward Neural Network (FNN)** — uses handcrafted statistical and frequency features.
- **Long Short-Term Memory (LSTM)** — uses the raw 6-channel time-series directly.

Both models were trained and tested for:
- **User Identification (1-in-N classification)**  
- **User Verification (1-vs-All binary authentication)**

---

## 🧠 Methodology

### 🔹 Preprocessing
- Combined accelerometer and gyroscope data into a 6-channel signal.  
- Segmented into **5-second windows with 50% overlap**.  
- Applied **Z-score outlier clipping** and a **5-point moving average filter** for noise reduction.

### 🔹 FNN Approach
- Extracted 78 features (statistical + frequency-domain) per window.  
- Used **PCA** to reduce to 10 key components.  
- Architecture: 10 → (5 → 5) → 10 (Softmax).  
- Used 5-fold cross-validation and early stopping.

### 🔹 LSTM Approach
- Used raw signals (250×6 per window).  
- Architecture: 5 stacked LSTM layers (6 units each), dense(6) → Softmax(10).  
- Regularized with dropout and batch normalization.  
- Also evaluated for user verification (binary setup).

---

## 📊 Results Summary

| Model | Task | Accuracy | AUC | EER | Key Observation |
|-------|------|-----------|------|------|----------------|
| **FNN** | Identification | 0.90 | – | – | Stable, strong performance |
| **LSTM** | Identification | 0.57 | – | – | Underfit, limited by data |
| **FNN** | Verification | 0.98 | 0.99 | 0.03 | Excellent separation |
| **LSTM** | Verification | 0.97 | 0.99 | 0.02 | Slightly higher FRR |

*(Plots for accuracy, confusion matrices, and ROC curves are available in the `results/plots/` folder.)*

---

## 🧩 Repository Structure

