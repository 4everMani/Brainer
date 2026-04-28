---
id: 03-bagp-a1b2
tags: [agentic-ai, 03_Architecture, ensemble-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Bagging and Pasting

> [!ABSTRACT]
> Bagging (Bootstrap Aggregating) and Pasting are ensemble methods where multiple models of the same type are trained on different random subsets of the training data. Bagging samples with replacement, while Pasting samples without replacement. The final prediction is an aggregation of all models, typically reducing variance without increasing bias.

## 🧠 Intuition First
- Imagine you have a classroom of students learning to identify birds. 
- **Pasting:** You give each student a different, unique set of 10 bird cards. 
- **Bagging:** You have a box of 100 bird cards. Each student picks 10 cards at random, writes them down, and puts them back (replacement). One student might pick the same "Eagle" card twice, while another student never sees it. 
- In both cases, you average all the students' guesses to get the final answer.

## 🎯 Why This Matters
- Problem it solves: Reduces the high variance of individual models (like Decision Trees) and allows for parallel training across multiple CPU cores.
- Real-world usage: Forms the core mechanism for Random Forests.

## 🧩 Glossary
- [[Bagging]] : Bootstrap Aggregating. Sampling with replacement.
- [[Pasting]] : Sampling without replacement.
- [[Bootstrap]] : A statistical method for sampling with replacement.
- [[Aggregation]] : Combining individual predictions via the statistical mode (classification) or average (regression).

## ⚙️ Mechanics (First Principles)
### The Process:
1. **Sampling:** Create $N$ random subsets of the training data.
2. **Parallel Training:** Train $N$ independent models (one per subset) in parallel.
3. **Prediction:** For a new instance, get predictions from all $N$ models.
4. **Final Vote:** 
    - **Classification:** Use the most frequent class (mode).
    - **Regression:** Use the average of all predictions.

### Bias-Variance Impact:
- Each individual model has a higher bias (trained on less data), but the aggregation step reduces both bias and variance. The net result is a model with similar bias to the original but significantly lower variance.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.ensemble import BaggingClassifier
from sklearn.tree import DecisionTreeClassifier

# bagging (bootstrap=True)
# pasting (bootstrap=False)
bag_clf = BaggingClassifier(
    DecisionTreeClassifier(), n_estimators=500,
    max_samples=100, n_jobs=-1, bootstrap=True
)
bag_clf.fit(X_train, y_train)
```

## 🧪 Experiments
1. **Boundary Smoothness:** Plot the decision boundary of a single Decision Tree vs a Bagging ensemble of 500 trees. Observe how the ensemble boundary is much smoother and more generalized.

## ⚠️ Constraints & Pitfalls
- **Sampling Size:** If `max_samples` is too small, each model will be too weak. If too large, the models will be too similar (highly correlated), and the ensemble won't reduce variance as much.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Decision_Trees_Basics]]
- Used in → [[Out_of_Bag_Evaluation]]
- Related to → [[Ensemble_Modeling]]
---
(MINIMUM 3 links)
