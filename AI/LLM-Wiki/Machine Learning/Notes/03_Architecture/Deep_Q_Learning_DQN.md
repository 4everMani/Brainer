---
id: 03-dqnx-a1b2
tags: [agentic-ai, 03_Architecture, reinforcement-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Deep Q Learning DQN

> [!ABSTRACT]
> Deep Q-Learning (DQN) combines Q-Learning with Deep Neural Networks to solve reinforcement learning problems with large or continuous state spaces. Instead of using a lookup table for Q-values, a **Deep Q-Network** acts as a function approximator, predicting the quality of each action given a state input.

## 🧠 Intuition First
- Imagine you're playing a video game with billions of possible screen frames (states). You can't have a strategy for every single frame. Instead, you develop an "instinct." You look at the screen and your brain tells you: "Jumping has a 90% chance of being good here." A **DQN** is the mathematical version of that instinct. It doesn't remember every frame; it generalizes from its experience to understand what a "good situation" looks like generally.

## 🎯 Why This Matters
- Problem it solves: Scales reinforcement learning to complex environments (like Atari games) where the state space is too large for tabular methods.
- Real-world usage: Recommendation engines with millions of items and complex industrial control systems.

## 🧩 Glossary
- [[DQN]] : Deep Q-Network. A neural network that maps states to Q-values.
- [[Approximate Q-Learning]] : Using a function (e.g., a DNN) to estimate Q-values instead of a table.
- [[Target Q-Value]] : The value the model tries to predict: $r + \gamma \max Q(s', a')$.
- [[TD Error]] : The difference between the current Q-value prediction and the target Q-value.

## ⚙️ Mechanics (First Principles)
### The Training Step:
1. **Predict:** Use the DQN to predict Q-values for the current state $s$.
2. **Select:** Pick an action $a$ (using $\epsilon$-greedy policy).
3. **Execute:** Observe reward $r$ and next state $s'$.
4. **Target Calculation:** Compute the target $y = r + \gamma \max_{a'} Q(s', a')$ using the same DQN (or a separate target network).
5. **Loss:** Minimize the MSE (or Huber Loss) between the predicted $Q(s, a)$ and the target $y$.

### Experience Replay:
- Crucial for stability. Instead of training on consecutive steps (which are highly correlated), the agent stores experiences $(s, a, r, s')$ in a buffer and samples random batches for training.

## 📐 Mathematical Foundations
- **Bellman Target:**
  $y^{(i)} = r^{(i)} + \gamma \cdot \max_{a'} Q_{\boldsymbol{\theta}}(s'^{(i)}, a')$
- **Loss Function:**
  $J(\boldsymbol{\theta}) = \mathbb{E} [ (y - Q_{\boldsymbol{\theta}}(s, a))^2 ]$

## 💻 Implementation
- High-level DQN architecture in Keras:
```python
model = tf.keras.Sequential([
    tf.keras.layers.Dense(32, activation="elu", input_shape=[n_states]),
    tf.keras.layers.Dense(32, activation="elu"),
    tf.keras.layers.Dense(n_outputs) # One output per possible action
])
```

## 🧪 Experiments
1. **The Target Network Test:** Train a DQN where the target is calculated using the *same* network that is being updated. Then, train one where the target is calculated using a "frozen" copy of the network that is updated only every 50 steps. Observe that the second one is much more stable.

## ⚠️ Constraints & Pitfalls
- [[Moving Target Problem]] : Since the target $y$ depends on the model's own predictions, the "goal" for the optimizer moves as the model learns, which can lead to divergence.
- **Catastrophic Forgetting:** If the agent only trains on its most recent wins, it will forget how to handle other parts of the game.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Markov_Decision_Processes_and_Bellman]]
- Used in → [[Experience_Replay_and_Exploration_Policies]]
- Related to → [[Neural_Network_Policies_and_PG]]
---
(MINIMUM 3 links)
