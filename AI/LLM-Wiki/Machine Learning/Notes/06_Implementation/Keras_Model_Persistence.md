---
id: 06-kper-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Keras Model Persistence

> [!ABSTRACT]
> Saving and restoring Keras models is essential for deploying them to production or continuing training later. Keras supports the standard TensorFlow `SavedModel` format (a directory) and the single-file `H5` or `.keras` formats. It also provides callbacks to automatically save checkpoints during training.

## 🧠 Intuition First
- Imagine you're writing a novel. You don't just finish the whole thing in one sitting. You save your progress every day (checkpoints) so if you lose your laptop, you don't lose the whole book. When you're done, you export the final version (SavedModel) so it can be published and read by everyone.

## 🎯 Why This Matters
- Problem it solves: Prevents data loss during long training sessions and enables the easy transfer of models from a training environment to a production server.
- Real-world usage: Deploying a model as a REST API or using it in a mobile app.

## 🧩 Glossary
- [[SavedModel]] : The default TensorFlow format for saving models, containing architecture, weights, and logic in a directory structure.
- [[H5 Format]] : A single-file format based on HDF5, useful for sharing models but less supported by production deployment tools.
- [[Checkpoint]] : A saved version of the model's weights and optimizer state at a specific point during training.
- [[Callbacks]] : Functions that can be called at various stages during training (e.g., at the end of each epoch).

## ⚙️ Mechanics (First Principles)
### Standard Save/Load:
1. **Save:** `model.save("my_model", save_format="tf")`. This creates a directory with `saved_model.pb` (architecture) and a `variables` subdirectory (weights).
2. **Load:** `model = tf.keras.models.load_model("my_model")`.

### Automated Checkpoints:
- Use `ModelCheckpoint` callback to save the model after every epoch (or only when it improves).
- Use `EarlyStopping` to stop training when the validation error stops improving.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Saving and using checkpoints:
```python
checkpoint_cb = tf.keras.callbacks.ModelCheckpoint("my_check.keras", 
                                                   save_best_only=True)
# Fit with callback
history = model.fit(X_train, y_train, epochs=10, 
                    validation_data=(X_valid, y_valid),
                    callbacks=[checkpoint_cb])

# Load the best version
model = tf.keras.models.load_model("my_check.keras")
```

## 🧪 Experiments
1. **The Restoration Test:** Train a model for 5 epochs. Save it. Shut down your Python session. Reload the model and verify that it produces the exact same predictions on a set of test instances.

## ⚠️ Constraints & Pitfalls
- **Custom Objects:** If your model uses custom layers or functions, you must provide a dictionary of these objects to `load_model()` so Keras knows how to reconstruct them.
- **Optimizer State:** `save_weights()` only saves the weights. `save()` saves everything, including the optimizer state, which is necessary to resume training correctly.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Model_Persistence_and_Deployment]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Early_Stopping]]
---
(MINIMUM 3 links)
