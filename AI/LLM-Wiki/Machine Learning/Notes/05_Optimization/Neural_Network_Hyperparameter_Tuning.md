---
id: 05-ntun-a1b2
tags: [agentic-ai, 05_Optimization, model-tuning]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Neural Network Hyperparameter Tuning

> [!ABSTRACT]
> Fine-tuning a neural network involves choosing the number of layers, neurons per layer, learning rate, and batch size. While automated tools like Keras Tuner and Bayesian optimization are effective, general rules of thumb—like the "stretch pants" approach—can provide a strong starting point for architecture design.

## 🧠 Intuition First
- Imagine you're tailoring a suit. 
- **Pyramid Approach:** You start with broad shoulders (many neurons) and taper down to the waist (few neurons). 
- **Stretch Pants Approach:** You build a suit that's a bit too large (more layers/neurons than needed) and then use "belts" (regularization like early stopping) to shrink it down to the perfect fit. This prevents the "tight suit" problem where the model doesn't have enough room to learn the data.

## 🎯 Why This Matters
- Problem it solves: Prevents building models that are too simple to learn the data (underfitting) or so complex that they learn only noise (overfitting).
- Real-world usage: Designing efficient deep learning models for mobile devices or high-accuracy server-side systems.

## 🧩 Glossary
- [[Parameter Efficiency]] : The ability of deep networks to model complex functions using exponentially fewer neurons than shallow ones.
- [[Bottleneck Layer]] : A layer with too few neurons that prevents useful information from passing to subsequent layers.
- [[Keras Tuner]] : A library for automated hyperparameter search for Keras models.
- [[Transfer Learning]] : Reusing the lower layers of a pretrained network to kickstart training on a new, related task.

## ⚙️ Mechanics (First Principles)
### Architecture Rules of Thumb:
1. **Hidden Layers:** For many problems, 1-2 layers are sufficient. Deep networks are more parameter-efficient for complex hierarchical data (e.g., images, speech).
2. **Neurons:** Using the same number of neurons for all hidden layers often performs as well as a pyramid structure and reduces tuning complexity.
3. **Stretch Pants:** Build slightly more layers/neurons than you think you need, then regularize.
4. **Learning Rate:** The most important hyperparameter. Find the "optimal" rate by growing it exponentially during a short training run and finding the point where the loss stops dropping.

### Automated Tuning (Keras Tuner):
- **RandomSearch:** Simple and fast.
- **Hyperband:** Smarter resource allocation (stops training poorly performing models early).
- **BayesianOptimization:** Uses Gaussian processes to zoom in on the best regions of hyperparameter space.

## 📐 Mathematical Foundations
- **Learning Rate Growth:** $\eta_{new} = \eta_{old} \times (10^{1/500})$ to grow from $10^{-5}$ to $10^{1}$ in 500 iterations.

## 💻 Implementation
- Finding optimal learning rate:
```python
# 1. Train for few hundred iterations
# 2. Multiply LR by constant factor each step
# 3. Plot Loss vs LR
# 4. Pick rate ~10x lower than the point where loss explodes
```

## 🧪 Experiments
1. **The Layer Test:** Compare a shallow MLP (1 layer, 1000 neurons) vs. a deep MLP (5 layers, 100 neurons each) on MNIST. Observe that the deep model often reaches the same accuracy with fewer total parameters.

## ⚠️ Constraints & Pitfalls
- **Generalization Gap:** Large batch sizes can lead to models that don't generalize as well as those trained with small batches (the "Friends don't let friends use mini-batches > 32" rule).
- **Search Space:** Bayesian optimization has its own hyperparameters that need careful setting.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Hyperparameter_Tuning_Strategies]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Early_Stopping]]
---
(MINIMUM 3 links)
