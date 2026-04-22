---
id: 06-base-w3x4
tags: [agentic-ai, 06_Implementation, heuristics]
source: building-machine-learning-powered-applications-going-from-idea-to-product.pdf
date: 2026-04-22
type: technical-note
---

# Baseline Heuristics

> [!ABSTRACT]
> A baseline heuristic is a simple, non-ML rule or logic used to solve a problem before implementing complex models. It serves as a benchmark to evaluate whether an ML approach provides actual value and helps in understanding the data better.

## 🧠 Intuition First
- Before building a high-tech robotic weather station, you might just look at the sky. If it's cloudy, you guess "rain." This "if-then" rule is your baseline. If your expensive robot can't predict better than your simple glance at the clouds, the robot isn't worth the investment yet.

## 🎯 Why This Matters
- Problem it solves: Prevents over-engineering and provides a yardstick for measuring ML performance improvements.
- Real-world usage: Using a simple keyword search as a baseline for a complex semantic search engine.

## 🧩 Glossary
- [[Heuristic]] : A "rule of thumb" or simplified method used to make decisions.
- [[Baseline]] : A starting point used for comparisons.

## ⚙️ Mechanics (First Principles)
- **Identify Simple Rules:** Look for patterns in data that can be captured with basic logic (e.g., "if word count < 10, then bad quality").
- **Implement Logic:** Write a simple function or script to apply these rules.
- **Measure Performance:** Evaluate the heuristic using the same metrics intended for the ML model.
- **Compare:** Only proceed with ML if it significantly outperforms the baseline.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Example Baseline Heuristic for text quality:
```python
def baseline_quality_checker(text):
    # Rule: If text is too short or lacks a question mark, it's 'bad'
    if len(text.split()) < 5:
        return "Bad"
    if "?" not in text:
        return "Bad"
    return "Good"

# Test the baseline
print(baseline_quality_checker("Help me")) # Bad
print(baseline_quality_checker("How do I fix this error?")) # Good
```

## 🧪 Experiments
1. **Rule Stacking:** Add three more rules to the Python example above (e.g., checking for capital letters) and see if the "accuracy" on a small labeled set improves.
2. **The "Random" Baseline:** Implement a baseline that just guesses the most frequent class every time. This is the absolute minimum an ML model must beat.

## ⚠️ Constraints & Pitfalls
- **Heuristic Complexity:** If a heuristic becomes too complex (dozens of nested if-statements), it's a sign you should switch to ML.
- **Maintenance:** Heuristics can be brittle and hard to update as data distributions shift.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[ML_Framing]]
- Used in → [[Model_Evaluation]]
- Related to → [[Data_Exploration]]
