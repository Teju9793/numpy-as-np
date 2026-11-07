# Missing Values

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Missing values represent information that was not recorded. Detect them and choose a justified treatment.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"age": [20, None, 30]})
df["age_missing"] = df["age"].isna().astype(int)
df["age"] = df["age"].fillna(df["age"].median())
```

## 4. Real-world use

Imputation is a common preprocessing step; missingness itself may carry information.

## 5. ML / AI connection

Imputation is a common preprocessing step; missingness itself may carry information.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Calculate imputation values from training data only. Do not automatically fill every column with zero.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Missing values represent information that was not recorded. Detect them and choose a justified treatment.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Imputation is a common preprocessing step; missingness itself may carry information.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
