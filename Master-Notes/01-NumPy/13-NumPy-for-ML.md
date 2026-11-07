# NumPy for ML

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

ML data commonly uses `X` for a feature matrix and `y` for a target vector. Rows are samples; columns are features.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

X = np.array([[2., 10.], [4., 20.], [6., 30.]])
y = np.array([0, 1, 1])
mean = X.mean(axis=0)
std = X.std(axis=0)
X_scaled = (X - mean) / std
print(X.shape, y.shape)
```

## 4. Real-world use

Prepare feature matrices, understand scaling and verify data passed into an estimator.

## 5. ML / AI connection

Prepare feature matrices, understand scaling and verify data passed into an estimator.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Fit preprocessing statistics on training data only. Handle zero standard deviations, missing values and non-finite values deliberately.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** ML data commonly uses `X` for a feature matrix and `y` for a target vector. Rows are samples; columns are features.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Prepare feature matrices, understand scaling and verify data passed into an estimator.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
