---
id: 04-lcur-a1b2
tags: [agentic-ai, 04_Training, model-evaluation]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Learning Curves

> [!ABSTRACT]
> Learning curves are plots of a model's performance on the training and validation sets as a function of the training set size (or training iteration). They are essential for diagnosing whether a model is underfitting or overfitting the data.

## 🧠 Intuition First
- Imagine you're learning a new language. 
- **Underfitting:** If you only learn 5 words, you'll be equally bad at talking to yourself (training) and talking to a native speaker (validation), no matter how much you practice those same 5 words.
- **Overfitting:** If you memorize 1,000 specific sentences but don't learn the grammar, you'll be perfect at those sentences (training) but fail completely when a native speaker says something slightly different (validation).

## 🎯 Why This Matters
- Problem it solves: Tells you if you need a more complex model, better features, or just more training data to improve performance.
- Real-world usage: Deciding whether to spend money gathering more data or time engineering better features.

## 🧩 Glossary
- [[Learning Curve]] : A plot of training error vs. validation error as the training set size increases.
- [[Generalization Gap]] : The distance between the training error curve and the validation error curve.
- [[learning_curve()]] : A Scikit-Learn function that automates the generation of these plots.

## ⚙️ Mechanics (First Principles)
### Diagnosing Underfitting:
- Both curves plateau at a high error level.
- Adding more training data will **not** help; you need a more complex model or better features.
### Diagnosing Overfitting:
- There is a large gap between the curves (low training error, high validation error).
- Adding more training data **will** help close the gap and improve generalization.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Generating curves in Scikit-Learn:
```python
from sklearn.model_selection import learning_curve

train_sizes, train_scores, valid_scores = learning_curve(
    LinearRegression(), X, y, train_sizes=np.linspace(0.01, 1.0, 40), cv=5,
    scoring="neg_root_mean_squared_error")

# RMSE is the negative of the scores
train_errors = -train_scores.mean(axis=1)
valid_errors = -valid_scores.mean(axis=1)
```

## 🧪 Experiments
1. **The Gap Test:** Train a 10th degree polynomial model on a small dataset (~20 instances). Observe the massive gap between the training and validation curves. Then, increase the dataset to 1,000 instances and watch the gap shrink.

## ⚠️ Constraints & Pitfalls
- **Negative Scores:** Scikit-Learn uses "greater is better" for scoring, so error metrics like RMSE are returned as negative numbers. Always multiply by -1 before plotting.
- **Computational Cost:** Generating learning curves requires training the model dozens of times on different subsets of the data.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Main_Challenges_of_Machine_Learning]]
- Used in → [[Bias_And_Variance]]
- Related to → [[Polynomial_Regression]]
---
(MINIMUM 3 links)
