---
id: 06-call-a1b2
tags: [agentic-ai, 06_Implementation, keras]
source: Hands-On_Machine_Learning_with_Scikit-Learn_Keras_and_Tensorflow_-_Aurelien_Geron.pdf
date: 2026-04-22
type: technical-note
---

# Keras Callbacks and TensorBoard

> [!ABSTRACT]
> Keras callbacks are objects that can perform actions at various stages of training, such as saving checkpoints or stopping early. TensorBoard is an interactive visualization tool used to monitor learning curves, visualize computation graphs, and profile network performance during training.

## 🧠 Intuition First
- **Callbacks:** Imagine you're baking a cake. A callback is like a kitchen timer that rings when the cake is done (EarlyStopping) or an automated camera that takes a picture of the cake every 5 minutes so you can see how it rose (ModelCheckpoint).
- **TensorBoard:** This is the dashboard of your "neural network car." It shows you the speed (accuracy), fuel levels (loss), and engine health (gradients) in real-time while you drive.

## 🎯 Why This Matters
- Problem it solves: Prevents losing hours of training progress if a system crashes and automates the process of finding the "best" model version.
- Real-world usage: Monitoring large-scale training runs and identifying performance bottlenecks.

## 🧩 Glossary
- [[ModelCheckpoint]] : A callback that saves the model at regular intervals (e.g., after each epoch).
- [[EarlyStopping]] : A callback that halts training when performance on a validation set stops improving.
- [[Patience]] : The number of epochs to wait for improvement before EarlyStopping triggers.
- [[Event Files]] : Binary log files where TensorBoard summaries are stored.

## ⚙️ Mechanics (First Principles)
### Using Callbacks:
1. **Define:** Create callback instances (e.g., `EarlyStopping(patience=10)`).
2. **Pass:** Provide a list of these instances to the `callbacks` argument in `model.fit()`.

### Using TensorBoard:
1. **Log Directory:** Define a root log directory (e.g., `my_logs`).
2. **Timestamping:** Use subdirectories with timestamps to separate multiple runs.
3. **Callback:** Use `tf.keras.callbacks.TensorBoard(run_logdir)`.
4. **Visualization:** Run the TensorBoard server pointing to the log directory.

## 📐 Mathematical Foundations
- Not applicable

## 💻 Implementation
- Combining Early Stopping and Checkpoints:
```python
checkpoint_cb = tf.keras.callbacks.ModelCheckpoint("best_model.keras", 
                                                   save_best_only=True)
early_stopping_cb = tf.keras.callbacks.EarlyStopping(patience=10, 
                                                   restore_best_weights=True)

history = model.fit(X_train, y_train, epochs=100,
                    validation_data=(X_valid, y_valid),
                    callbacks=[checkpoint_cb, early_stopping_cb])
```

## 🧪 Experiments
1. **The Overfitting Visualization:** Intentionally train a model without any regularization on a small dataset. Use TensorBoard to visualize the gap between training loss and validation loss as it widens over time.

## ⚠️ Constraints & Pitfalls
- **Weights Only:** If using `save_weights_only=True`, you must have the model's architecture defined in code to reload it.
- **Log Management:** Without timestamped subdirectories, TensorBoard will merge learning curves from different runs, making them unreadable.

## 💥 Knowledge Collision (If Applicable)
> [!CONFLICT]
> Not applicable

## 🔗 Connections
- Builds on → [[Keras_Sequential_API]]
- Used in → [[MLOps_Fundamentals]]
- Related to → [[Early_Stopping]]
---
(MINIMUM 3 links)
