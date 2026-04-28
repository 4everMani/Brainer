---
id: 03-poly-a1b2
tags: [agentic-ai, 03_Architecture, regression]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Polynomial Regression

> [!ABSTRACT]
> Polynomial Regression is a method for fitting nonlinear data by adding powers of original features as new features and then training a linear model on this extended feature set. This allows the model to learn the complex, curved relationships in the data.

## 🧠 Intuition First
- Imagine you're trying to draw a line through a set of points that form a "U" shape (a parabola). A straight line will never work. But if you take your "X" values and also use "X squared" as a feature, you can now draw that curve perfectly using a "linear" equation of those two features.

## 🎯 Why This Matters
- Problem it solves: Enables linear models to capture nonlinear relationships without changing the underlying training algorithms.
- Real-world usage: Predicting growth curves, physical trajectories, or any relationship that isn't a straight line.

## 🧩 Glossary
- [[Polynomial Regression]] : A type of regression where the relationship between the independent variable $x$ and the dependent variable $y$ is modeled as an $n^{th}$ degree polynomial.
- [[Quadratic Equation]] : A second-degree polynomial of the form $ax^2 + bx + c$.
- [[Combinatorial Explosion]] : The rapid increase in the number of features when using a high-degree polynomial with multiple input features.

## ⚙️ Mechanics (First Principles)
### The Process:
1. **Transform Data:** Add the square (or cube, etc.) of each feature as a new feature.
    - Example: For one feature $x$, create a new feature $x^2$.
2. **Train Linear Model:** Fit a standard linear regression model on the new dataset containing both $x$ and $x^2$.
3. **Capture Interactions:** With multiple features (e.g., $a$ and $b$), polynomial regression can also find relationships like $a \times b$ (combinations).

## 📐 Mathematical Foundations
- **Degrees of Freedom Equation:**
  PolynomialFeatures(degree=d) transforms an array of $n$ features into an array of:
  $\frac{(n + d)!}{d!n!}$ features.
- *Warning:* For $n=10$ and $d=3$, this results in 286 features!

## 💻 Implementation
- Using Scikit-Learn's `PolynomialFeatures`:
```python
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression

# Add x^2 to the features
poly_features = PolynomialFeatures(degree=2, include_bias=False)
X_poly = poly_features.fit_transform(X)

# Train a linear model on the extended set
lin_reg = LinearRegression()
lin_reg.fit(X_poly, y)
```

## 🧪 Experiments
1. **Degree Comparison:** Train a 1st degree (linear), 2nd degree (quadratic), and 300th degree polynomial model on the same quadratic dataset. Observe how the 300th degree model wiggles around (overfitting).

## ⚠️ Constraints & Pitfalls
- **Combinatorial Explosion:** High-degree polynomials on many features will quickly exceed your memory and computation capacity.
- **Overfitting:** A high-degree model is much more likely to "memorize" the noise in your training set than generalize to new data.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Linear_Regression_Mechanics]]
- Used in → [[Learning_Curves]]
- Related to → [[Main_Challenges_of_Machine_Learning]]
---
(MINIMUM 3 links)
