---
id: 03-acpp-a1b2
tags: [agentic-ai, 03_Architecture, reinforcement-learning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Actor Critic and PPO

> [!ABSTRACT]
> Actor-Critic architectures combine the benefits of policy gradients and Q-learning. An **Actor** network proposes actions, while a **Critic** network evaluates them by estimating the state value ($V$). Proximal Policy Optimization (PPO) is a popular, stable algorithm that ensures policy updates remain within a safe range, preventing the model from collapsing during training.

## 🧠 Intuition First
- Imagine you're learning to dance. 
- **The Actor:** You (the dancer). You try out new moves based on your best guess. 
- **The Critic:** Your teacher watching from the sidelines. They don't tell you *what* to do, but they shout a score after each move (e.g., "That was a 9/10!"). 
- You use the teacher's feedback to adjust your moves. If you tried something new and the teacher's score went up, you do that more often. 
- **PPO:** This is like the teacher saying, "Don't change your dance style too much in one day! If you suddenly switch from Ballet to Hip-Hop in one lesson, you'll fall over." PPO forces you to make small, safe changes.

## 🎯 Why This Matters
- Problem it solves: Combines the high performance of policy-based methods with the stability and variance-reduction of value-based methods.
- Real-world usage: The current standard for high-performance deep RL, used in everything from game-playing bots to training LLMs with human feedback (RLHF).

## 🧩 Glossary
- [[Actor]] : The network that learns the policy $\pi(a|s)$.
- [[Critic]] : The network that learns to estimate the state value $V(s)$.
- [[TD Error (AC)]] : The difference between the immediate reward + discounted next state value and the current state value. Used as the "Advantage."
- [[PPO]] : Proximal Policy Optimization. An algorithm that clips the policy update to ensure it doesn't change too much from the previous version.
- [[A3C]] : Asynchronous Advantage Actor-Critic. Running multiple agents in parallel to speed up training.

## ⚙️ Mechanics (First Principles)
### The Actor-Critic Loop:
1. **Act:** Actor predicts action $a$ for state $s$.
2. **Evaluate:** Critic predicts value $V(s)$.
3. **Execute:** Observe reward $r$ and next state $s'$.
4. **Compute Advantage:** $A = r + \gamma V(s') - V(s)$.
5. **Update Critic:** Minimize the square of $A$ (Critic error).
6. **Update Actor:** Use $A$ as the return in the Policy Gradient update.

### PPO Clipping:
- The ratio of the new policy to the old policy is clipped between $1-\epsilon$ and $1+\epsilon$ (e.g., $0.8$ and $1.2$). This prevents "catastrophic updates" that can ruin a model's progress.

## 📐 Mathematical Foundations
- **PPO Objective:**
  $L^{CLIP} = \mathbb{E} [ \min(r_t(\theta) \hat{A}_t, \text{clip}(r_t(\theta), 1-\epsilon, 1+\epsilon) \hat{A}_t) ]$
  - Where $r_t(\theta)$ is the policy ratio.

## 💻 Implementation
- High-level PPO update logic (conceptual):
```python
# 1. Compute ratio: new_probs / old_probs
# 2. Compute clipped ratio
# 3. Take minimum of (ratio * advantage) and (clipped_ratio * advantage)
# 4. Minimize the negative of this objective
```

## 🧪 Experiments
1. **The Stability Test:** Train a standard Policy Gradient (REINFORCE) agent and a PPO agent on the same environment. Observe how the PPO agent's learning curve is much smoother and less prone to sudden "crashes" in performance.

## ⚠️ Constraints & Pitfalls
- **Parallelism:** While A3C/A2C benefit from parallelism, they can be complex to implement correctly without specialized libraries.
- **Actor/Critic Balance:** If the critic learns much faster or slower than the actor, training can become unstable.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Neural_Network_Policies_and_PG]]
- Used in → [[Reinforcement_Learning_Fundamentals]]
- Related to → [[Double_and_Dueling_DQN]]
---
(MINIMUM 3 links)
