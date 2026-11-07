# String and Date Operations

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Pandas provides vectorized string and datetime tools through `.str` and `.dt`.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"joined": ["2025-06-10", "2025-08-15"], "city": ["tumkur", "MYSURU"]})
df["joined"] = pd.to_datetime(df["joined"])
df["month"] = df["joined"].dt.month
df["city"] = df["city"].str.title()
```

## 4. Real-world use

Extract month, weekday, duration or normalized text features from raw columns.

## 5. ML / AI connection

Extract month, weekday, duration or normalized text features from raw columns.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Parse ambiguous dates explicitly. `.str` and `.dt` operate on Series.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Pandas provides vectorized string and datetime tools through `.str` and `.dt`.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Extract month, weekday, duration or normalized text features from raw columns.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
