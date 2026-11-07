# Pivot Tables and Crosstab

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Reshape data to compare categories across rows and columns or summarize groups.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"city": ["A", "A", "B"], "type": ["X", "Y", "X"], "sales": [10, 20, 15]})
print(pd.pivot_table(df, values="sales", index="city", columns="type", aggfunc="sum"))
print(pd.crosstab(df["city"], df["type"]))
```

## 4. Real-world use

Explore category combinations and identify patterns before feature selection.

## 5. ML / AI connection

Explore category combinations and identify patterns before feature selection.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `pivot` requires unique index/column combinations; use `pivot_table` when aggregation is needed.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Reshape data to compare categories across rows and columns or summarize groups.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Explore category combinations and identify patterns before feature selection.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
