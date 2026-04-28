---
id: 05-roc-a1b2
tags: [agentic-ai, 05_Optimization, ml-metrics]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# ROC and AUC

> [!ABSTRACT]
> The Receiver Operating Characteristic (ROC) curve plots the True Positive Rate (Recall) against the False Positive Rate (FPR) for all possible thresholds. The Area Under the Curve (AUC) provides a single number to compare the overall performance of different classifiers.

## 🧠 Intuition First
- Imagine a radar operator looking for enemy planes. 
- **ROC:** If they're sensitive to any blip (high TPR), they'll also see many birds or clouds (high FPR). If they're very strict, they'll miss some planes but avoid all birds. The ROC curve is like a blueprint of the operator's decision-making ability.
- **AUC:** A perfect operator (1.0) always sees planes and never birds. A blind operator (0.5) just guesses randomly.

## 🎯 Why This Matters
- Problem it solves: Provides an overall assessment of a classifier's performance across all possible thresholds, making it easier to compare models.
- Real-world usage: Evaluating medical diagnostic tests or fraud detection systems.

## 🧩 Glossary
- [[ROC Curve]] : A plot of True Positive Rate (TPR) versus False Positive Rate (FPR).
- [[AUC]] : Area Under the Curve. 1.0 is perfect, 0.5 is random.
- [[FPR]] : False Positive Rate ($FP / (FP + TN)$). Also called **Fall-out**.
- [[TNR]] : True Negative Rate ($TN / (TN + FP)$). Also called **Specificity**.
- [[Sensitivity]] : Another name for Recall or TPR.

## ⚙️ Mechanics (First Principles)
### The ROC Trade-off:
1. **Raising Sensitivity (Recall):** Results in a higher False Positive Rate.
2. **Ideal Model:** Stays as far away from the random diagonal (top-left corner) as possible.
3. **Random Classifier:** A diagonal line ($AUC=0.5$).

## 📐 Mathematical Foundations
- **True Positive Rate (TPR):** $TP / (TP + FN)$
- **False Positive Rate (FPR):** $FP / (FP + TN) = 1 - Specificity$
- **Total ROC AUC:** The integral of the TPR over all possible FPR values.

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.metrics import roc_curve, roc_auc_score

# Compute TPR and FPR for all thresholds
fpr, tpr, thresholds = roc_curve(y_true, y_scores)
# Compute single score
auc = roc_auc_score(y_true, y_scores)
```

## 🧪 Experiments
1. **Random Comparison:** Plot the ROC curve for your trained model versus a random classifier (a straight diagonal line). Compare their AUC scores.

## ⚠️ Constraints & Pitfalls
- **Rare Positives:** If the positive class is very rare, the ROC curve can look deceptively good. In these cases (like rare diseases or fraud), **always prefer the PR curve**.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> **ROC vs PR:** Use PR curve when you care more about false positives than false negatives, or when the positive class is rare. Otherwise, use ROC.

## 🔗 Connections
- Builds on → [[Classification_Metrics]]
- Used in → [[Precision_Recall_Tradeoff]]
- Related to → [[Multiclass_Classification_Strategies]]
---
(MINIMUM 3 links)
