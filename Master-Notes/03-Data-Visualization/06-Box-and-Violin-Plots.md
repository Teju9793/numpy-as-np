# Box and Violin Plots

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

A box plot summarizes a distribution using quartiles and potential outliers; a violin plot also shows density shape.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import seaborn as sns
import matplotlib.pyplot as plt

sns.boxplot(data=df, x="group", y="score")
plt.show()
```

## 4. Real-world use

Compare feature distributions across classes and identify possible outliers.

## 5. ML / AI connection

Compare feature distributions across classes and identify possible outliers.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- A plotted outlier is not automatically an error. Investigate it using domain knowledge.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** A box plot summarizes a distribution using quartiles and potential outliers; a violin plot also shows density shape.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Compare feature distributions across classes and identify possible outliers.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Data Visualization chapter index](README.md) · [Master Notes home](../README.md)
