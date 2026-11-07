# Vectorization

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Vectorization expresses an operation over an entire array instead of writing a Python loop for each element.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

x = np.arange(1_000_000)
y = x * 2 + 5
```

## 4. Real-world use

Perform preprocessing and numerical calculations over large datasets.

## 5. ML / AI connection

Perform preprocessing and numerical calculations over large datasets.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Vectorization often improves speed and clarity, but measure performance for your real workload.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Vectorization expresses an operation over an entire array instead of writing a Python loop for each element.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Perform preprocessing and numerical calculations over large datasets.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
