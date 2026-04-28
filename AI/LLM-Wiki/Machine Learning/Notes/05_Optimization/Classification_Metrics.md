---
id: 05-clme-a1b2
tags: [agentic-ai, 05_Optimization, ml-metrics]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Classification Metrics

> [!ABSTRACT]
> Evaluating a classifier is more complex than a regressor, especially for skewed datasets where accuracy is misleading. Core metrics include the Confusion Matrix, Precision, Recall, and the F1 Score, which provide a more nuanced view of a model's performance on different classes.

## 🧠 Intuition First
- Imagine you're a doctor testing for a rare disease (1% of population). 
- **Accuracy:** If you always say "Negative," you'll be 99% accurate, but you'll never find the sick people. Accuracy is a "Nostradamus" metric—it's right by default but useless for the goal.
- **Precision:** "Of all the people I said have the disease, how many actually have it?" (Quality).
- **Recall:** "Of all the people who actually have the disease, how many did I find?" (Quantity).
- **F1 Score:** A single number that balances both.

## 🎯 Why This Matters
- Problem it solves: Prevents "false confidence" in models trained on imbalanced data.
- Real-world usage: Spam filters (high precision needed) vs. shoplifter detection (high recall needed).

## 🧩 Glossary
- [[Confusion Matrix]] : A table counting true/false positives and negatives.
- [[Precision]] : Accuracy of the positive predictions. $TP / (TP + FP)$.
- [[Recall]] : Ratio of positive instances correctly detected. $TP / (TP + FN)$. Also called **Sensitivity** or **True Positive Rate (TPR)**.
- [[F1 Score]] : The harmonic mean of precision and recall. It gives much more weight to low values.

## ⚙️ Mechanics (First Principles)
### The Confusion Matrix:
- **Rows:** Actual classes.
- **Columns:** Predicted classes.
- **True Negative (TN):** Correctly predicted negative.
- **False Positive (FP):** Wrongly predicted positive (Type I error).
- **False Negative (FN):** Wrongly predicted negative (Type II error).
- **True Positive (TP):** Correctly predicted positive.

## 📐 Mathematical Foundations
- **F1 Score Equation:**
  $F_1 = \frac{2}{\frac{1}{precision} + \frac{1}{recall}} = 2 \cdot \frac{precision \cdot recall}{precision + recall}$

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.metrics import confusion_matrix, precision_score, recall_score, f1_score

# Compute matrix
cm = confusion_matrix(y_true, y_pred)
# Get scores
p = precision_score(y_true, y_pred)
r = recall_score(y_true, y_pred)
f1 = f1_score(y_true, y_pred)
```

## 🧪 Experiments
1. **The Dummy Test:** Train a "Dummy Classifier" that always predicts the majority class. Observe its 90%+ accuracy but 0% precision and recall.

## ⚠️ Constraints & Pitfalls
- **Harmonic Mean Bias:** The F1 score favors classifiers that have similar precision and recall. This is not always what you want (e.g., in medical diagnosis, you often prefer higher recall even if precision is lower).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Classification_Basics]]
- Used in → [[Precision_Recall_Tradeoff]]
- Related to → [[ROC_and_AUC]]
---
(MINIMUM 3 links)
