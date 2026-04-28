---
id: 06-clme-c1d2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Custom Loss and Metrics Keras

> [!ABSTRACT]
> Keras allows for the creation of custom loss functions and metrics to handle specialized objectives. For stateless objectives, simple functions suffice; for objectives with hyperparameters or state (streaming metrics), subclassing `tf.keras.losses.Loss` or `tf.keras.metrics.Metric` is required to ensure correct serialization and accumulation.

## 🧠 Intuition First
- Imagine you're judging a competition. 
- **Simple Loss Function:** You have a fixed rulebook (e.g., "deduct 1 point for every mistake"). You just apply the rule to every performance.
- **Stateful Metric:** You're a sports commentator tracking a player's average points per game. You can't just look at the last game; you have to remember the total points and the total games played so far (state) to give the current average.

## 🎯 Why This Matters
- Problem it solves: Enables the training and evaluation of models for non-standard tasks (e.g., Huber loss for outlier robustness) and ensures that these custom settings are saved and loaded correctly.
- Real-world usage: Implementing a custom "Profit" metric for financial models or a specialized "Intersection over Union" (IoU) loss for object detection.

## 🧩 Glossary
- [[Huber Loss]] : A loss function that is quadratic for small errors and linear for large errors, making it less sensitive to outliers than MSE.
- [[Streaming Metric]] : A metric that maintains a state (e.g., running sum and count) across multiple batches in an epoch (also called **Stateful Metric**).
- [[get_config]] : A method used to return a dictionary of hyperparameters for model serialization.

## ⚙️ Mechanics (First Principles)
### Custom Loss (Subclassing):
1. **`__init__`**: Define hyperparameters (e.g., `threshold`).
2. **`call(y_true, y_pred)`**: Compute the loss for each instance in the batch.
3. **`get_config`**: Return dictionary of hyperparameters for saving.

### Custom Metric (Subclassing):
1. **`__init__`**: Create variables using `self.add_weight()` to track the state.
2. **`update_state(y_true, y_pred)`**: Update the running variables based on the new batch.
3. **`result()`**: Calculate and return the final value (e.g., `total / count`).

## 📐 Mathematical Foundations
- **Huber Loss Definition:**
  $L_\delta(y, f(x)) = \begin{cases} \frac{1}{2}(y - f(x))^2 & |y - f(x)| \leq \delta \\ \delta(|y - f(x)| - \frac{1}{2}\delta) & \text{otherwise} \end{cases}$

## 💻 Implementation
- Creating a Custom Huber Loss class:
```python
class HuberLoss(tf.keras.losses.Loss):
    def __init__(self, threshold=1.0, **kwargs):
        self.threshold = threshold
        super().__init__(**kwargs)
    def call(self, y_true, y_pred):
        error = y_true - y_pred
        is_small_error = tf.abs(error) < self.threshold
        squared_loss = tf.square(error) / 2
        linear_loss = self.threshold * tf.abs(error) - self.threshold**2 / 2
        return tf.where(is_small_error, squared_loss, linear_loss)
    def get_config(self):
        base_config = super().get_config()
        return {**base_config, "threshold": self.threshold}
```

## 🧪 Experiments
1. **The Average Test:** Calculate a precision metric for two batches. Batch 1: 4/5 correct (80%). Batch 2: 0/3 correct (0%). Show that the mean of the means (40%) differs from the true precision (4/8 = 50%). Verify that `tf.keras.metrics.Precision` gives the correct 50%.

## ⚠️ Constraints & Pitfalls
- **Load Mismatch:** When loading a model with custom objects, you **must** provide the `custom_objects` dictionary to `load_model()`.
- **Differentiability:** Loss functions MUST be differentiable for Gradient Descent to work. Metrics do not have this requirement.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Neural_Network_Regression_and_Classification]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Keras_Model_Persistence]]
---
(MINIMUM 3 links)
