# Random Numbers and Sampling

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Use NumPy's random Generator to create reproducible random values, samples and permutations.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

rng = np.random.default_rng(7)
print(rng.integers(0, 10, size=5))
print(rng.normal(0, 1, size=3))
print(rng.permutation(5))
```

## 4. Real-world use

Create synthetic datasets, shuffle observations and sample data for experiments.

## 5. ML / AI connection

Create synthetic datasets, shuffle observations and sample data for experiments.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Use a fixed seed while developing for reproducibility; reproducibility is not the same as true randomness.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Use NumPy's random Generator to create reproducible random values, samples and permutations.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Create synthetic datasets, shuffle observations and sample data for experiments.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
