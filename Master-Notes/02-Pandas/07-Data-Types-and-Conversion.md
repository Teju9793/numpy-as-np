# Data Types and Conversion

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Correct data types make operations reliable and can reduce memory use.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"age": ["18", "21"], "date": ["2026-01-01", "2026-01-02"]})
df["age"] = pd.to_numeric(df["age"])
df["date"] = pd.to_datetime(df["date"])
print(df.dtypes)
```

## 4. Real-world use

Convert numeric-looking text and dates before feature extraction or modelling.

## 5. ML / AI connection

Convert numeric-looking text and dates before feature extraction or modelling.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Invalid strings can raise conversion errors. Use `errors='coerce'` only when invalid values should become missing.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Correct data types make operations reliable and can reduce memory use.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Convert numeric-looking text and dates before feature extraction or modelling.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
