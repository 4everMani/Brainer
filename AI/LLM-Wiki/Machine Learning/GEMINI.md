# 🧠 Knowledge Engineer Schema v3 (Production-Ready Agent Contract)

---

# 🎯 CORE OBJECTIVE

Transform raw technical content into a **structured, multi-file Obsidian knowledge system** using:

- First-principles reasoning
    
- Layered learning abstraction
    
- Atomic note architecture
    
- Graph-based linking
    

---

# 📂 ENVIRONMENT CONFIGURATION

- SOURCE_ROOT: /raw
    
- DESTINATION_ROOT: /Notes
    
- LOG_FILE_PATH: /Notes/log.md
    

---

# 📊 1. STATE MANAGEMENT (STRICT)

## 1.1 Log File Format (MANDATORY)

The `log.md` MUST follow this exact YAML structure:

```yaml
---
session_id: <hash>
source: <file_name>
status: completed | partial
notes_created: [Concept_A, Concept_B]
bottlenecks_identified: [List any gaps]
---
```

## 1.2 Rules

- ALWAYS read `log.md` before processing
    
- IF `source` already exists with status = completed → STOP (do not regenerate)
    
- IF status = partial → process only missing concepts
    
- ALWAYS append new entry after processing
    

---

# 🧩 2. KNOWLEDGE LAYERS (MANDATORY CLASSIFICATION)

Every concept MUST belong to EXACTLY one layer:

00_Intuition → analogies, mental models  
01_Foundations → primitives (tokens, embeddings)  
02_Mathematics → formulas, derivations  
03_Architecture → system design (transformers, attention)  
04_Training → loss, backpropagation  
05_Optimization → gradient descent, efficiency  
06_Implementation → code, engineering  
07_Experiments → hands-on tasks

## Rules

- DO NOT skip layers
    
- Prefer lower layer if ambiguous
    
- Higher layer concepts MUST link to lower layer dependencies
    

---

# 🧱 3. ATOMIC NOTE CONTRACT

## 3.1 Granularity Rules

- One concept = one file
    
- If content > 300 lines → split
    
- If content < 50 lines → merge with closest concept
    

## 3.2 Naming Convention

PascalCase_With_Underscores.md

Examples:

- Attention_Mechanism.md
    
- Gradient_Descent.md
    

## 3.3 Unique ID (MANDATORY)

Each note MUST include:

id: --<4charhash>

Example:  
id: 01-tokenization-a1b2

---

# 📄 4. NOTE TEMPLATE (STRICT — NO DEVIATION)

```markdown
---
id: <unique_id>
tags: [agentic-ai, <layer>, <topic>]
source: <source_file_name>
date: <YYYY-MM-DD>
type: technical-note
---

# <Concept Title>

> [!ABSTRACT]
> 3–5 sentence high-level summary

## 🧠 Intuition First
- Explain using analogy
- NO math allowed

## 🎯 Why This Matters
- Problem it solves
- Real-world usage

## 🧩 Glossary
- [[Term]] : Definition
(MINIMUM 2 terms)

## ⚙️ Mechanics (First Principles)
- Step-by-step explanation
- No skipped reasoning

## 📐 Mathematical Foundations
- Use LaTeX where applicable
- If not applicable → write "Not applicable"

## 💻 Implementation
- Minimal working example (Python preferred)
- If not applicable → explain why

## 🧪 Experiments
- Minimum 2 actionable experiments

## ⚠️ Constraints & Pitfalls
- Minimum 2 limitations or failure cases

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Describe contradiction between sources
> Reference both sources explicitly

## 🔗 Connections
- Builds on → [[Concept]]
- Used in → [[Concept]]
- Related to → [[Concept]]
(MINIMUM 3 links)
```

---

# 🔍 5. DECOMPOSITION STRATEGY

## Step 1: Extract Concepts

- Identify all core and sub-concepts
    
- Split complex topics into atomic units
    

## Step 2: Assign Layer

- Map each concept to correct layer
    

## Step 3: Generate Notes

- Apply template strictly
    
- Avoid mixing concepts
    

## Step 4: Link Graph

- Ensure each note has ≥ 3 connections
    
- Create bidirectional links where possible


### 5.2 Large-Scale Ingestion (The 5,000 Page Rule)

If the source material is massive, the Agent MUST:

1. **Map Phase:** Scan Table of Contents/Headers across all sources.
    
2. **Cluster Phase:** Group similar concepts from different books (e.g., Book 1 and Book 4 both cover "Attention").
    
3. **Sequence Phase:** Process in "Logical Sprints" (max 50 pages or 100k tokens per pass) to maintain precision.
    

---

# 💥 6. COLLISION DETECTION RULES

A conflict MUST be flagged if:

- Same concept has contradictory claims across sources
    
- Performance claims differ significantly
    
- Architectural trade-offs are inconsistent
    

## Agent MUST:

- Use `[!CONFLICT]` block
    
- Mention both sources
    
- NOT resolve conflict
    
- ONLY highlight discrepancy
    

---

# 📘 7. INDEX MANAGEMENT

## Rules

- Maintain strict order (00 → 07)
    
- Use hierarchical markdown lists
    
- Use [[wikilinks]] ONLY
    
- DO NOT duplicate entries
    

## Format

# 🧠 Knowledge Garden Index

## 🌱 00 - Intuition

- [[Concept]]
    

## 🧩 01 - Foundations

- [[Concept]]
    

(continue for all layers)

---

# 📂 8. DEPLOYMENT MANIFEST (MANDATORY OUTPUT)

Agent MUST output BEFORE notes:

### 📂 DEPLOYMENT_MANIFEST

Format:  
<DESTINATION_ROOT>//.md

Example:  
LLM-Knowledge-Garden/01_Foundations/Tokenization.md

---

# 🔄 9. UPDATE STRATEGY

When processing new data:

- IF concept overlap > 60% → update existing note
    
- ELSE → create new note
    
- ALWAYS update connections
    
- ALWAYS update index.md
    

---

# 🧠 10. QUALITY RULES

Each note MUST:

- Be self-contained
    
- Be understandable by intermediate engineer
    
- Include intuition + mechanics + (math if applicable)
    
- Include implementation or reasoning
    
- Have ≥ 3 connections
    

---

# 🚀 11. OUTPUT ORDER (STRICT)

Agent MUST output in this order:

1. 📂 DEPLOYMENT_MANIFEST
    
2. 📘 index.md
    
3. 📄 All atomic notes
    
4. 📄 updated log.md
    

---

# ❌ 12. HARD FAIL CONDITIONS

Agent MUST STOP if:

- SOURCE_ROOT data missing
    
- log.md is corrupted or not readable JSON
    
- Concepts cannot be clearly extracted
    

---

# 🧠 FINAL PRINCIPLE

Always follow learning order:

Intuition → Mechanics → Math → Code → Experiment

Violation of this order is NOT allowed.