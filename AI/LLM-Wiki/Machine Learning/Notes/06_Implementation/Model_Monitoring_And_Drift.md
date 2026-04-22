---
id: 06-moni-d7r8
tags: [agentic-ai, 06_Implementation, monitoring]
source: building-machine-learning-powered-applications-going-from-idea-to-product.pdf
date: 2026-04-22
type: technical-note
---

# Model Monitoring and Drift

> [!ABSTRACT]
> Model Monitoring is the continuous tracking of a model's performance in production to ensure it remains accurate and safe. Performance often degrades over time due to **Drift**, where the statistical properties of the incoming data or the relationship between inputs and targets change.

## 🧠 Intuition First
- Imagine you have a model that predicts "what is in fashion." In the winter, it learns that "coats" are high value. When summer arrives, the data changes (it gets hotter), but the model still thinks "coats" are the answer. The model is no longer "fresh" because the world has moved on. This is **Drift**.

## 🎯 Why This Matters
- Problem it solves: Detects silent failures where the model continues to run but gives increasingly wrong answers.
- Real-world usage: Monitoring a house-price predictor to see if a sudden economic shift makes the model's past training data irrelevant.

## 🧩 Glossary
- [[Data Drift]] : (Feature Drift) Changes in the distribution of input data (e.g., more users from a new country).
- [[Concept Drift]] : Changes in the relationship between input and target (e.g., what was "spam" yesterday is "normal" today).
- [[Training-Serving Skew]] : Differences between the data used to train the model and the data it sees in production.

## ⚙️ Mechanics (First Principles)
1. **What to Monitor:**
    - **Software Metrics:** Latency, Memory, Throughput, Error rates (500s).
    - **Model Input Metrics:** Mean/Variance of features, percentage of missing values.
    - **Model Output Metrics:** Distribution of predictions (e.g., is the model suddenly predicting "Spam" 90% of the time?).
2. **Identifying Drift:** Compare the distribution of live data against the training data using statistical tests (e.g., Kolmogorov-Smirnov).
3. **Closing the Loop:** Use **Feedback Loops** (implicit or explicit) to get ground truth labels for live data and calculate actual performance.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Conceptual monitoring logic:
```python
def check_drift(training_mean, live_batch):
    live_mean = sum(live_batch) / len(live_batch)
    if abs(live_mean - training_mean) > threshold:
        trigger_alert("Data Drift detected in feature X")
```

## 🧪 Experiments
1. **Simulated Drift:** Take a test set and manually shift the values of one feature (e.g., add 10 to every age). Observe how your model's prediction distribution changes.
2. **Feedback Latency Analysis:** Measure how long it takes to get a "ground truth" label (e.g., did the user actually click the recommendation?). This determines how fast you can detect performance drops.

## ⚠️ Constraints & Pitfalls
- **The "Ground Truth" Delay:** In many cases (like loan defaults), you won't know if a prediction was right for months or years. In these cases, you must rely on **Proxy Metrics** (input distributions).
- **Alert Fatigue:** Setting monitoring thresholds too tight leads to many false alarms, causing engineers to ignore real issues.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Model_Deployment_Options]]
- Used in → [[ML_Success_Metrics]]
- Related to → [[Data_Leakage]]
