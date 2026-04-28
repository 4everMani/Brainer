---
id: 06-kseq-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Keras Sequential API

> [!ABSTRACT]
> The Keras Sequential API is the simplest way to build neural networks that consist of a single stack of layers connected sequentially. It is ideal for most basic architectures where data flows linearly from input to output.

## 🧠 Intuition First
- Imagine an assembly line. Each station (layer) performs one specific task on the product (data) before passing it to the next station. There are no branches or loops; the product just moves in a straight line from start to finish.

## 🎯 Why This Matters
- Problem it solves: Provides a clean, highly readable, and boilerplate-free way to define and train standard feedforward neural networks.
- Real-world usage: Building image classifiers (MNIST), basic time-series predictors, and simple tabular data models.

## 🧩 Glossary
- [[Sequential Model]] : A linear stack of layers where each layer has exactly one input tensor and one output tensor.
- [[Flatten Layer]] : A preprocessing layer that converts high-dimensional inputs (e.g., 28x28 images) into a 1D array.
- [[Dense Layer]] : A fully connected layer where every neuron is connected to every neuron in the previous layer.
- [[Compile]] : The step where you specify the loss function, optimizer, and metrics for the model.

## ⚙️ Mechanics (First Principles)
### The 3-Step Workflow:
1. **Define Architecture:** Create a `Sequential` object and add layers (Input, Flatten, Dense).
2. **Compile:** Configure training parameters (e.g., `loss="sparse_categorical_crossentropy"`, `optimizer="sgd"`).
3. **Fit:** Train the model on data for a specified number of epochs.

## 📐 Mathematical Foundations
- **Broadcasting:** When adding a bias vector to a weight-input matrix product, Keras automatically adds the bias to every row (instance) in the matrix.

## 💻 Implementation
- Building a classification MLP for Fashion MNIST:
```python
import tensorflow as tf

model = tf.keras.Sequential([
    tf.keras.layers.Input(shape=[28, 28]),
    tf.keras.layers.Flatten(),
    tf.keras.layers.Dense(300, activation="relu"),
    tf.keras.layers.Dense(100, activation="relu"),
    tf.keras.layers.Dense(10, activation="softmax")
])

model.compile(loss="sparse_categorical_crossentropy",
              optimizer="sgd", metrics=["accuracy"])

history = model.fit(X_train, y_train, epochs=30, 
                    validation_data=(X_valid, y_valid))
```

## 🧪 Experiments
1. **The Shape Trap:** Try to add a Dense layer with 10 neurons immediately after an Input layer of shape [28, 28] without a Flatten layer. Observe the error message.

## ⚠️ Constraints & Pitfalls
- **Single Path Only:** Cannot handle models with multiple inputs, multiple outputs, or non-linear layer connections (e.g., skip connections).
- **Static Graph:** Architecture must be defined before training starts.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Multilayer_Perceptrons_and_DNNs]]
- Used in → [[Neural_Network_Regression_and_Classification]]
- Related to → [[Keras_Functional_API]]
---
(MINIMUM 3 links)
