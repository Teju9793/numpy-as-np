# Array Attributes and Dtypes

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

`shape`, `ndim`, `size` and `dtype` describe an array's dimensions, element count and data type.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

x = np.array([[1, 2, 3], [4, 5, 6]])
print(x.shape)  # (2, 3)
print(x.ndim)   # 2
print(x.size)   # 6
print(x.dtype)
```

## 4. Real-world use

Check feature-matrix dimensions and numeric types before model training.

## 5. ML / AI connection

Check feature-matrix dimensions and numeric types before model training.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `shape` is a tuple. `astype()` returns a converted array; assign the result if you want to keep it.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** `shape`, `ndim`, `size` and `dtype` describe an array's dimensions, element count and data type.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Check feature-matrix dimensions and numeric types before model training.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
