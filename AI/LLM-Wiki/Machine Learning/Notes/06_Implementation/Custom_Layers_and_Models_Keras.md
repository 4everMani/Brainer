---
id: 06-clay-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Custom Layers and Models Keras

> [!ABSTRACT]
> Keras provides a hierarchical framework for building custom architectures. While `tf.keras.layers.Layer` is the base class for modular components (stateless or with internal weights), `tf.keras.Model` adds high-level features like `fit()` and `evaluate()`. Models can also include internal losses (e.g., reconstruction loss) via the `add_loss()` method.

## 🧠 Intuition First
- **Layer:** Imagine a single component in a machine, like a gear. It has a specific job and might have internal settings (weights), but it can't run the whole machine by itself.
- **Model:** This is the machine itself. It's built by connecting gears (layers). It has a start button (fit), an output display (predict), and can be saved and transported as a single unit.

## 🎯 Why This Matters
- Problem it solves: Enables researchers and engineers to implement state-of-the-art architectures found in papers that aren't yet available as standard library components.
- Real-world usage: Building Residual blocks for CNNs, custom Attention mechanisms, or Variational Autoencoders (VAEs).

## 🧩 Glossary
- [[Lambda Layer]] : A wrapper for simple, stateless functions (e.g., `tf.exp`) to treat them as layers.
- [[build() method]] : A layer method used to initialize weights once the input shape is known.
- [[add_loss()]] : A model/layer method used to add a custom penalty based on model internals (e.g., hidden activations).
- [[Residual Block]] : A common custom architecture that adds a layer's input directly to its output (skip connection).

## ⚙️ Mechanics (First Principles)
### Custom Layer Workflow:
1. **`__init__`**: Save hyperparameters.
2. **`build(input_shape)`**: Create weights using `self.add_weight()`.
3. **`call(X)`**: Implement the mathematical transformation.
4. **`get_config`**: Return settings for serialization.

### Internal Losses:
- Losses don't always have to depend on labels ($y_{true}$). 
- You can compute a loss based on any internal tensor (e.g., a "reconstruction error" in an autoencoder) and pass it to `self.add_loss()`. Keras will automatically add this to the total loss during training.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Creating a stateful Custom Layer:
```python
class MyDense(tf.keras.layers.Layer):
    def __init__(self, units, activation=None, **kwargs):
        super().__init__(**kwargs)
        self.units = units
        self.activation = tf.keras.activations.get(activation)
    def build(self, batch_input_shape):
        self.kernel = self.add_weight(name="kernel", 
                                      shape=[batch_input_shape[-1], self.units],
                                      initializer="glorot_normal")
        self.bias = self.add_weight(name="bias", shape=[self.units], 
                                    initializer="zeros")
        super().build(batch_input_shape) # tell Keras it's done
    def call(self, X):
        return self.activation(X @ self.kernel + self.bias)
```

## 🧪 Experiments
1. **The Shape Inference:** Create a `MyDense` layer. Call it on a tensor of shape `(None, 5)`. Check `layer.kernel.shape` to see if the `build()` method correctly inferred that it needed 5 input connections.

## ⚠️ Constraints & Pitfalls
- **Composition over Inheritance:** Usually better to define a `Model` that contains `Layers` rather than a `Layer` that contains `Models`, although both are technically possible.
- **Serialization:** If you forget `get_config`, you won't be able to reload the model from disk.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Keras_Subclassing_API]]
- Used in → [[Neural_Network_Regression_and_Classification]]
- Related to → [[Keras_Model_Persistence]]
---
(MINIMUM 3 links)
