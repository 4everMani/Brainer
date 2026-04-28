---
id: 01-inst-a1b2
tags: [agentic-ai, 01_Foundations, ml-generalization]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Instance-based vs Model-based Learning

> [!ABSTRACT]
> Machine learning systems generalize from training examples to new instances using two main approaches: comparing new data to known examples (instance-based) or detecting patterns in training data to build a predictive model (model-based).

## 🧠 Intuition First
- **Instance-based Learning:** Like learning by heart. If you see a new email, you compare it to all the emails you've ever labeled. If it's very similar to a "spam" email, you flag it. No underlying "rules" are created—just direct comparison.
- **Model-based Learning:** Like learning a rule. You look at many spam emails and notice they often contain the word "free." You create a rule (a model) that says "if email contains 'free', then it's spam." You no longer need the original emails to make a prediction.

## 🎯 Why This Matters
- Problem it solves: Defines how a system generalizes its knowledge to unseen data.
- Real-world usage: K-Nearest Neighbors (instance-based) vs. Linear Regression (model-based).

## 🧩 Glossary
- [[Generalization]] : The ability of a model to perform well on new, unseen instances.
- [[Similarity Measure]] : A metric (like word count overlap) used in instance-based learning to compare new data to training instances.
- [[Model Parameter]] : The tunable parts of a model (e.g., $\theta_0, \theta_1$) found during training.
- [[Cost Function]] : A measure of how "bad" a model's predictions are compared to the training data.

## ⚙️ Mechanics (First Principles)
### Instance-based Learning
- **Process:** Stores all training instances.
- **Prediction:** Compares the new instance to the stored training instances using a similarity measure.
- **Example:** K-Nearest Neighbors.

### Model-based Learning
- **Process:** Build a mathematical model from training instances.
- **Training:** Run an algorithm to find the optimal model parameters that minimize a cost function (or maximize a utility function).
- **Prediction:** Use the trained model (with its fixed parameters) to predict new instances.
- **Example:** Linear Regression.

## 📐 Mathematical Foundations
- **Simple Linear Model:**
  $y = \theta_0 + \theta_1 \cdot x$
- **Training Objective:** Minimize the cost function (e.g., Mean Squared Error):
  $MSE(\theta) = \text{Minimize distance between predictions and actual values}$

## 💻 Implementation
- Conceptual example of Model-based prediction:
```python
# Linear Model: Life satisfaction = 3.75 + 6.78e-5 * GDP
def predict_life_satisfaction(gdp):
    theta0 = 3.75
    theta1 = 6.78e-5
    return theta0 + theta1 * gdp

# Prediction for Cyprus
print(predict_life_satisfaction(37655)) # Output: ~6.30
```

## 🧪 Experiments
1. **Model Complexity:** Compare a linear model vs. a high-degree polynomial model on the same dataset and observe which one generalizes better to new points.
2. **K-Value Tuning:** In an instance-based system like KNN, try varying the number of neighbors (k) and observe how the decision boundary changes.

## ⚠️ Constraints & Pitfalls
- **Memory Cost:** Instance-based learning can be memory-intensive as it needs to keep all training data.
- **Model Selection:** In model-based learning, choosing the wrong "type" of model (e.g., a line for a curve) will result in poor performance.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[Linear_Regression]]
- Related to → [[Batch_vs_Online_Learning]]
