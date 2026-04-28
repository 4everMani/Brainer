---
id: 06-tpre-a1b3
tags: [agentic-ai, 06_Implementation, tensorflow]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Data Preparation for Time Series

> [!ABSTRACT]
> Preparing data for time series forecasting involves creating overlapping windows of a fixed length and mapping them to corresponding targets. TensorFlow provides the `timeseries_dataset_from_array` utility for simple pipelines and the `window()` method in `tf.data` for complex, highly-customizable data loading scenarios.

## 🧠 Intuition First
- Imagine you're trying to learn the rhythm of a song. You can't just listen to one beat (data point). You have to listen to a 4-beat bar (window) and try to guess what the 5th beat (target) will be. You then shift your focus by one beat and repeat. **Data Preparation** is the process of chopping the full song into thousands of these "4-beat-to-5th-beat" practice segments.

## 🎯 Why This Matters
- Problem it solves: Converts a single long sequence into a standard supervised learning dataset (X, y) that a neural network can digest.
- Real-world usage: Mandatory preprocessing step for any sequential modeling task, including NLP, audio processing, and financial forecasting.

## 🧩 Glossary
- [[Overlapping Windows]] : Sequences that share most of their elements with the previous sequence (e.g., $t \dots t+4$ followed by $t+1 \dots t+5$).
- [[Window Size]] : The number of past time steps used as input ($L$).
- [[Shift]] : The number of steps the window moves forward at each iteration (usually 1).
- [[Drop Remainder]] : A setting that discards smaller windows at the very end of a sequence to maintain constant input shapes.

## ⚙️ Mechanics (First Principles)
### The `window()` Workflow:
1. **`window(size, shift, drop_remainder=True)`**: Creates a dataset of datasets (nested).
2. **`flat_map(lambda ds: ds.batch(size))`**: Converts the nested datasets into flat tensors of the correct size.
3. **`map(lambda w: (w[:-n], w[-n:]))`**: Splits each tensor into input features (the first $L$ steps) and targets (the last $n$ steps).
4. **`shuffle()` and `batch()`**: Standard tf.data operations to prepare for training.

### High-level Utility:
- **`timeseries_dataset_from_array()`**: Handles steps 1-3 in a single line. Perfect for simple regression.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Using the `timeseries_dataset_from_array` utility:
```python
import tensorflow as tf

dataset = tf.keras.utils.timeseries_dataset_from_array(
    data,
    targets=data[sequence_length:], # targets are L steps ahead
    sequence_length=sequence_length,
    batch_size=32,
    shuffle=True # Only shuffle the windows, not their internal order!
)
```

## 🧪 Experiments
1. **The Shape Check:** Create a dataset from the numbers 0 to 10 with `sequence_length=3`. Iterate through and print the shapes of X and y. Verify that X has 3 elements and y is the single number following those 3.

## ⚠️ Constraints & Pitfalls
- [[Data Leakage]] : Never shuffle the raw data before windowing, or your windows will contain random points from across time, which is impossible in the real world.
- **Scaling:** Always scale your time-series data *before* creating the windows for faster and more stable convergence.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[tf_data_API_Fundamentals]]
- Used in → [[RNN_Forecasting_Architectures]]
- Related to → [[Time_Series_Analysis_Fundamentals]]
---
(MINIMUM 3 links)
