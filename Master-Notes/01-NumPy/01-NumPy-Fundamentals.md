# NumPy Fundamentals

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

NumPy is a library for fast numerical computing. Its main object, `ndarray`, stores values in a multidimensional array.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

values = [1, 2, 3]
arr = np.array(values)
print(arr * 2)  # [2 4 6]
```

## 4. Real-world use

Represent numeric features and targets as arrays before passing data to ML tools.

## 5. ML / AI connection

Represent numeric features and targets as arrays before passing data to ML tools.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- A NumPy array is not a Python list: multiplying an array scales each element; multiplying a list repeats it.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** NumPy is a library for fast numerical computing. Its main object, `ndarray`, stores values in a multidimensional array.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Represent numeric features and targets as arrays before passing data to ML tools.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
