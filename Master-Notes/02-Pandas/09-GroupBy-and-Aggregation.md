# GroupBy and Aggregation

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

GroupBy follows split–apply–combine: split rows into groups, calculate per group, then combine results.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"team": ["A", "A", "B"], "score": [70, 90, 80]})
print(df.groupby("team")["score"].agg(["mean", "max", "count"]))
```

## 4. Real-world use

Summarize categories, compare groups and create group-level features.

## 5. ML / AI connection

Summarize categories, compare groups and create group-level features.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `agg` usually reduces each group; `transform` returns results aligned to the original rows.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** GroupBy follows split–apply–combine: split rows into groups, calculate per group, then combine results.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Summarize categories, compare groups and create group-level features.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
