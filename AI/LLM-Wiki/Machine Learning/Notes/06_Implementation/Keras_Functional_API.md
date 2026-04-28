---
id: 06-kfun-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Keras Functional API

> [!ABSTRACT]
> The Keras Functional API provides a way to build neural networks with complex topologies, such as those with multiple inputs, multiple outputs, or non-sequential connections (e.g., Wide & Deep networks). Layers are treated like functions that accept and return symbolic tensors.

## 🧠 Intuition First
- Imagine you're building a complex transportation network instead of a simple straight road. You have highway sections (deep path) for long-distance travel and surface streets (wide path) for local rules. Some cargo (features) might take only the highway, some only the streets, and some might switch between both. The **Functional API** is the blueprint that tells you exactly where every road starts, ends, and intersects.

## 🎯 Why This Matters
- Problem it solves: Handles complex data relationships that a simple linear stack of layers cannot capture, such as combining raw features with high-level learned representations.
- Real-world usage: Building object detectors (location + classification), recommendation systems (user ID + product ID), and multi-task learning models.

## 🧩 Glossary
- [[Functional API]] : A way to build models by calling layers like functions.
- [[Wide & Deep Model]] : An architecture that connects part of the input directly to the output while also passing it through a deep stack of hidden layers.
- [[Concatenate Layer]] : A layer that joins multiple input tensors along a specific axis.
- [[Symbolic Input]] : An `Input` object that specifies the shape and type of data but holds no actual values.

## ⚙️ Mechanics (First Principles)
### The Process:
1. **Define Inputs:** Create one or more `Input` objects.
2. **Call Layers:** Pass the input tensors through layers (e.g., `Dense`, `Normalization`) just like calling a Python function.
3. **Connect/Merge:** Use layers like `Concatenate` or `Add` to combine different branches of the network.
4. **Instantiate Model:** Create a `tf.keras.Model` by specifying the `inputs` and `outputs` tensors.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Building a Wide & Deep model with multiple inputs:
```python
input_wide = tf.keras.layers.Input(shape=[5], name="wide")
input_deep = tf.keras.layers.Input(shape=[6], name="deep")

norm_wide = tf.keras.layers.Normalization()(input_wide)
norm_deep = tf.keras.layers.Normalization()(input_deep)

hidden1 = tf.keras.layers.Dense(30, activation="relu")(norm_deep)
hidden2 = tf.keras.layers.Dense(30, activation="relu")(hidden1)

concat = tf.keras.layers.concatenate([norm_wide, hidden2])
output = tf.keras.layers.Dense(1, name="output")(concat)

model = tf.keras.Model(inputs=[input_wide, input_deep], outputs=[output])
```

## 🧪 Experiments
1. **The Branch Test:** Build a model with two different branches: one using ReLU and one using Tanh. Concatenate their outputs and observe if the combined model learns faster than either branch alone on a multimodal dataset.

## ⚠️ Constraints & Pitfalls
- **Input Order:** When fitting a model with multiple inputs, ensure that the data matrices are passed in the exact same order as defined in the `Model(inputs=[...])` call, or use a named dictionary.
- **Reference Management:** Unlike the Sequential API, you must keep track of each layer's output tensor to connect it to the next step.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Keras_Sequential_API]]
- Used in → [[Neural_Network_Regression_and_Classification]]
- Related to → [[Keras_Subclassing_API]]
---
(MINIMUM 3 links)
