# Bar and Count Plots

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Bar charts compare values across categories; count plots show how many observations belong to each category.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.countplot(data=df, x="category", order=df["category"].value_counts().index)
plt.xticks(rotation=30)
plt.show()
```

## 4. Real-world use

Check class balance and compare target rates across categories.

## 5. ML / AI connection

Check class balance and compare target rates across categories.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- A bar plot summarizes a numeric value; a count plot counts observations.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Bar charts compare values across categories; count plots show how many observations belong to each category.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Check class balance and compare target rates across categories.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Data Visualization chapter index](README.md) · [Master Notes home](../README.md)
