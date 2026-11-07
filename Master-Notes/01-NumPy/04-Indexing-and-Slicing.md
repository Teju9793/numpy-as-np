# Indexing and Slicing

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Indexing selects elements; slicing selects ranges. NumPy uses zero-based indexing.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import numpy as np

x = np.array([[10, 20, 30], [40, 50, 60]])
print(x[1, 0])   # 40
print(x[:, 1])   # second column
print(x[x > 30])
```

## 4. Real-world use

Select rows, columns and feature subsets from a matrix.

## 5. ML / AI connection

Select rows, columns and feature subsets from a matrix.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Basic slices often create views; advanced and boolean indexing create copies. Use `x[row, col]` for a 2D element.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Indexing selects elements; slicing selects ranges. NumPy uses zero-based indexing.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Select rows, columns and feature subsets from a matrix.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to NumPy chapter index](README.md) · [Master Notes home](../README.md)
