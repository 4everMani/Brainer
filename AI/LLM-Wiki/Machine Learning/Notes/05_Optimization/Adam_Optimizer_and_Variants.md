---
id: 05-adam-a1b2
tags: [agentic-ai, 05_Optimization, gradient-descent]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Adam Optimizer and Variants

> [!ABSTRACT]
> Adam (Adaptive Moment Estimation) is the most popular optimizer for deep learning. It combines the ideas of momentum (tracking past gradients) and RMSProp (scaling by past squared gradients). Variants like Nadam (Adam + Nesterov) and AdamW (Adam + weight decay) further improve convergence speed and generalization.

## 🧠 Intuition First
- Imagine you're a hiker trying to reach the lowest point in a fog. 
- **Momentum:** You remember your previous direction and speed (velocity). 
- **RMSProp:** You adjust your step size based on how steep the ground has been (scaling). 
- **Adam:** You do both. You have a "memory" of your path and "special shoes" that adapt to the terrain. It's the most reliable way to navigate complex, high-dimensional landscapes.

## 🎯 Why This Matters
- Problem it solves: Automates the tuning of individual learning rates for every parameter, making training faster and less sensitive to the initial global learning rate.
- Real-world usage: The standard "go-to" optimizer for almost all neural network architectures.

## 🧩 Glossary
- [[Adam]] : Adaptive Moment Estimation. Tracks the first moment (mean) and second moment (variance) of gradients.
- [[Nadam]] : Adam with the Nesterov Accelerated Gradient trick. Often converges slightly faster.
- [[AdamW]] : Adam with decoupled weight decay. Essential for correct regularization when using Adam.
- [[Momentum Decay]] : $\beta_1$ (typically 0.9) controls how fast the optimizer "forgets" old gradients.
- [[Scaling Decay]] : $\beta_2$ (typically 0.999) controls how fast the optimizer "forgets" old squared gradients.

## ⚙️ Mechanics (First Principles)
### The 3 Steps:
1. **Estimate Mean:** $\mathbf{m} \leftarrow \beta_1 \mathbf{m} + (1-\beta_1) \nabla J(\boldsymbol{\theta})$.
2. **Estimate Variance:** $\mathbf{s} \leftarrow \beta_2 \mathbf{s} + (1-\beta_2) \nabla J(\boldsymbol{\theta})^2$.
3. **Correct Bias:** $\mathbf{\hat{m}}$ and $\mathbf{\hat{s}}$ are adjusted to account for their initialization at zero.
4. **Update:** $\boldsymbol{\theta} \leftarrow \boldsymbol{\theta} - \eta \mathbf{\hat{m}} / \sqrt{\mathbf{\hat{s}} + \epsilon}$.

## 📐 Mathematical Foundations
- **AdamW Distinction:** In SGD, $\ell_2$ regularization is equivalent to weight decay. In Adam, they are **not** equivalent. Using standard $\ell_2$ with Adam often leads to poor generalization; AdamW fixes this.

## 💻 Implementation
- Using Adam variants in Keras:
```python
import tensorflow as tf

# Standard Adam
opt_adam = tf.keras.optimizers.Adam(learning_rate=0.001)

# Nadam (Faster convergence)
opt_nadam = tf.keras.optimizers.Nadam(learning_rate=0.001)

# AdamW (Better generalization with weight decay)
opt_adamw = tf.keras.optimizers.experimental.AdamW(weight_decay=0.01)
```

## 🧪 Experiments
1. **The Default Race:** Compare Adam, RMSProp, and NAG on a standard MLP training run. Observe that Adam usually reaches a lower loss in fewer epochs with its default settings.

## ⚠️ Constraints & Pitfalls
- **Generalization Risk:** Some research suggests that adaptive optimizers like Adam may lead to solutions that generalize worse than those found by standard SGD + Nesterov on certain datasets.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Advanced_Optimizers_Momentum_Nesterov_AdaGrad]]
- Used in → [[Neural_Network_Hyperparameter_Tuning]]
- Related to → [[Learning_Rate_Scheduling_Techniques]]
---
(MINIMUM 3 links)
