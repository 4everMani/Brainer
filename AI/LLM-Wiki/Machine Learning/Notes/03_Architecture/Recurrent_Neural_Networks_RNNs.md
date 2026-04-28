---
id: 03-rnns-a1b2
tags: [agentic-ai, 03_Architecture, sequential-data]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Recurrent Neural Networks RNNs

> [!ABSTRACT]
> Recurrent Neural Networks (RNNs) are a class of neural networks designed to process sequential data. By incorporating feedback connections, they maintain an internal state (memory) that allows them to "remember" previous inputs in a sequence, making them ideal for tasks like time series forecasting and natural language processing.

## 🧠 Intuition First
- Imagine you're reading a book. To understand the current sentence, you need to remember the previous ones. A standard neural network is like someone who forgets the beginning of a sentence before they reach the end. An **RNN** is like a person who keeps a running summary of the story in their head. Each new word (input) is combined with the summary (hidden state) to update the understanding and predict what happens next.

## 🎯 Why This Matters
- Problem it solves: Enables the processing of variable-length inputs and captures temporal dependencies that static models (like MLPs) ignore.
- Real-world usage: Stock market prediction, speech-to-text, and translating languages.

## 🧩 Glossary
- [[Recurrent Neuron]] : A neuron that receives its own output from the previous time step as an additional input.
- [[Unrolling through Time]] : Representing a recurrent neuron as a sequence of identical neurons, one for each time step.
- [[Hidden State]] : The internal memory ($h_{(t)}$) of a recurrent cell that persists across time steps.
- [[Univariate Time Series]] : A sequence of single values (e.g., daily temperature).
- [[Multivariate Time Series]] : A sequence of vectors (e.g., temperature, humidity, and pressure).

## ⚙️ Mechanics (First Principles)
### The Recurrent Step:
- At each time step $t$, the neuron receives:
    1. The current input vector $\mathbf{x}_{(t)}$.
    2. The output from the previous time step $\hat{\mathbf{y}}_{(t-1)}$.
- **Output Calculation:** $\hat{\mathbf{y}}_{(t)} = \phi(\mathbf{W}_x^T \mathbf{x}_{(t)} + \mathbf{W}_{\hat{y}}^T \hat{\mathbf{y}}_{(t-1)} + b)$.
- **Memory:** Because $\hat{\mathbf{y}}_{(t)}$ depends on $\hat{\mathbf{y}}_{(t-1)}$, and that depends on $\hat{\mathbf{y}}_{(t-2)}$, the final output is a function of all previous inputs since $t=0$.

### Input/Output Topologies:
- **Seq-to-Seq:** Predicts a sequence (e.g., forecasting next 10 days).
- **Seq-to-Vector:** Predicts a single value (e.g., sentiment of a sentence).
- **Vector-to-Seq:** One input produces a sequence (e.g., image captioning).
- **Encoder-Decoder:** Sequence in -> Vector -> Sequence out (e.g., translation).

## 📐 Mathematical Foundations
- **Concatenated Weights:** The two weight matrices $\mathbf{W}_x$ and $\mathbf{W}_{\hat{y}}$ are often vertically concatenated into a single matrix $\mathbf{W}$ of shape $(n_{inputs} + n_{neurons}) \times n_{neurons}$.

## 💻 Implementation
- Basic RNN in Keras:
```python
import tensorflow as tf
# univariate sequences of any length [None, 1]
model = tf.keras.Sequential([
    tf.keras.layers.SimpleRNN(32, input_shape=[None, 1]),
    tf.keras.layers.Dense(1)
])
```

## 🧪 Experiments
1. **The Parameter Count:** For an RNN with 10 inputs and 32 neurons, calculate the total weights: $(10 \times 32) + (32 \times 32) + 32 = 1376$. Compare this to a Dense layer with 32 neurons.

## ⚠️ Constraints & Pitfalls
- **Short-term Memory:** Simple RNNs (like `SimpleRNN`) can only remember patterns ~10 steps long. For longer dependencies, use **LSTMs** or **GRUs**.
- **Input Shape:** Keras recurrent layers expect a 3D input: `[batch_size, time_steps, dimensionality]`.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Multilayer_Perceptrons_and_DNNs]]
- Used in → [[RNN_Forecasting_Architectures]]
- Related to → [[Backpropagation_Through_Time_BPTT]]
---
(MINIMUM 3 links)
