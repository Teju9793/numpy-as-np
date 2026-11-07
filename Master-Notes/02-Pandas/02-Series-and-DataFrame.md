# Series and DataFrame

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

A Series is one-dimensional; a DataFrame is two-dimensional and contains aligned columns.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

s = pd.Series([10, 20, 30], name="marks")
df = pd.DataFrame({"marks": s, "passed": [False, True, True]})
print(df.shape)
print(df["marks"])
```

## 4. Real-world use

Understand the table structure that will be cleaned and converted into model features.

## 5. ML / AI connection

Understand the table structure that will be cleaned and converted into model features.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `df['col']` usually returns a Series; `df[['col']]` returns a DataFrame.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** A Series is one-dimensional; a DataFrame is two-dimensional and contains aligned columns.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Understand the table structure that will be cleaned and converted into model features.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
