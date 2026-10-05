# Multivariate Sensor Anomaly Detection: PCA vs. Geometric Entropy Minimization (GEM)

A comparative machine learning framework designed to detect operational anomalies in multi-channel telemetry and industrial sensor networks. This repository implements and evaluates two complementary unsupervised paradigms: **Principal Component Analysis (PCA)** for linear subspace reconstruction and **Geometric Entropy Minimization (GEM via k-NN)** for non-parametric minimum-volume set anomaly detection.

---

## 📌 Problem Overview

Industrial control systems, satellite telemetry, and aerospace sensors generate high-frequency multivariate time-series data. In many operating regimes, labeled anomalous data is scarce or nonexistent.

This project explores unsupervised anomaly detection on an automated system monitored by **10 distinct sensor channels** across time:

- **Data Topology:** 10 synchronized sensor streams tracking operational parameters.
- **Challenge:** Identifying transient faults, sensor degradation, and systemic out-of-nominal behavior without supervised labels.
- **Approaches:**
  1. **PCA (Global/Linear):** Identifies anomalies when the linear cross-correlation structure between sensor dimensions breaks down.
  2. **GEM (Non-Parametric/Geometric):** Uses Geometric Entropy Minimization via $k$-nearest neighbors to estimate a minimal-volume acceptance region for nominal states, flagging points falling outside as anomalies.

---

## ⚙️ Algorithms & Methodology

### 1. Principal Component Analysis (PCA)
- **Dimensionality Reduction:** Computes the covariance matrix across sensor channels to extract dominant eigenvectors[cite: 1].
- **Metric:** **Squared Prediction Error (SPE / Reconstruction Error):**
  > **`SPE(x) = ||x - x̂||² = ||x - P Pᵀ x||²`**
- Samples exhibiting a high reconstruction error indicate a violation of normal multi-sensor correlations.

### 2. Geometric Entropy Minimization (GEM via k-NN)
- **Theory:** Non-parametric method estimating a minimum-volume (low-entropy) acceptance region of normal data using $k$-nearest neighbor graph structures.
- **Metric:** **$k$-NN Distance / Empirical Entropy Score:**
  > **`Score(x) = (1 / k) * Σ ||x - x(i)||`**
- Points residing outside the dense normal operational region yield large neighbor distances and accumulate higher anomaly scores over a sliding window.

---

## 📁 Repository Structure

```text
├── data.csv                 # Raw multi-channel sensor telemetry
├── PCA.ipynb                # PCA pipeline, reconstruction error, and residual scoring
├── GEM.ipynb                # GEM-based k-NN sliding-window anomaly detector
├── anomaly_plots_PCA/       # Reconstruction error and anomaly threshold plots (PCA)
├── anomaly_plots_GEM/       # GEM distance scores and detection visualizations
├── anomaly_results_PCA/     # Exported evaluation metrics, predictions, and logs (PCA)
├── anomaly_results_GEM/     # Exported evaluation metrics, predictions, and logs (GEM)
└── README.md                # Project documentation and analysis
