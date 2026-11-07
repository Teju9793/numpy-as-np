# Reading and Inspecting Data

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Inspect a dataset before changing it: check size, sample rows, column types and summary statistics.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.read_csv("data.csv")
print(df.head())
print(df.shape)
df.info()
print(df.describe(include="all"))
```

## 4. Real-world use

Initial dataset inspection is the first step in a reliable ML workflow.

## 5. ML / AI connection

Initial dataset inspection is the first step in a reliable ML workflow.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `info()` prints a summary and returns `None`; `describe()` summarizes numeric columns by default.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Inspect a dataset before changing it: check size, sample rows, column types and summary statistics.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Initial dataset inspection is the first step in a reliable ML workflow.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
