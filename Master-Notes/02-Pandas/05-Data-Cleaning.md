# Data Cleaning

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Cleaning fixes inaccurate, duplicated or inconsistent records before analysis.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"city": ["Tumkur ", "tumkur", "Mysuru"]})
df["city"] = df["city"].str.strip().str.title()
df = df.drop_duplicates()
```

## 4. Real-world use

Poor-quality inputs can mislead a model and reduce performance.

## 5. ML / AI connection

Poor-quality inputs can mislead a model and reduce performance.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Inspect before dropping rows or columns. Cleaning decisions should follow domain meaning, not convenience.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Cleaning fixes inaccurate, duplicated or inconsistent records before analysis.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Poor-quality inputs can mislead a model and reduce performance.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
