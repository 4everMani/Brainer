---
id: 06-ctlo-a1b2
tags: [agentic-ai, 06_Implementation, tensorflow]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Custom Training Loops TensorFlow

> [!ABSTRACT]
> While Keras `fit()` is sufficient for 95% of cases, custom training loops provide the ultimate flexibility needed for complex research or production requirements, such as using multiple optimizers (e.g., Wide & Deep) or applying unique gradient constraints.

## 🧠 Intuition First
- Imagine you're using an automatic car (Keras `fit()`). It handles the gears and acceleration perfectly for most trips. A **Custom Training Loop** is like driving a manual car with a customized engine. You control every shift, every brake, and exactly how much fuel goes in. It's more work and easier to stall, but it's the only way to win a race that requires a specialized driving style.

## 🎯 Why This Matters
- Problem it solves: Allows implementation of architectures where standard `fit()` logic fails, such as GANs or models with auxiliary losses that depend on non-standard signals.
- Real-world usage: Building state-of-the-art research models or fine-tuning performance on highly specialized hardware.

## 🧩 Glossary
- [[Step Function]] : A function that processes a single mini-batch and returns the loss (often decorated with `@tf.function`).
- [[Training Loop]] : The outer loop (epochs) and inner loop (batches) that orchestrate the training process.
- [[Optimizer Step]] : The call to `optimizer.apply_gradients()` that actually updates the model weights.

## ⚙️ Mechanics (First Principles)
### The Manual Workflow:
1. **Iterate Epochs:** Loop over the desired number of training passes.
2. **Iterate Batches:** Sample a mini-batch from the dataset.
3. **Open GradientTape:** Record operations for autodiff.
4. **Compute Loss:** Calculate the model output and the error compared to labels.
5. **Compute Gradients:** Use `tape.gradient()` to find the partial derivatives.
6. **Apply Gradients:** Use `optimizer.apply_gradients()` to update weights.
7. **Track Metrics:** Update mean loss and accuracy metrics manually at each step.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- A simplified custom training step:
```python
@tf.function
def train_step(X_batch, y_batch):
    with tf.GradientTape() as tape:
        y_pred = model(X_batch)
        main_loss = tf.reduce_mean(loss_fn(y_batch, y_pred))
        loss = tf.add_n([main_loss] + model.losses) # include internal losses
    gradients = tape.gradient(loss, model.trainable_variables)
    optimizer.apply_gradients(zip(gradients, model.trainable_variables))
    train_acc_metric.update_state(y_batch, y_pred)
    return loss
```

## 🧪 Experiments
1. **The optimizer split:** Modify the training step to use two different optimizers: one for the first 3 layers and another for the rest of the model. Observe the loss curve.

## ⚠️ Constraints & Pitfalls
- **Complexity:** Harder to debug and more boilerplate code compared to high-level APIs.
- **Metric Management:** You must remember to `reset_states()` for metrics at the end of every epoch, or they will show a cumulative average since the beginning of training.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Automatic_Differentiation_with_GradientTape]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Keras_Model_Persistence]]
---
(MINIMUM 3 links)
