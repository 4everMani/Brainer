---
id: 05-succ-m1s2
tags: [agentic-ai, 05_Optimization, metrics]
source: building-machine-learning-powered-applications-going-from-idea-to-product.pdf
date: 2026-04-22
type: technical-note
---

# ML Success Metrics

> [!ABSTRACT]
> ML Success Metrics define how the performance of a machine learning model is measured and how it relates to the overall product goal. Success requires a hierarchy of metrics, ranging from high-level business outcomes to granular model-specific performance indicators.

## 🧠 Intuition First
- Imagine you are building a GPS for hikers. The **Product Goal** is "don't let people get lost." The **Business Metric** might be "number of rescued hikers" (lower is better). The **Model Metric** might be "prediction error in meters." If the model is very accurate (low error) but only works when there is cell service, it fails the product goal even if the model metrics are "good."

## 🎯 Why This Matters
- Problem it solves: Alignment between technical optimization and business value.
- Real-world usage: Using **Guardrail Metrics** to ensure that while increasing CTR (Click-Through Rate), you aren't also increasing the amount of offensive content shown.

## 🧩 Glossary
- [[Business Metric]] : High-level outcome (e.g., Revenue, User Retention).
- [[Model Metric]] : Technical performance (e.g., Precision, RMSE).
- [[Guardrail Metric]] : Secondary metrics monitored to prevent unintended negative side effects.
- [[Offline Metric]] : A metric calculated on a historical dataset before the model is deployed.

## ⚙️ Mechanics (First Principles)
- **Hierarchy of Metrics:** 
    1. **Business Performance:** Does it make/save money or satisfy users?
    2. **Product Performance:** Does it perform the intended task (e.g., accuracy of a recommendation)?
    3. **Model Performance:** Technical evaluation (e.g., Precision vs. Recall).
- **Metric Selection:** Choose metrics that penalize the most costly errors. For a writing assistant, **Precision** is prioritized over recall because giving bad advice is more harmful than giving no advice.
- **Freshness and Speed:** Metrics must also account for how quickly the model generates a result (Latency) and how often it needs to be updated (Freshness).

## 📐 Mathematical Foundations
- **Precision:** $P = \frac{TP}{TP + FP}$
- **Recall:** $R = \frac{TP}{TP + FN}$
- **F1-Score:** $2 \cdot \frac{Precision \cdot Recall}{Precision + Recall}$

## 💻 Implementation
- Conceptual selection for "Question Quality" model:
    - **Goal:** Filter out bad questions.
    - **Primary Model Metric:** Precision (ensure questions marked "bad" truly are bad).
    - **Guardrail Metric:** Throughput (ensure we don't accidentally filter out 99% of all questions).
    - **Product Metric:** User satisfaction ratings on filtered results.

## 🧪 Experiments
1. **Metric Trade-off Analysis:** Plot a Precision-Recall curve and identify the point that minimizes the specific cost of your application's failure mode.
2. **Impact Bottleneck Identification:** Replace a model component with a "perfect" manual heuristic to see how much the business metric improves; this identifies where to focus optimization.

## ⚠️ Constraints & Pitfalls
- **Metric Misalignment:** Optimizing for Accuracy on an imbalanced dataset (e.g., 99% of transactions are legitimate, so a model that always says "Legitimate" is 99% accurate but useless).
- **Proxy Failure:** Using a metric that is easy to measure but doesn't correlate with user value.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[ML_Framing]]
- Used in → [[Model_Debugging_Process]]
- Related to → [[Bias_And_Variance]]
