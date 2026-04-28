---
id: 05-regr-a1b2
tags: [agentic-ai, 05_Optimization, ml-metrics]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Regression Metrics

> [!ABSTRACT]
> Regression metrics quantify the performance of a model by measuring the distance between predicted values and actual target values. The most common metrics are Root Mean Squared Error (RMSE) and Mean Absolute Error (MAE), which correspond to different vector norms.

## 🧠 Intuition First
- Imagine you're throwing darts. 
- **RMSE:** If you miss the bullseye by a large margin even once, it counts heavily against your score. RMSE is like a harsh judge who penalizes big mistakes much more than small ones.
- **MAE:** This is like a friend who just averages the distance of all your throws from the bullseye. It treats a big miss as just another data point.

## 🎯 Why This Matters
- Problem it solves: Provides a objective way to compare the accuracy of different models.
- Real-world usage: Deciding which model to launch in a house price prediction system.

## 🧩 Glossary
- [[RMSE]] : Root Mean Squared Error. The most common performance measure for regression tasks.
- [[MAE]] : Mean Absolute Error. A performance measure that is more robust to outliers than RMSE.
- [[Outliers]] : Data points that are significantly different from the rest of the dataset.

## ⚙️ Mechanics (First Principles)
- Both metrics measure the distance between the vector of predictions ($\hat{y}$) and the vector of target values ($y$).
- **RMSE:** Corresponds to the **Euclidean norm** ($\ell_2$ norm). It is sensitive to outliers because errors are squared before being averaged.
- **MAE:** Corresponds to the **Manhattan norm** ($\ell_1$ norm). It is less sensitive to outliers.
- **Selection Rule:** If outliers are rare (e.g., in a bell-shaped curve), RMSE is usually preferred. If there are many outliers, MAE might be better.

## 📐 Mathematical Foundations
- **RMSE Equation:**
  $RMSE(X, h) = \sqrt{\frac{1}{m} \sum_{i=1}^{m} (h(x^{(i)}) - y^{(i)})^2}$
- **MAE Equation:**
  $MAE(X, h) = \frac{1}{m} \sum_{i=1}^{m} |h(x^{(i)}) - y^{(i)}|$
- **Vector Norms:**
  - $\ell_1$ norm ($\|v\|_1$): Sum of absolute values (Manhattan).
  - $\ell_2$ norm ($\|v\|_2$): Root of sum of squares (Euclidean).

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.metrics import mean_squared_error, mean_absolute_error
import numpy as np

rmse = np.sqrt(mean_squared_error(y_true, y_pred))
mae = mean_absolute_error(y_true, y_pred)
```

## 🧪 Experiments
1. **Outlier Impact:** Take a small dataset and manually change one value to be a huge outlier. Calculate both RMSE and MAE before and after the change and observe which one increases more.

## ⚠️ Constraints & Pitfalls
- **Capped Targets:** If the targets in the training set are capped (e.g., at $500,000), the model will never learn to predict beyond that limit, and RMSE will be artificially low.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[Linear_Regression]]
- Related to → [[Bias_And_Variance]]
---
(MINIMUM 3 links)
