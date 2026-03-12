# Bayesian Adaptive Fault Observer (BAFO)

![BAFO Monitoring Dashboard](figures/monitoring_dashboard.png)

*Monitoring dashboard comparing BAFO with classical vibration monitoring methods.*

A probabilistic monitoring framework for detecting operational regime changes and fault conditions in industrial machinery.

This project presents the development and evaluation of the **Bayesian Adaptive Fault Observer (BAFO)**, a dynamic anomaly detection approach inspired by concepts from **Bayesian inference**, **multivariate statistical monitoring**, and **state observers from control theory**.

The framework is evaluated using a simulated industrial motor model and compared against classical monitoring approaches such as **RMS threshold monitoring** and **PCA-based Multivariate Statistical Process Control (MSPC)**.

---

# Overview

Industrial condition monitoring systems must detect abnormal operating conditions while remaining robust to noise, transient disturbances, and operational variability.

Traditional monitoring approaches typically rely on:

- amplitude thresholds
- static statistical models

However, these methods may struggle to detect **regime changes and structural faults** in complex systems.

The **BAFO framework** addresses this challenge by integrating:

- multivariate statistical evidence
- Bayesian probabilistic updates
- temporal state observation

resulting in a monitoring method capable of detecting **regime divergence and fault evolution**.

---

# Feature Engineering

Vibration signals are segmented into temporal windows and converted into statistical descriptors:

- RMS
- Kurtosis
- Crest Factor
- Skewness

A correlation analysis revealed strong redundancy between RMS and standard deviation.

![Feature Correlation Matrix](figures/correlation_matrix.png)

Due to the **high correlation between RMS and STD (ρ ≈ 0.97)**, the STD feature was removed to avoid multicollinearity and improve the numerical conditioning of the covariance matrix used in multivariate monitoring.

---

# Operational Regime Feature Space

The extracted features form a multivariate representation of machine behavior across simulated regimes.

![Feature Space by Scenario](figures/feature_space.png)

Different fault conditions produce distinct patterns in the feature space.  
This separation allows statistical monitoring methods to identify regime transitions and abnormal operating conditions.

---

# Monitoring Framework

The monitoring pipeline follows four stages:

**Monitoring Pipeline**

Simulation → Feature Extraction → Fault Detection → Evaluation

### Multivariate Regime Signal

A **Mahalanobis distance-based regime score** is constructed using baseline operating conditions.

This score measures the deviation of the current feature vector from the reference operating regime.

---

# Bayesian Adaptive Fault Observer (BAFO)

The **BAFO** framework operates as a probabilistic state observer that integrates multivariate evidence over time.

Conceptually:

```
Multivariate Evidence
        ↓
    Bayesian Update
        ↓
Health State Observer
```

This structure allows the observer to react to regime changes while maintaining robustness to impulsive disturbances and transient noise.

---

# Monitoring Dashboard

The monitoring dashboard combines multiple signals to evaluate system behavior:

- operational regime timeline
- Mahalanobis regime score
- PCA Hotelling T² statistic
- RMS threshold monitoring
- BAFO posterior and health state

![Monitoring Dashboard](figures/monitoring_dashboard.png)

This consolidated view enables direct comparison between the proposed observer and classical detection methods.

---

# Benchmark Methods

The proposed approach is compared with two commonly used monitoring strategies.

### RMS Threshold Monitoring

A classical vibration monitoring method based on amplitude thresholds.

### PCA-Based Multivariate Statistical Process Control (MSPC)

A multivariate monitoring technique using the **Hotelling T² statistic**.

These methods serve as baseline detectors for evaluating BAFO performance.

---

# Detection Performance

Detection delay was measured for each simulated regime.

![Detection Delay](figures/detection_delay.png)

Key observations:

- RMS threshold monitoring fails to detect several structural faults.
- PCA-based MSPC detects most regimes but exhibits sensitivity to transient disturbances.
- BAFO detects all simulated regimes while maintaining smoother temporal behavior.

---

# Fault Detection Map

The fault detection timeline highlights when each detector identifies regime changes.

![Fault Detection Map](figures/fault_detection_map.png)

BAFO demonstrates consistent detection across all simulated regimes while maintaining temporal stability.

---

# Applications

The proposed monitoring framework is applicable to:

- rotating machinery monitoring
- predictive maintenance systems
- industrial SCADA monitoring
- edge-based machine health monitoring
- anomaly detection in industrial processes

---

# Repository Structure

```
BAFO/
│
├── notebooks
│   └── motor_model.ipynb
│
├── figures
│   ├── correlation_matrix.png
│   ├── feature_space.png
│   ├── monitoring_dashboard.png
│   ├── detection_delay.png
│   └── fault_detection_map.png
│
├── src
│
├── README.md
└── requirements.txt
```

---

# Author

Victor Dutra  
Control & Automation Engineer  
Industrial Data & Process Analytics
