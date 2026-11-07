# Selection and Filtering

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Select rows and columns by labels, integer positions or conditions.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

df = pd.DataFrame({"age": [18, 25, 31], "city": ["Tumkur", "Bengaluru", "Tumkur"]})
print(df.loc[df["age"] >= 25, ["age", "city"]])
print(df.iloc[:2, 0])
```

## 4. Real-world use

Choose features, filter invalid observations and create subsets.

## 5. ML / AI connection

Choose features, filter invalid observations and create subsets.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- `loc` is label-based; `iloc` is position-based. Put parentheses around conditions combined with `&` or `|`.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Select rows and columns by labels, integer positions or conditions.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Choose features, filter invalid observations and create subsets.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
