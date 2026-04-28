---
id: 05-lear-a1b2
tags: [agentic-ai, 05_Optimization, gradient-descent]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Learning Rate and Schedules

> [!ABSTRACT]
> The learning rate ($\eta$) is the most critical hyperparameter in Gradient Descent, determining the size of each step. A learning schedule gradually reduces the learning rate during training, allowing the model to make fast progress initially and settle at the global minimum later.

## 🧠 Intuition First
- Imagine you're trying to park a car.
- **Fast Speed (High Learning Rate):** You zoom toward the spot and might overshoot, crashing or overshooting.
- **Crawl Speed (Low Learning Rate):** You're so slow it takes half an hour just to get within 10 feet.
- **Learning Schedule:** You drive fast toward the spot, then slow down as you get closer to align perfectly.

## 🎯 Why This Matters
- Problem it solves: Prevents a model from jumping around the minimum (diverging) and speeds up training when starting far from the optimal solution.
- Real-world usage: Fine-tuning deep learning models or training stochastic gradient descent (SGD) models.

## 🧩 Glossary
- [[Learning Rate]] : The step size ($\eta$) used to update model parameters in the direction of descending gradient.
- [[Learning Schedule]] : A function that decreases the learning rate at each iteration.
- [[Simulated Annealing]] : An optimization technique inspired by the cooling of molten metal.
- [[Divergence]] : A scenario where the cost function increases at every step because the learning rate is too high.

## ⚙️ Mechanics (First Principles)
### The 3 Learning Rate Scenarios:
1. **Too Small:** Takes an extremely long time to converge; might stop early at a local minimum (though not in linear regression).
2. **Too Large:** Jumps across the valley, end up on the other side, and potentially diverges with larger and larger values.
3. **Optimal:** Settles quickly at the global minimum.

### Learning Schedule Function:
- A common schedule: $\eta = \frac{t_0}{t + t_1}$, where $t$ is the iteration number and $t_0, t_1$ are hyperparameters. 
- *Benefit:* Helps stochastic gradient descent (SGD) converge exactly to the minimum despite its random nature.

## 📐 Mathematical Foundations
- **Step Equation:** $\boldsymbol{\theta}^{(next step)} = \boldsymbol{\theta} - \eta(t) \nabla_{\boldsymbol{\theta}}MSE(\boldsymbol{\theta})$
- $\eta(t)$ is the dynamic learning rate at iteration $t$.

## 💻 Implementation
- A simple learning schedule in Python:
```python
def learning_schedule(t):
    return 5 / (t + 50)

eta = learning_schedule(epoch * m + iteration)
theta = theta - eta * gradients
```

## 🧪 Experiments
1. **Divergence Test:** Intentionally set the learning rate to 10 in a gradient descent script. Observe how the RMSE quickly becomes `nan` as the model diverges.

## ⚠️ Constraints & Pitfalls
- **Hyperparameter Overhead:** A learning schedule adds more hyperparameters to tune ($t_0, t_1$), which can be time-consuming.
- **Early Stopping:** If the learning rate is reduced too quickly, the model might "freeze" halfway to the minimum.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Gradient_Descent_Variants]]
- Used in → [[Main_Challenges_of_Machine_Learning]]
- Related to → [[Bias_And_Variance]]
---
(MINIMUM 3 links)
