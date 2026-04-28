---
id: 06-tfva-a1b2
tags: [agentic-ai, 06_Implementation, libraries]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# TensorFlow Tensors and Variables

> [!ABSTRACT]
> Tensors are the fundamental data structures of TensorFlow, similar to NumPy arrays but with GPU acceleration and support for automatic differentiation. While standard tensors are immutable, `tf.Variable` objects provide mutable state for storing model parameters that are updated during training.

## 🧠 Intuition First
- **Tensor:** Imagine a printed photograph. You can look at it, measure the colors (data), and even transform it (e.g., crop), but you can't change the pixels on the original paper.
- **Variable:** Imagine a chalkboard. You can write numbers on it (initialization), and then come back later and erase or change them (updates). This is where the model stores its weights so it can "learn" by changing them.

## 🎯 Why This Matters
- Problem it solves: Provides the efficient, offloadable data structures needed for the millions of mathematical operations involved in training deep neural networks.
- Real-world usage: Implementing any custom logic or low-level algorithm that isn't provided by high-level Keras layers.

## 🧩 Glossary
- [[tf.Tensor]] : An immutable multidimensional array.
- [[tf.Variable]] : A mutable tensor used to store parameters (weights/biases) that are modified by backpropagation.
- [[Dtype]] : The data type of the tensor elements (e.g., `tf.float32`).
- [[Broadcasting]] : Automatically expanding the shape of smaller tensors during operations (like NumPy).

## ⚙️ Mechanics (First Principles)
### Standard Tensors:
- Created via `tf.constant()`.
- Operations: `tf.add()`, `tf.matmul()` (or `@`), `tf.transpose()`.
- **Interoperability:** Convert to NumPy using `.numpy()` or `np.array()`. Tensors and NumPy arrays can often be mixed in operations.

### Variables:
- Created via `tf.Variable()`.
- Updated via `.assign()`, `.assign_add()`, or `.assign_sub()`.
- **Tracking:** Keras automatically tracks `tf.Variable` attributes in layers and models for saving and optimization.

## 📐 Mathematical Foundations
- **Precision:** TensorFlow uses `float32` by default for performance. NumPy uses `float64`. Be careful with type mismatches.

## 💻 Implementation
- Creating and Updating state:
```python
import tensorflow as tf

# Immutable Tensor
t = tf.constant([[1., 2.], [3., 4.]])

# Mutable Variable
v = tf.Variable([[1., 2.], [3., 4.]])
v.assign(2 * v)           # multiply by 2
v[0, 1].assign(42)        # change one element
v.assign_add([[1, 1], [1, 1]]) # increment
```

## 🧪 Experiments
1. **The Immutability Test:** Try to use item assignment (e.g., `t[0,0] = 5`) on a `tf.constant`. Observe the `TypeError`. Then do the same with a `tf.Variable` using `.assign()`.
2. **Speed Benchmarking:** Measure the time to add two $5000 \times 5000$ matrices in NumPy vs. TensorFlow on a GPU.

## ⚠️ Constraints & Pitfalls
- **Type Sensitivity:** TensorFlow does NOT perform automatic type conversion (e.g., adding `int32` to `float32` will raise an error). Use `tf.cast()` explicitly.
- **Copying:** `tf.transpose()` creates a copy of the data, unlike NumPy's `.T` which is a view.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[TensorFlow_Core_Basics]]
- Used in → [[Custom_Layers_and_Models_Keras]]
- Related to → [[Automatic_Differentiation_with_GradientTape]]
---
(MINIMUM 3 links)
