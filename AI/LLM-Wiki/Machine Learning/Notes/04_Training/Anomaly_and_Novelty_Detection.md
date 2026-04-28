---
id: 04-anom-a1b2
tags: [agentic-ai, 04_Training, clustering]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Anomaly and Novelty Detection

> [!ABSTRACT]
> Anomaly detection is the task of identifying abnormal instances (outliers) that differ significantly from the "normal" training data. Novelty detection differs by assuming the training set is "clean" (uncontaminated by outliers). Both tasks often leverage density estimation techniques like GMMs to identify instances in low-density regions.

## 🧠 Intuition First
- **Anomaly Detection:** You're a security guard at a museum. You watch everyone and flag anyone doing something weird (running, touching art). You don't assume everyone is good initially; you just look for the weirdness.
- **Novelty Detection:** You're an expert who knows exactly what a "standard" diamond looks like. You're given a new stone. If it has a different crystalline structure, you flag it as "new" or "different." You only learn the "normal" pattern and compare everything to that standard.

## 🎯 Why This Matters
- Problem it solves: Automates the detection of fraud, equipment failure, or data quality issues.
- Real-world usage: Identifying defective products on a production line, credit card fraud detection, and identifying new trends in time-series data.

## 🧩 Glossary
- [[Anomaly]] : An observation that deviates so much from other observations as to arouse suspicion (also called **Outlier**).
- [[Novelty]] : A new type of instance that was not present in the training set.
- [[Density Estimation]] : Estimating the probability density function (PDF) of the data-generating process.
- [[Inlier]] : A "normal" instance that follows the standard distribution.

## ⚙️ Mechanics (First Principles)
### Using GMM for Detection:
1. **Train:** Fit a GMM on the available data.
2. **Score:** Use `score_samples()` to get the log of the density at each instance.
3. **Threshold:** Define a density threshold (e.g., the 4th percentile). 
4. **Identify:** Any instance below the threshold is an anomaly.

### Other Algorithms:
- **Fast-MCD:** Assumes data is Gaussian but ignores outliers when estimating parameters.
- **Isolation Forest:** Efficiently identifies anomalies by randomly partitioning features (anomalies are easier to isolate).
- **One-class SVM:** Learns the boundary of the normal class.

## 📐 Mathematical Foundations
- **Percentile Thresholding:** Setting $T$ such that $P(PDF(x) < T) = \alpha$, where $\alpha$ is the expected contamination rate.

## 💻 Implementation
- GMM Anomaly Detection:
```python
densities = gm.score_samples(X)
# Set threshold at the 4th percentile
threshold = np.percentile(densities, 4)
anomalies = X[densities < threshold]
```

## 🧪 Experiments
1. **The Contamination Test:** Artificially add 10 random noise points to a 2-cluster dataset. Train a GMM and see if the 4th percentile threshold correctly identifies those 10 points.

## ⚠️ Constraints & Pitfalls
- **Outlier Bias:** GMM tries to fit all data. If the dataset is too contaminated, the GMM will "normalize" the outliers and fail to detect them.
- **Novelty Assumption:** Novelty detection will fail if the training set used to define "normal" is actually contaminated.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Gaussian_Mixture_Models]]
- Used in → [[ML_Success_Metrics]]
- Related to → [[DBSCAN_and_Density_Clustering]]
---
(MINIMUM 3 links)
