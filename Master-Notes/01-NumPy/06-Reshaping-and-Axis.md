# Reshaping and Axis

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Reshaping changes an array's arrangement without changing its element count. An axis tells a reduction which dimension to operate across.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

x = np.arange(6)
M = x.reshape(2, 3)
print(M.sum(axis=0))  # column sums
print(M.sum(axis=1))  # row sums
print(M.T)
```

## 4. Real-world use

Convert flat data to model-compatible shapes and aggregate rows or features.

## 5. ML / AI connection

Convert flat data to model-compatible shapes and aggregate rows or features.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- For a 2D array, `axis=0` reduces rows (one result per column); `axis=1` reduces columns (one result per row).
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Reshaping changes an array's arrangement without changing its element count. An axis tells a reduction which dimension to operate across.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Convert flat data to model-compatible shapes and aggregate rows or features.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
