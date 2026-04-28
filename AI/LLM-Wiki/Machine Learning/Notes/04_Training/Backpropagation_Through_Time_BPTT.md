---
id: 04-bptt-a1b2
tags: [agentic-ai, 04_Training, sequential-data]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Backpropagation Through Time BPTT

> [!ABSTRACT]
> Backpropagation Through Time (BPTT) is the algorithm used to train RNNs. It involves unrolling the network across time steps to form a static graph, performing a forward pass to compute outputs and loss, and then propagating gradients backward through each time step to update the shared parameters.

## 🧠 Intuition First
- Imagine a row of dominoes. Each domino is a time step. 
- **Forward Pass:** You tip the first domino, and the energy (signal) flows to the end. You measure how far the last domino fell compared to where it should be.
- **Backward Pass:** You work backward from the last domino, calculating how much the angle of each previous domino contributed to the final error. Since every domino is actually the *same* physical object (weight sharing), you sum up all the tiny adjustments to decide exactly how to carve that single object for the next run.

## 🎯 Why This Matters
- Problem it solves: Enables the application of standard gradient-based optimization to networks with temporal dependencies and shared weights.
- Real-world usage: Training any architecture with recurrent connections.

## 🧩 Glossary
- [[Unrolling]] : Creating a static representation of an RNN by replicating the recurrent layer for each time step.
- [[Shared Parameters]] : The property where the same weight matrices ($\mathbf{W}_x, \mathbf{W}_{\hat{y}}$) and bias ($b$) are used at every time step.
- [[Truncated BPTT]] : Limiting the number of time steps gradients flow back to prevent computational explosion and vanishing gradients (often used for very long sequences).

## ⚙️ Mechanics (First Principles)
### The 3 Steps:
1. **Forward Pass:** Pass the full input sequence through the unrolled network. Store all hidden states $h_{(t)}$ and outputs $\hat{y}_{(t)}$.
2. **Loss Evaluation:** Compute the loss using the targets $\mathbf{Y}$ and predictions $\hat{\mathbf{Y}}$. The loss can be a sum over all time steps or only the last one.
3. **Backward Pass:** Compute the gradient of the loss with respect to each output and state, moving from $t=T$ back to $t=0$.
    - **Weight Update:** Because weights are shared, the gradient for $\mathbf{W}$ is the sum of gradients computed at each time step.

## 📐 Mathematical Foundations
- **Weight Gradient Summation:**
  $\frac{\partial \mathcal{L}}{\partial \mathbf{W}} = \sum_{t=0}^{T} \frac{\partial \mathcal{L}}{\partial \mathbf{y}_{(t)}} \frac{\partial \mathbf{y}_{(t)}}{\partial \mathbf{W}}$

## 💻 Implementation
- BPTT is handled automatically by Keras when you call `model.fit()`.

## 🧪 Experiments
1. **The Gradient Sum:** In a custom training loop, track the gradient of the weights for a 5-step sequence. Verify that it is larger than a single-step gradient, reflecting the accumulation across time steps.

## ⚠️ Constraints & Pitfalls
- **Vanishing/Exploding Gradients:** Because the same matrix is multiplied repeatedly across time steps, gradients tend to either disappear (vanishing) or skyrocket (exploding) for long sequences.
- **Memory Cost:** Storing all intermediate states for long sequences can exceed RAM.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Backpropagation_and_Autodiff]]
- Used in → [[RNN_Forecasting_Architectures]]
- Related to → [[Recurrent_Neural_Networks_RNNs]]
---
(MINIMUM 3 links)
