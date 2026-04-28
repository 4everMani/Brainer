---
id: 03-bnrm-a1b2
tags: [agentic-ai, 03_Architecture, neural-networks]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Batch Normalization

> [!ABSTRACT]
> Batch Normalization (BN) is a technique to stabilize training by zero-centering and rescaling inputs to each layer. It learns the optimal scale and mean for each layer's activations during training, effectively mitigating the vanishing gradients problem and allowing for much larger learning rates.

## 🧠 Intuition First
- Imagine a relay race where runners pass a baton. If each runner is a different height and speed, the handoff (signal) is unstable. **Batch Normalization** is like giving every runner a standard uniform and training them to stay in the exact center of their lane. Even if the world (input data) is messy, the inner workings of the race stay predictable and stable.

## 🎯 Why This Matters
- Problem it solves: Eliminates the vanishing/exploding gradients problem in very deep networks and makes models less sensitive to the specific weight initialization used.
- Real-world usage: Universal standard in deep convolutional neural networks (CNNs) and many other deep architectures.

## 🧩 Glossary
- [[BN Layer]] : A layer that performs centering and rescaling, typically placed before or after the activation function.
- [[Trainable Parameters (BN)]] : $\gamma$ (scale) and $\beta$ (offset) learned by backpropagation.
- [[Non-trainable Parameters (BN)]] : $\mu$ (mean) and $\sigma$ (standard deviation) tracked as moving averages during training.
- [[Momentum (BN)]] : A hyperparameter (usually ~0.99) that determines how fast the BN layer updates its moving averages.

## ⚙️ Mechanics (First Principles)
### The 4 Operations:
1. **Centering:** Subtract the batch mean $\mu_B$ from the input.
2. **Normalizing:** Divide by the batch standard deviation $\sigma_B$.
3. **Scaling:** Multiply by a learned parameter $\gamma$.
4. **Shifting:** Add a learned parameter $\beta$.

### During Inference:
- The individual batch statistics are no longer available. Instead, the layer uses the **moving averages** of $\mu$ and $\sigma$ it tracked during training to normalize new instances.

## 📐 Mathematical Foundations
- **BN Equation:**
  $\mathbf{y}^{(i)} = \gamma \otimes \frac{\mathbf{x}^{(i)} - \mu_B}{\sqrt{\sigma_B^2 + \epsilon}} + \beta$
  - $\epsilon$ is a tiny smoothing term to avoid division by zero.

## 💻 Implementation
- Standard BN in Keras (after activation):
```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(300, activation="relu", kernel_initializer="he_normal"),
    tf.keras.layers.BatchNormalization(),
    tf.keras.layers.Dense(100, activation="relu", kernel_initializer="he_normal"),
    tf.keras.layers.BatchNormalization(),
    # ...
])
```

## 🧪 Experiments
1. **The Learning Rate Test:** Train two deep networks: one with BN and one without. Observe that the BN network can converge with a 10x higher learning rate without diverging.

## ⚠️ Constraints & Pitfalls
- **Prediction Latency:** BN adds extra computations, slowing down inference. (Can be fixed by "fusing" layers after training).
- **Batch Size Sensitivity:** BN relies on batch statistics; if the batch size is too small (e.g., 1), the mean and std will be highly unstable.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> **BN Position:** There is ongoing debate about whether BN should be placed *before* or *after* the activation function. The original paper suggested before, but many modern architectures put it after. Scikit-Learn/Keras supports both.

## 🔗 Connections
- Builds on → [[Vanishing_and_Exploding_Gradients]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Weight_Initialization_Strategies]]
---
(MINIMUM 3 links)
