---
id: 04-wini-a1b2
tags: [agentic-ai, 04_Training, neural-networks]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Weight Initialization Strategies

> [!ABSTRACT]
> To ensure stable gradients, signal variance must be preserved as it flows forward through the layers and backward through the gradients. Specialized initialization schemes like Glorot (Xavier), He (Kaiming), and LeCun scale the initial weight variance based on the number of inputs and outputs of the layer (fan-in and fan-out).

## 🧠 Intuition First
- Imagine you're building a network of speakers and microphones. If the first speaker is too loud, the next microphone will clip (saturate). If it's too quiet, the signal will be lost in noise (vanishing). **Initialization** is like setting the master gain for each speaker before the concert starts, ensuring that the volume stays consistent from the first stage to the last.

## 🎯 Why This Matters
- Problem it solves: Prevents signal saturation and vanishing gradients during the early stages of training, allowing deep networks to converge much faster.
- Real-world usage: Standard practice for initializing all types of layers in deep learning frameworks.

## 🧩 Glossary
- [[Fan-in]] : The number of input connections to a layer.
- [[Fan-out]] : The number of output connections from a layer.
- [[Glorot Initialization]] : Scales weights based on $\text{fan}_{avg}$. Best for Sigmoid, Tanh, and Softmax.
- [[He Initialization]] : Scales weights based on $\text{fan}_{in}$. Best for ReLU and its variants.
- [[LeCun Initialization]] : Scales weights based on $\text{fan}_{in}$. Best for SELU.

## ⚙️ Mechanics (First Principles)
### The Rule of Variance:
- For signal to flow properly, the variance of layer outputs must equal the variance of its inputs.
- For gradients to flow backward properly, the variance of gradients before and after a layer must be equal.

### Scaling Factors (Normal Distribution):
| Initialization | Activation Functions | Variance ($\sigma^2$) |
| :--- | :--- | :--- |
| **Glorot** | None, Tanh, Sigmoid, Softmax | $1 / \text{fan}_{avg}$ |
| **He** | ReLU, Leaky ReLU, ELU, GELU | $2 / \text{fan}_{in}$ |
| **LeCun** | SELU | $1 / \text{fan}_{in}$ |

## 📐 Mathematical Foundations
- **$\text{fan}_{avg}$:** $(\text{fan}_{in} + \text{fan}_{out}) / 2$.
- **He Uniform Limit:** $r = \sqrt{3 \sigma^2} = \sqrt{6 / \text{fan}_{in}}$.

## 💻 Implementation
- Setting He initialization in Keras:
```python
import tensorflow as tf

layer = tf.keras.layers.Dense(50, activation="relu",
                              kernel_initializer="he_normal")
```

## 🧪 Experiments
1. **The Convergence Race:** Train a 5-layer network on MNIST using standard normal initialization vs. He initialization (with ReLU). Compare the number of epochs needed to reach 90% accuracy.

## ⚠️ Constraints & Pitfalls
- **Activation Matching:** Using the wrong initialization for an activation (e.g., Glorot for ReLU) can significantly slow down convergence or cause saturation.
- **Keras Defaults:** By default, Keras uses Glorot initialization with a uniform distribution. Remember to switch if using ReLU.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Vanishing_and_Exploding_Gradients]]
- Used in → [[Multilayer_Perceptrons_and_DNNs]]
- Related to → [[Neural_Network_Activation_Functions]]
---
(MINIMUM 3 links)
