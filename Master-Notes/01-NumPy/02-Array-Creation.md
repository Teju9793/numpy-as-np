# Array Creation

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Create arrays from data or generate arrays with chosen shapes and values.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

x = np.array([2, 4, 6])
z = np.zeros((2, 3))
seq = np.arange(0, 10, 2)
points = np.linspace(0, 1, 5)
rng = np.random.default_rng(42)
```

## 4. Real-world use

Create feature matrices, initial values and reproducible synthetic data.

## 5. ML / AI connection

Create feature matrices, initial values and reproducible synthetic data.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `arange` uses a step; `linspace` uses a requested number of points. Floating-point steps can make `arange` endpoints surprising.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Create arrays from data or generate arrays with chosen shapes and values.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Create feature matrices, initial values and reproducible synthetic data.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
