# Multivariate Sensor Anomaly Detection: PCA vs. Neighborhood Embedding (GEM/k-NN)

A comparative machine learning framework designed to detect operational anomalies in multi-channel telemetry and industrial sensor networks. This repository implements and evaluates two complementary unsupervised paradigms: **Principal Component Analysis (PCA)** for linear subspace reconstruction and **Graph/Neighborhood Embeddings (GEM via k-NN)** for local density estimation.

---

## 📌 Problem Overview

Industrial control systems, satellite telemetry, and aerospace sensors generate high-frequency multivariate time-series data. In many operating regimes, labeled anomalous data is scarce or nonexistent.

This project explores unsupervised anomaly detection on an automated system monitored by **10 distinct sensor channels** across time:

- **Data Topology:** 10 synchronized sensor streams tracking operational parameters.
- **Challenge:** Identifying transient faults, sensor degradation, and systemic out-of-nominal behavior without supervised labels.
- **Approaches:**
  1. **PCA (Global/Linear):** Identifies anomalies when the linear relationship between sensor dimensions breaks down.
  2. **k-NN/GEM (Local/Non-Linear):** Detects states that depart from typical operational clusters in the metric manifold.

---

## ⚙️ Algorithms & Methodology

### 1. Principal Component Analysis (PCA)
- **Dimensionality Reduction:** Computes the covariance matrix across sensor channels to extract dominant eigenvectors[cite: 1].
- **Metric:** **Squared Prediction Error (SPE / Reconstruction Error):**
  > **`SPE(x) = ||x - x̂||² = ||x - P Pᵀ x||²`**
- Samples exhibiting a high reconstruction error indicate a violation of standard multi-sensor correlations.

### 2. Graph / Neighborhood Embedding (GEM / k-NN)
- **Manifold Representation:** Maps sensor configurations to a metric vector space and constructs a k-nearest neighbor graph[cite: 2].
- **Metric:** **Mean Distance to k-Nearest Neighbors:**
  > **`Score(x) = (1 / k) * Σ ||x - x(i)||`**
- Samples with high distance scores reside in sparse regions of the operational manifold, signaling novel or faulty states.

---

## 📁 Repository Structure

```text
├── data.csv                 # Raw multi-channel sensor telemetry
├── PCA.ipynb                # PCA pipeline, reconstruction error, and residual scoring
├── GEM.ipynb                # k-NN / GEM neighborhood distance anomaly detector
├── anomaly_plots_PCA/       # Reconstruction error and anomaly threshold plots (PCA)
├── anomaly_plots_GEM/       # k-NN distance scores and detection visualizations (GEM)
├── anomaly_results_PCA/     # Exported evaluation metrics, predictions, and logs (PCA)
├── anomaly_results_GEM/     # Exported evaluation metrics, predictions, and logs (GEM)
└── README.md                # Project documentation and analysis
