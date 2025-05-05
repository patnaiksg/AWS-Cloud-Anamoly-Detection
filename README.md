# AWS CloudWatch Anomaly Detection & Clustering Dashboard

This project provides an end-to-end framework to stream, cluster, and visualize performance metrics from AWS CloudWatch using multiple unsupervised learning techniques.

---

## 📌 Objective

Detect performance anomalies from CloudWatch logs and group system behavior patterns into risk-based clusters using unsupervised machine learning — with free-tier AWS services and open-source Python tooling.

---

## 📊 Features

- 📥 Stream data from CloudWatch CSV (simulated or real-time via Kinesis)
- 📈 Feature Engineering & Scaling
- 🤖 Clustering Models:
  - KMeans with Elbow Method
  - DBSCAN for noise detection
  - Ensemble Clustering (KMeans + DBSCAN)
  - Hierarchical Clustering with Dendrogram
  - KMedoids (robust clustering)
- 🧠 Risk-based cluster labeling (Idle, Normal, High Load, Critical)
- 🔥 Anomaly identification using latency, CPU, and active connections
- 📊 Heatmaps for per-feature intensity
- 🧬 PCA-based visualizations
- 📌 Auto risk-tagging & alert logic (planned for Lambda/SNS integration)

---

## 🛠️ Tech Stack

- Python 3.x
- Pandas, NumPy
- scikit-learn, scikit-learn-extra
- Seaborn, Matplotlib
- AWS CloudWatch (data source), Kinesis
- SageMaker or Lambda (for real-time inference deployment - optional)

---

## Dashboard Preview

- ![Dashboard Screenshot 1](dash1.png)
- ![Dashboard Screenshot 2](dash2.png)
