# Array Operations

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Arithmetic and comparison operations are usually element-wise; universal functions apply common math operations to arrays.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

x = np.array([1, 2, 3])
y = np.array([10, 20, 30])
print(x + y)
print(np.sqrt(y))
```

## 4. Real-world use

Scale features, calculate errors and perform numerical transformations.

## 5. ML / AI connection

Scale features, calculate errors and perform numerical transformations.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `*` is element-wise multiplication. Use `@` or `np.matmul` for matrix multiplication.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Arithmetic and comparison operations are usually element-wise; universal functions apply common math operations to arrays.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Scale features, calculate errors and perform numerical transformations.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
