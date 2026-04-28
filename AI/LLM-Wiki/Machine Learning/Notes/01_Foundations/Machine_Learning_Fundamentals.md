---
id: 01-fund-a1b2
tags: [agentic-ai, 01_Foundations, ml-basics]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Machine Learning Fundamentals

> [!ABSTRACT]
> Machine Learning (ML) is the science of programming computers so they can learn from data. Unlike traditional programming, where rules are explicitly defined, ML systems improve their performance on a specific task through experience gained from training data.

## 🧠 Intuition First
- Imagine a spam filter. Instead of writing thousands of "if-then" rules to catch spam, you show the computer thousands of examples of spam and non-spam (ham) emails. The computer "learns" to recognize the patterns that distinguish them, much like a child learns to identify animals by being shown pictures.

## 🎯 Why This Matters
- Problem it solves: Automates tasks that are too complex for manual rule-based programming or where environments change over time (e.g., spammers changing their tactics).
- Real-world usage: Spam filtering, speech recognition, product recommendations, and autonomous driving.

## 🧩 Glossary
- [[Training Set]] : The set of examples the system uses to learn.
- [[Training Instance]] : A single example in the training set (also called a sample).
- [[Model]] : The part of an ML system that learns from data and makes predictions (e.g., a neural network).
- [[Accuracy]] : A performance measure often used in classification tasks, representing the ratio of correctly classified instances.

## ⚙️ Mechanics (First Principles)
- **Task (T):** The specific goal the system is trying to achieve (e.g., flagging spam).
- **Experience (E):** The data the system learns from (the training set).
- **Performance Measure (P):** The metric used to evaluate how well the system performs the task (e.g., accuracy).
- **Learning Rule:** A computer program is said to learn from experience **E** with respect to some task **T** and some performance measure **P**, if its performance on **T**, as measured by **P**, improves with experience **E**.

## 📐 Mathematical Foundations
- Performance Measure $P$ can be expressed as:
  $Accuracy = \frac{\text{Correct Predictions}}{\text{Total Predictions}}$

## 💻 Implementation
- Not applicable (See specific algorithm notes for implementation)

## 🧪 Experiments
1. **Rule-based vs. ML:** Try to write a set of 5 rules to identify spam. Then, consider how many more you'd need for "creative" spammers.
2. **Performance Impact:** Compare the accuracy of a model trained on 100 instances vs. 10,000 instances of the same task.

## ⚠️ Constraints & Pitfalls
- **Data Dependency:** Without high-quality experience (E), the performance (P) will not improve.
- **Task Specificity:** A model trained for task T1 (spam) cannot perform task T2 (face recognition) without new experience.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[ML_Framing]]
- Used in → [[Supervised_Learning]]
- Related to → [[Unsupervised_Learning]]
---
(MINIMUM 3 links)
