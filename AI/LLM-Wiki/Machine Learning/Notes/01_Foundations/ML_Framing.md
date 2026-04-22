---
id: 01-fram-u1v2
tags: [agentic-ai, 01_Foundations, ml-lifecycle]
source: building-machine-learning-powered-applications-going-from-idea-to-product.pdf
date: 2026-04-22
type: technical-note
---

# ML Framing

> [!ABSTRACT]
> ML Framing is the process of translating a high-level product goal or business problem into a well-defined machine learning task. It involves defining the model's inputs, outputs, and the success metrics that align with the intended user experience.

## 🧠 Intuition First
- Imagine you want to "help people write better." That is a vague goal. To frame it for ML, you must decide: Do you want to predict the next word (autocomplete), identify spelling errors (classification), or rank a draft on a scale of 1-10 (regression)? Each choice is a different way of "framing" the same problem.

## 🎯 Why This Matters
- Problem it solves: Prevents building technically accurate models that don't actually solve the user's problem.
- Real-world usage: Deciding whether to frame fraud detection as a binary classification (Spam vs. Not Spam) or an anomaly detection task.

## 🧩 Glossary
- [[Product Goal]] : The desired outcome for the user (e.g., "save time").
- [[ML Task]] : The technical formulation (e.g., "multi-class classification").

## ⚙️ Mechanics (First Principles)
- **Identify the Goal:** Define what service the application delivers to the user.
- **Estimate Feasibility:** Evaluate if the data exists and if the task is solvable with current ML techniques.
- **Select Task Type:** Map the goal to a category (Classification, Regression, Ranking, or Generation).
- **Define Input/Output:** Specify exactly what the model receives and what it must return.
- **Select Metrics:** Choose evaluation criteria (e.g., Precision, Recall, RMSE) that reflect product success.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Conceptual Framing for a "Writing Assistant":
    - **Goal:** Help users write better questions.
    - **Framing 1 (Classification):** Input: Text. Output: "Good" or "Bad".
    - **Framing 2 (Regression):** Input: Text. Output: Predicted score (0.0 to 1.0).
    - **Framing 3 (Sequence-to-Sequence):** Input: Poor text. Output: Improved text.

## 🧪 Experiments
1. **Alternative Framings:** Take a single problem (e.g., "recommend movies") and describe how it would change if framed as classification vs. ranking.
2. **Metric Alignment:** List three business goals (e.g., "increase revenue") and identify which ML metric (e.g., "CTR") best correlates with them.

## ⚠️ Constraints & Pitfalls
- **Over-framing:** Trying to solve a complex problem with a single model when a simple heuristic or multiple smaller models would be better.
- **Metric Misalignment:** Optimizing for a metric (like accuracy) that doesn't capture the true cost of failure (e.g., missing a rare but deadly disease).

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Supervised_Learning]]
- Used in → [[Baseline_Heuristics]]
- Related to → [[Data_Vectorization]]
