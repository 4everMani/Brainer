---
id: 03-nnpg-a1b2
tags: [agentic-ai, 03_Architecture, reinforcement-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Neural Network Policies and PG

> [!ABSTRACT]
> In Reinforcement Learning, a neural network can be used to represent a stochastic policy, mapping observations directly to action probabilities. Policy Gradients (PG) is an optimization technique that improves this policy by increasing the probability of actions that lead to high rewards and decreasing it for those that lead to low rewards.

## 🧠 Intuition First
- Imagine you're learning to balance a plate on a stick. 
- **Stochastic Policy:** Your brain says "Move left with 70% chance and right with 30% chance." You're not 100% sure yet, so you keep it random to explore. 
- **Policy Gradients:** You play for 10 seconds and the plate falls. You look back at all your moves. You think: "The moves I made right before the fall were probably bad." You reduce their probability for the next attempt. If you balance it for 60 seconds, you think: "Those were great moves!" and you increase their probability. You're "reinforcing" the good choices.

## 🎯 Why This Matters
- Problem it solves: Enables the learning of complex control strategies in high-dimensional or continuous action spaces where calculating exact Q-values is difficult.
- Real-world usage: Robotic control, autonomous drones, and sophisticated game playing agents.

## 🧩 Glossary
- [[Action Probability]] : The output of a policy network (e.g., via Softmax or Sigmoid).
- [[REINFORCE]] : A classic PG algorithm that uses the full episode's return to estimate the gradient.
- [[Action Advantage]] : A measure of how much better an action was compared to the average (often calculated by discounting and normalizing rewards).
- [[Action Score]] : The log-probability of an action, used in the gradient update.

## ⚙️ Mechanics (First Principles)
### The PG Training Loop:
1. **Play:** Use the current policy to play several episodes. At each step, record the observation, the action taken, and the gradient of the log-probability.
2. **Compute Return:** At the end of each episode, calculate the discounted return for every action taken.
3. **Weight Gradients:** Multiply each recorded gradient by its corresponding discounted return.
4. **Average & Apply:** Compute the mean of these weighted gradients across all steps/episodes and update the model weights using Gradient Descent.

## 📐 Mathematical Foundations
- **Score Function Gradient:**
  $\nabla_{\boldsymbol{\theta}} J(\boldsymbol{\theta}) \approx \mathbb{E} [ \nabla_{\boldsymbol{\theta}} \log \pi_{\boldsymbol{\theta}}(a|s) \cdot R ]$
  - Where $R$ is the return.

## 💻 Implementation
- High-level PG training step in Keras:
```python
with tf.GradientTape() as tape:
    left_proba = model(observations)
    # Binary cross-entropy between action taken and predicted proba
    loss = tf.keras.losses.binary_crossentropy(actions, left_proba)

# Weight loss by the advantage (discounted rewards)
weighted_loss = tf.reduce_mean(loss * action_advantages)
grads = tape.gradient(weighted_loss, model.trainable_variables)
optimizer.apply_gradients(zip(grads, model.trainable_variables))
```

## 🧪 Experiments
1. **The Advantage Test:** Compare a PG agent that uses raw rewards vs. one that uses normalized advantages (subtracting the mean reward). Observe that normalization significantly reduces the "gradient noise" and speeds up training.

## ⚠️ Constraints & Pitfalls
- [[Sample Inefficiency]] : PG algorithms often require playing thousands of episodes to get a stable estimate of the gradient.
- **High Variance:** Gradients can be very noisy, leading to unstable learning.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Reinforcement_Learning_Fundamentals]]
- Used in → [[Deep_Q_Learning_DQN]]
- Related to → [[OpenAI_Gym_and_Environments]]
---
(MINIMUM 3 links)
