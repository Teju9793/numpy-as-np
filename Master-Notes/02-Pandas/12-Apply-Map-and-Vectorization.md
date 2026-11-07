# Apply, Map and Vectorization

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Transform values with mapping and functions. Prefer built-in vectorized operations when possible.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"price": [100, 200, 300]})
df["tax"] = df["price"] * 0.18
df["band"] = df["price"].map(lambda x: "high" if x >= 200 else "low")
```

## 4. Real-world use

Create derived features and apply simple rules to columns.

## 5. ML / AI connection

Create derived features and apply simple rules to columns.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Do not reach for row-wise `apply(axis=1)` first; vectorized column expressions are often clearer and faster.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Transform values with mapping and functions. Prefer built-in vectorized operations when possible.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Create derived features and apply simple rules to columns.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
