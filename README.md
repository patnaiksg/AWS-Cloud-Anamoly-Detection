# AWS CloudWatch Anomaly Detection & Clustering Dashboard

This project demonstrates a **real-time anomaly detection pipeline** using simulated **Amazon CloudWatch performance metrics**. It is fully compatible with the **AWS Cloud** and utilizes **Kinesis**, **Lambda**, **DynamoDB** .

It’s designed to help **identify performance anomalies** in compute resources like EC2 by clustering real-time metrics and classifying unusual behavior as high-risk — allowing for early detection and response.

Modern cloud applications generate massive volumes of real-time performance telemetry across compute, storage, and network layers. While this data is critical for maintaining availability and performance, it becomes increasingly difficult to detect critical anomalies in real time due to sheer scale and complexity.

Traditional anomaly detection systems often operate as binary detectors — labeling data as "normal" or "anomalous" — without any contextual understanding of business impact. This results in:
- ❗ Alert fatigue due to false positives and low-priority noise
- 🧍‍♂️ Manual triaging of alerts, delaying responses to critical incidents
- 📉 Reactive monitoring, where damage is already done before detection

## 💡 Our Solution
We introduce an Adaptive Risk Scoring Mechanism integrated with a real-time streaming pipeline. It’s designed to:
- ✅ Assign dynamic risk levels to anomalies based on resource behavior, system context, and historical trends
- ✅ Reduce alert noise by intelligently suppressing low-impact anomalies
- ✅ Prioritize critical issues through cluster-based severity tagging
- ✅ Enable proactive monitoring with clear anomaly categorization (e.g., CPU bottleneck, network saturation)

## 🔍 Key Differentiators
- Cluster-aware anomaly ranking using unsupervised learning (KMeans/DBSCAN)
- Lightweight real-time pipeline using AWS Kinesis, Lambda, and DynamoDB
- Scalable risk labeling based on performance signatures instead of static thresholds
- Live dashboard visualization for engineering and operations teams to act swiftly


---

## Objective

Detect performance anomalies from CloudWatch logs and group system behavior patterns into risk-based clusters using unsupervised machine learning — with free-tier AWS services and open-source Python tooling.

---

## Motivation & Purpose
Cloud applications power critical business operations and services.
Even brief performance incidents or anomalies can cause significant financial, reputational, and operational impact.
Manual detection is often too slow, leading to delayed incident response and longer downtime.


Data-driven, automated anomaly detection enables:
Proactive incident management
Better resource optimization and cost savings
Enhanced service reliability and user experience
Our goal: Leverage unsupervised learning to detect, profile, and explain anomalies in real-world cloud application metrics.

## Features

- Stream data from CloudWatch CSV (simulated or real-time via Kinesis)
- Feature Engineering & Scaling
- Clustering Models:
  - KMeans with Elbow Method
  - DBSCAN for noise detection
  - Ensemble Clustering (KMeans + DBSCAN)
  - Hierarchical Clustering with Dendrogram
  - KMedoids (robust clustering)
- Risk-based cluster labeling (Idle, Normal, High Load, Critical)
- Anomaly identification using latency, CPU, and active connections
- Heatmaps for per-feature intensity
- PCA-based visualizations
- Auto risk-tagging & alert logic (planned for Lambda/SNS integration)

---

## Project Flow
### Stream Metrics via Kinesis
- A Python script reads metric rows from a CSV file.
- Each row is serialized to a Kinesis Data Stream (cloudwatch-metrics-stream).

### Predict Cluster (Risk) Label in Lambda

- A Lambda function is triggered on each Kinesis record.
- It loads a pre-trained clustering model (KMeans, DBSCAN, etc.) and scaler.
- The metric data is transformed, and a cluster label (risk level) is predicted.

### Display in Dashboard
Our dashboard fetches labeled risk levels of instances in real time.

Displays:
- Risk label distribution (e.g., bar chart)
- Recent metrics with anomaly highlights
- Future Work: time-series trends within the dashboard for better instance health monitoring

### Trigger Alerts

If the predicted cluster label matches a known anomaly or high-risk cluster:
- Sends an SNS alert (email, Slack, etc.)



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

- Live Dashboard to monitor the current risk level of the resources and operating conditions.
- ![Dashboard Screenshot 1](dash1.png)
- FIlter out instances with critical conditions as necessary.
- ![Dashboard Screenshot 2](dash_2.png)

---

## Limitations & Assumptions

- Data limitations:
Dataset lacks explicit labeled failures/incidents—evaluation is fully unsupervised.
- Assumptions:
Selected 10 core features are representative of overall cloud resource behavior.
Clusters identified via unsupervised learning truly reflect distinct operational states and anomalies.
Hyperparameter tuning (k, eps, min_samples) was performed using a limited grid due and might not be the same for all cloud scenarios.
- Model limitations:
Some true anomalies may be missed if they do not create clear feature separation.
Real-time applicability and generalizability to other cloud workloads need further validation.

---

## Future Scope

- Cross-Service Anomaly Correlation:
Expand the project to correlate with more anomalies across AWS services (e.g., EC2, RDS, S3) to detect systemic issues and complex failure chains in distributed systems.


- Alert Optimization:
Incorporate classification models to predict risk severity proactively (before anomaly occurs) and optimize alert thresholds to reduce false positives/alert fatigue.


- Incorporate feedback loop: 
Integrate engineer-validated incident labels to retrain and refine anomaly models (semi-supervised learning).


More Interactive Dashboards: Display additional system health data to enable enhanced monitoring.

---


