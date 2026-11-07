# Statistical Operations

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

NumPy provides descriptive statistics such as mean, median, standard deviation, variance, minimum, maximum and percentiles.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

scores = np.array([60, 70, 80, 90])
print(np.mean(scores))
print(np.median(scores))
print(np.std(scores))
print(np.percentile(scores, 75))
```

## 4. Real-world use

Understand feature scales and distributions; calculate summary statistics for EDA.

## 5. ML / AI connection

Understand feature scales and distributions; calculate summary statistics for EDA.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Choose the correct axis. Standard deviation is the square root of variance.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** NumPy provides descriptive statistics such as mean, median, standard deviation, variance, minimum, maximum and percentiles.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Understand feature scales and distributions; calculate summary statistics for EDA.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
