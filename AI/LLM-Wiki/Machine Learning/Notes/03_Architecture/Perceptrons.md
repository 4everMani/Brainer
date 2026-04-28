---
id: 03-perc-a1b2
tags: [agentic-ai, 03_Architecture, neural-networks]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Perceptrons

> [!ABSTRACT]
> The Perceptron is one of the simplest artificial neural network (ANN) architectures. It is composed of one or more Threshold Logic Units (TLUs) that compute a weighted sum of inputs and apply a step function to produce a binary classification.

## 🧠 Intuition First
- Imagine a light switch that only turns on if multiple people press it at the same time. Some people have stronger fingers (higher weights) than others. The switch has a "threshold"—if the combined force of the fingers is high enough, the light flips on (Step Function). A Perceptron is a mathematical version of this switch.

## 🎯 Why This Matters
- Problem it solves: Provides a foundational building block for complex neural networks and enables simple linear binary classification.
- Real-world usage: Linear classification tasks where speed is more important than high accuracy or probability estimates.

## 🧩 Glossary
- [[TLU]] : Threshold Logic Unit. An artificial neuron that computes a weighted sum and applies a step function.
- [[Heaviside Step Function]] : A function that outputs 0 for negative inputs and 1 for positive inputs.
- [[Perceptron Learning Rule]] : A variant of Hebb's rule that reinforces connections contributing to correct predictions.
- [[Linearly Separable]] : A dataset where two classes can be perfectly separated by a straight line (or hyperplane).

## ⚙️ Mechanics (First Principles)
### TLU Computation:
- $z = w_1 x_1 + w_2 x_2 + \dots + w_n x_n + b = \mathbf{w}^T \mathbf{x} + b$
- Output: $h(\mathbf{x}) = step(z)$

### Training Rule (Weight Update):
- $w_{i,j}^{(next step)} = w_{i,j} + \eta(y_j - \hat{y}_j)x_i$
- $\eta$ is the learning rate.
- $y_j - \hat{y}_j$ is the prediction error.

## 📐 Mathematical Foundations
- **Convergence Theorem:** If the training instances are linearly separable, the Perceptron algorithm is guaranteed to find a solution in a finite number of steps.

## 💻 Implementation
- Using Scikit-Learn:
```python
from sklearn.linear_model import Perceptron

per_clf = Perceptron()
per_clf.fit(X, y)
y_pred = per_clf.predict([[2, 0.5]])
```

## 🧪 Experiments
1. **The XOR Failure:** Try to train a Perceptron to solve the XOR problem (exclusive OR). Observe that it fails because XOR is not linearly separable.

## ⚠️ Constraints & Pitfalls
- **Linear Boundaries:** Perceptrons can only learn linear decision boundaries.
- **No Probabilities:** Unlike Logistic Regression, standard Perceptrons do not output a probability score, only a hard class label.
- **No Regularization:** Standard Perceptrons don't use regularization and stop training as soon as the training set is correct, which can lead to poor generalization.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[Multilayer_Perceptrons_and_DNNs]]
- Related to → [[Logistic_Regression_Mechanics]]
---
(MINIMUM 3 links)
