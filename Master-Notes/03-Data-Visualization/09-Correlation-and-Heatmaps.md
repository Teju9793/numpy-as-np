# Correlation and Heatmaps

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Correlation measures strength and direction of association between numeric variables. A heatmap displays a matrix using colour.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import seaborn as sns
import matplotlib.pyplot as plt

corr = df.select_dtypes(include="number").corr()
sns.heatmap(corr, annot=True, cmap="coolwarm", center=0)
plt.show()
```

## 4. Real-world use

Find strongly related features and possible multicollinearity before modelling.

## 5. ML / AI connection

Find strongly related features and possible multicollinearity before modelling.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Correlation is not causation. Pearson correlation mainly captures linear association and can be affected by outliers.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Correlation measures strength and direction of association between numeric variables. A heatmap displays a matrix using colour.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Find strongly related features and possible multicollinearity before modelling.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Data Visualization chapter index](README.md) · [Master Notes home](../README.md)
