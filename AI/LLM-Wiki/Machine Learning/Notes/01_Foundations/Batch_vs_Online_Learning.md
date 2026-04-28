---
id: 01-batc-a1b2
tags: [agentic-ai, 01_Foundations, ml-paradigms]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Batch vs Online Learning

> [!ABSTRACT]
> Machine learning systems can be classified by their ability to learn incrementally. Batch learning requires training on the full dataset offline, while online learning (or incremental learning) allows the system to update itself sequentially as new data arrives.

## 🧠 Intuition First
- **Batch Learning:** Like a student who studies an entire textbook once, takes an exam, and never reads another page. To learn new material, they must re-read the old textbook plus the new chapters from scratch.
- **Online Learning:** Like a student who reads one page every day and immediately incorporates that new knowledge into their understanding without needing to re-read everything they've ever learned.

## 🎯 Why This Matters
- Problem it solves: Handles fast-changing data (e.g., stock prices) and huge datasets that don't fit in memory (out-of-core learning).
- Real-world usage: A smartphone app that adapts to a user's voice on the fly (online) vs. a recommendation engine updated weekly (batch).

## 🧩 Glossary
- [[Offline Learning]] : Another term for batch learning, as training happens away from the live system.
- [[Mini-batch]] : A small group of data instances used in a single learning step in online learning.
- [[Learning Rate]] : A parameter in online learning that determines how fast the system should adapt to changing data.
- [[Model Rot]] : The slow decay of a model's performance over time as the world evolves (also called data drift).

## ⚙️ Mechanics (First Principles)
### Batch Learning
- **Process:** Train on all available data -> Launch to production -> Run without further learning.
- **Updates:** To include new data, a new version of the system must be trained from scratch on the **full** dataset (old + new).
- **Constraints:** Requires significant computing resources and time; cannot adapt quickly to rapid changes.

### Online Learning
- **Process:** Feed data instances sequentially (individually or in mini-batches).
- **Updates:** Each learning step is fast and cheap, allowing the system to learn "on the fly."
- **Out-of-core Learning:** Can train on datasets larger than main memory by loading and training on chunks of data.
- **Risk:** High sensitivity to "bad data," which can rapidly degrade performance if not monitored.

## 📐 Mathematical Foundations
- **Learning Rate ($\eta$):**
  - High $\eta$: Rapid adaptation, but quick forgetting of old patterns.
  - Low $\eta$: High inertia, slower learning, but more resilient to noise and outliers.

## 💻 Implementation
- Conceptual example of Out-of-core learning:
```python
# Pseudo-code for out-of-core learning
for batch in large_dataset_iterator:
    model.partial_fit(batch.X, batch.y)
```

## 🧪 Experiments
1. **Drift Detection:** Train a model on 2020 data and test it on 2024 data to measure the performance decay (model rot).
2. **Learning Rate Impact:** In an online system, artificially inject 10% noisy data and observe how quickly the model recovers with a low vs. high learning rate.

## ⚠️ Constraints & Pitfalls
- **Resource Exhaustion:** Batch learning can become impossible if the dataset grows beyond a certain size.
- **Catastrophic Forgetting:** In online learning, a high learning rate might cause the model to forget fundamental patterns when exposed to a string of atypical data.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> **Terminology Confusion:** "Online learning" is often used for systems that learn on a live stream, but the same algorithms are used for "Out-of-core learning" which is typically done offline. Geron suggests thinking of it as **Incremental Learning** to avoid confusion.

## 🔗 Connections
- Builds on → [[Machine_Learning_Fundamentals]]
- Used in → [[Model_Monitoring_And_Drift]]
- Related to → [[Instance_vs_Model_Based_Learning]]
