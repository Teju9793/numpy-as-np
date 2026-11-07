# Seaborn Fundamentals

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Seaborn is a statistical visualization library built on Matplotlib and works naturally with DataFrames.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.set_theme(style="whitegrid")
sns.scatterplot(data=df, x="age", y="income", hue="segment")
plt.show()
```

## 4. Real-world use

Quickly explore relationships and category differences using DataFrame column names.

## 5. ML / AI connection

Quickly explore relationships and category differences using DataFrame column names.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Know whether a function is axes-level (such as `scatterplot`) or figure-level (such as `relplot`).
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Seaborn is a statistical visualization library built on Matplotlib and works naturally with DataFrames.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Quickly explore relationships and category differences using DataFrame column names.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Data Visualization chapter index](README.md) · [Master Notes home](../README.md)
