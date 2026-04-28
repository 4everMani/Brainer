---
id: 06-rarc-a1b2
tags: [agentic-ai, 06_Implementation, sequential-data]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# RNN Forecasting Architectures

> [!ABSTRACT]
> RNNs can be applied to forecasting through various architectural patterns. While simple univariate RNNs provide a starting point, deep RNNs and multivariate models (incorporating multiple time series and auxiliary features) often yield superior performance by capturing complex, multi-scale temporal dependencies.

## 🧠 Intuition First
- Imagine you're predicting the temperature for tomorrow. 
- **Simple RNN:** You only look at the temperature from today. 
- **Deep RNN:** You have a team of experts. One looks at the hour-by-hour changes, another looks at the daily trend, and the third combines their insights to make a high-level prediction. 
- **Multivariate RNN:** You don't just look at temperature; you also look at wind speed, humidity, and the time of year to get a more complete picture.

## 🎯 Why This Matters
- Problem it solves: Optimizes the capacity and input signals of recurrent models to match the complexity of real-world time-series data.
- Real-world usage: Industrial demand forecasting, multi-sensor predictive maintenance, and multi-asset financial modeling.

## 🧩 Glossary
- [[Univariate Model]] : A model that takes only one time-series as input.
- [[Multivariate Model]] : A model that takes multiple time-series (e.g., rail and bus ridership) as input.
- [[Deep RNN]] : An architecture formed by stacking multiple recurrent layers.
- [[Multi-step Forecasting]] : Predicting a sequence of future values ($t+1, t+2, \dots, t+n$) instead of just the next step.

## ⚙️ Mechanics (First Principles)
### Architecture Comparison:
1. **Linear Baseline:** One Dense layer on the flattened sequence. Fast but ignores temporal order.
2. **Simple RNN:** One layer with $N$ neurons. Captures temporal order but has limited memory.
3. **Deep RNN:** Multiple layers (e.g., 3 stacks of 32 neurons). 
    - *Constraint:* All but the last layer must have `return_sequences=True`.
4. **Multivariate Model:** Receives a vector of features at each time step (e.g., input shape `[None, 5]`).

### Multi-step Strategies:
1. **Autoregressive:** Predict $t+1$, append it to input, predict $t+2$. (Error accumulates).
2. **One-shot:** Change output Dense layer to $N$ units to predict the whole future sequence at once.
3. **Seq-to-Seq:** Train the model to predict the future sequence at *every* time step. (Best gradient flow).

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Building a Deep Multivariate RNN for multi-step forecasting:
```python
model = tf.keras.Sequential([
    tf.keras.layers.SimpleRNN(32, return_sequences=True, input_shape=[None, 5]),
    tf.keras.layers.SimpleRNN(32, return_sequences=True),
    tf.keras.layers.SimpleRNN(32), # output is vector of 32
    tf.keras.layers.Dense(14)      # predict next 14 steps
])
```

## 🧪 Experiments
1. **The Depth Test:** Compare the MAE of a 1-layer vs. 3-layer RNN on the same task. Observe that deeper isn't always better; for some tasks, the added complexity leads to worse generalization.

## ⚠️ Constraints & Pitfalls
- **Hyperparameter Overhead:** Stacking recurrent layers adds many more hyperparameters (neurons per layer, dropout per layer) to tune.
- **Data Scaling:** All inputs in a multivariate model MUST be on a similar scale (e.g., 0-1) for stable training.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Recurrent_Neural_Networks_RNNs]]
- Used in → [[Backpropagation_Through_Time_BPTT]]
- Related to → [[Time_Series_Analysis_Fundamentals]]
---
(MINIMUM 3 links)
