---
id: 03-resn-a1b2
tags: [agentic-ai, 03_Architecture, computer-vision]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# ResNet and Residual Learning

> [!ABSTRACT]
> Residual Networks (ResNet) introduced skip connections (or shortcut connections) to enable the training of extremely deep networks (up to 1,000 layers). Instead of learning the direct mapping $h(\mathbf{x})$, the network learns the residual mapping $f(\mathbf{x}) = h(\mathbf{x}) - \mathbf{x}$, forcing the layers to model the identity function by default.

## 🧠 Intuition First
- Imagine you're drawing a picture based on a series of instructions. 
- **Plain DNN:** Each instruction tells you exactly what to draw from scratch. If instruction #100 is wrong, the whole picture is ruined. 
- **ResNet:** Each instruction only tells you how to *tweak* what's already on the page. If instruction #100 is "do nothing" (identity), you just keep the previous version. This makes it much easier to correct mistakes and pass information safely through many layers.

## 🎯 Why This Matters
- Problem it solves: Eliminates the vanishing gradient problem in very deep networks and accelerates training by providing a "clean" path for signal and gradient flow.
- Real-world usage: The core of most modern deep learning models, including ResNets, ResNeXts, and even Transformers (via residual paths).

## 🧩 Glossary
- [[Skip Connection]] : Adding a layer's input directly to its output.
- [[Residual Unit]] : A small neural network block (e.g., 2 Conv layers) with a skip connection.
- [[Residual Learning]] : Forcing the model to learn the difference between the input and the target function.
- [[Identity Function]] : A function that returns its input unchanged ($f(x) = x$).

## ⚙️ Mechanics (First Principles)
### The Residual Mapping:
- Target function: $h(\mathbf{x})$
- Model learns: $f(\mathbf{x})$
- Output: $f(\mathbf{x}) + \mathbf{x}$
- At initialization, weights are near zero, so $f(\mathbf{x}) \approx 0$ and the output is $\approx \mathbf{x}$. The network effectively starts as a stack of identity functions.

### Handling Shape Changes:
- When a residual unit changes the number of feature maps (depth) or the spatial size (H x W), the skip connection must include a $1 \times 1$ convolutional layer with the appropriate stride and filter count to match the shapes for addition.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Building a ResNet-34 style Residual Unit:
```python
class ResidualUnit(tf.keras.layers.Layer):
    def __init__(self, filters, strides=1, **kwargs):
        super().__init__(**kwargs)
        self.main_layers = [
            tf.keras.layers.Conv2D(filters, 3, strides=strides, padding="same", 
                                   use_bias=False),
            tf.keras.layers.BatchNormalization(),
            tf.keras.layers.Activation("relu"),
            tf.keras.layers.Conv2D(filters, 3, strides=1, padding="same", 
                                   use_bias=False),
            tf.keras.layers.BatchNormalization()
        ]
        self.skip_layers = []
        if strides > 1: # Match shape if stride > 1
            self.skip_layers = [
                tf.keras.layers.Conv2D(filters, 1, strides=strides, 
                                       padding="same", use_bias=False),
                tf.keras.layers.BatchNormalization()
            ]
    def call(self, inputs):
        Z = inputs
        for layer in self.main_layers: Z = layer(Z)
        skip_Z = inputs
        for layer in self.skip_layers: skip_Z = layer(skip_Z)
        return tf.keras.activations.relu(Z + skip_Z)
```

## 🧪 Experiments
1. **The Signal Test:** Train a 100-layer "Plain" network vs. a 100-layer ResNet. Observe that the Plain network's accuracy often *decreases* as layers are added, while the ResNet continues to improve.

## ⚠️ Constraints & Pitfalls
- **Addition over Concatenation:** Skip connections in ResNet use element-wise **addition**, which requires identical shapes. This differs from DenseNet, which uses concatenation.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Batch_Normalization]]
- Used in → [[Evolution_of_CNN_Architectures]]
- Related to → [[Xception_and_Separable_Convolutions]]
---
(MINIMUM 3 links)
