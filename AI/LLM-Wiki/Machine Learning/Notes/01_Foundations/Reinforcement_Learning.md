---
id: 01-rein-e5f6
tags: [agentic-ai, 01_Foundations, reinforcement-learning]
source: 0812_Machine-Learning-for-Absolute-Beginners.pdf
date: 2026-04-22
type: technical-note
---

# Reinforcement Learning

> [!ABSTRACT]
> Reinforcement learning (RL) is a machine learning category where an agent learns to make decisions by performing actions in an environment to maximize a reward. It relies on a trial-and-error approach, receiving feedback (positive or negative) to refine its behavior over time.

## 🧠 Intuition First
- Think of training a dog. You don't give the dog a math formula or show it thousands of pictures of people sitting. Instead, when the dog sits on command, you give it a treat (positive reward). If it ignores you, it gets nothing. Eventually, the dog learns that the "sit" action in the "command" environment leads to the best outcome.

## 🎯 Why This Matters
- Problem it solves: Optimizing decision-making in complex, dynamic environments where historical labels are unavailable but success can be measured.
- Real-world usage: Training AI to play video games (e.g., Pac-Man), optimizing logistics routes, or controlling autonomous vehicles.

## 🧩 Glossary
- [[Agent]] : The entity that makes decisions and learns.
- [[Environment]] : The world in which the agent operates.
- [[Reward]] : The feedback received from the environment based on an action.

## ⚙️ Mechanics (First Principles)
- **State Selection:** The agent observes the current state (S) of the environment.
- **Action Execution:** The agent chooses and executes an action (A) from the available options.
- **Feedback Loop:** The environment provides a reward or penalty based on the action taken.
- **Value Update:** The agent updates its strategy (often represented by a Q-value) to favor actions that led to higher rewards in similar states.
- **Trial & Error:** This cycle repeats millions of times until the agent identifies the optimal policy.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Minimal conceptual example (Q-learning logic):
```python
# Conceptual logic for updating a Q-value
# Q(state, action) = Q(state, action) + learning_rate * (reward + discount_factor * max(Q_next_state) - Q(state, action))

states = ["level_start", "near_ghost", "near_power_pill"]
actions = ["move_left", "move_right", "stay"]
q_table = {} # Dictionary mapping (state, action) to a value

# If Pac-Man eats a pill:
# reward = 10
# q_table[("near_power_pill", "move_right")] += 1 
```

## 🧪 Experiments
1. **Reward Shaping:** Change the reward values (e.g., make penalties for "death" much larger) and observe how quickly the agent learns to avoid danger.
2. **Exploration vs. Exploitation:** Adjust the agent's tendency to try new random moves versus using known high-reward moves to see the effect on total learning time.

## ⚠️ Constraints & Pitfalls
- **Computational Cost:** RL often requires vast amounts of computing power and millions of iterations to converge on a good solution.
- **Credit Assignment Problem:** It can be difficult for the agent to know which specific action in a long sequence was responsible for a final reward or penalty.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Supervised_Learning]]
- Used in → [[Q_Learning]]
- Related to → [[Unsupervised_Learning]]
