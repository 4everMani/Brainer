---
id: 05-trde-a1b2
tags: [agentic-ai, 05_Optimization, model-tuning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Precision Recall Tradeoff

> [!ABSTRACT]
> For any classifier, there is a fundamental trade-off: as you increase precision, you generally decrease recall, and vice-versa. This is controlled by adjusting the model's decision threshold.

## 🧠 Intuition First
- Imagine a security guard deciding if a person is a "threat."
- **Low Threshold:** If you think anyone who looks suspicious *might* be a threat, you'll catch almost all threats (high recall), but you'll also falsely accuse many innocent people (low precision).
- **High Threshold:** If you only stop people when you're 99% sure they're a threat, you'll rarely be wrong (high precision), but you'll miss many clever or less obvious threats (low recall).

## 🎯 Why This Matters
- Problem it solves: Allows developers to fine-tune a model to match a specific business objective (e.g., safety vs. convenience).
- Real-world usage: Making a kids-safe video filter (high precision to avoid bad videos) vs. a shoplifter-detecting camera (high recall to catch all shoplifters).

## 🧩 Glossary
- [[Decision Threshold]] : The numeric value that determines if an instance belongs to the positive or negative class.
- [[PR Curve]] : A plot of precision versus recall for every possible threshold.
- [[Decision Function]] : A model's method that returns a score for each instance, which is then compared to the threshold.

## ⚙️ Mechanics (First Principles)
### The Trade-off Rule:
1. **Raising the Threshold:** Increases precision (fewer false positives) but decreases recall (more false negatives).
2. **Lowering the Threshold:** Decreases precision (more false positives) but increases recall (fewer false negatives).

### Model Selection Strategy:
- Plot the PR curve and find the "elbow"—the point where precision starts falling sharply. Pick a trade-off just before that drop (e.g., aiming for 90% precision).

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Adjusting threshold in Scikit-Learn:
```python
from sklearn.metrics import precision_recall_curve

# Get scores, not predictions
y_scores = sgd_clf.decision_function(X_train)
# Compute p/r for all thresholds
precisions, recalls, thresholds = precision_recall_curve(y_train, y_scores)

# Find threshold for 90% precision
idx = (precisions >= 0.90).argmax()
threshold_for_90 = thresholds[idx]

# Make custom predictions
y_pred_90 = (y_scores >= threshold_for_90)
```

## 🧪 Experiments
1. **The Threshold Sweep:** Take a binary classifier and manually increase the threshold in steps. Plot the resulting precision and recall values to recreate the PR curve yourself.

## ⚠️ Constraints & Pitfalls
- **One Score is Not Enough:** Never just report precision without recall. You can reach 99.9% precision easily by setting a near-infinite threshold, but the model will be useless because its recall will be near zero.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Classification_Metrics]]
- Used in → [[ROC_and_AUC]]
- Related to → [[Multiclass_Classification_Strategies]]
---
(MINIMUM 3 links)
