---
id: 02-mdpb-a1b2
tags: [agentic-ai, 02_Mathematics, reinforcement-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Markov Decision Processes and Bellman

> [!ABSTRACT]
> Markov Decision Processes (MDPs) provide the mathematical framework for modeling decision-making in environments where outcomes are partly random and partly under the control of a decision maker. The **Bellman Optimality Equation** is the cornerstone of MDPs, defining the optimal value of a state or state-action pair recursively.

## 🧠 Intuition First
- Imagine a board game where every square is a "state." You roll a die (randomness) to move, but you also choose which path to take (agent's action). Some squares give you points (rewards). The **Bellman Equation** is the formula that tells you exactly how many points you can expect to get from any square if you play perfectly from that point onward.

## 🎯 Why This Matters
- Problem it solves: Formulates the "value" of being in a particular situation, allowing an agent to compare choices based on long-term consequences rather than just immediate rewards.
- Real-world usage: The mathematical foundation for Q-Learning, Value Iteration, and Actor-Critic models.

## 🧩 Glossary
- [[Markov Chain]] : A stochastic process where the next state depends only on the current state (memoryless).
- [[MDP]] : Markov Decision Process. A Markov chain with actions and rewards.
- [[Transition Probability]] : $T(s, a, s')$, the probability of reaching state $s'$ from state $s$ given action $a$.
- [[Discount Factor]] : $\gamma \in [0, 1]$, determines the importance of future rewards.
- [[State Value (V)]] : The expected return starting from state $s$ and following a specific policy.

## ⚙️ Mechanics (First Principles)
### The Bellman Optimality Equation ($V^*$):
- The optimal value of state $s$ is the maximum expected reward from any action $a$, plus the discounted value of the next state $s'$.
- $V^*(s) = \max_a \sum_{s'} T(s, a, s') [ R(s, a, s') + \gamma V^*(s') ]$

### Value Iteration:
- An algorithm that starts with $V(s) = 0$ for all $s$ and iteratively applies the Bellman equation as an update rule.
- It is guaranteed to converge to the unique optimal values $V^*$.

## 📐 Mathematical Foundations
- **Stationarity Assumption:** The transition probabilities and reward functions do not change over time.
- **Optimal Policy:** Once $V^*$ is known, the optimal action is simply the one that maximizes the term in the brackets.

## 💻 Implementation
- Updating state values (conceptual):
```python
for s in all_states:
    v_values[s] = max([
        sum([T(s, a, sp) * (R(s, a, sp) + gamma * v_prev[sp]) 
             for sp in next_states])
        for a in possible_actions[s]])
```

## 🧪 Experiments
1. **The Discount Impact:** Solve a simple 3-state MDP with $\gamma=0.1$ and $\gamma=0.99$. Observe how the "value" of states far from the reward is nearly zero when $\gamma$ is small, but large when $\gamma$ is near one.

## ⚠️ Constraints & Pitfalls
- [[Curse of Dimensionality (MDP)]] : Standard value iteration requires iterating over every state. For environments like Pac-Man or Chess, the number of states is so large it's impossible to compute (requires **Deep RL**).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Reinforcement_Learning_Fundamentals]]
- Used in → [[Deep_Q_Learning_DQN]]
- Related to → [[Q_Means_Clustering]]
---
(MINIMUM 3 links)
