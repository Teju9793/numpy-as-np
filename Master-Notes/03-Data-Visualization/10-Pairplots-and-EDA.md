# Pairplots and EDA

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

A pair plot displays pairwise relationships between selected numeric columns and their individual distributions.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import seaborn as sns

sns.pairplot(df[["feature_a", "feature_b", "feature_c", "target"]], hue="target")
```

## 4. Real-world use

Spot clusters, class separation and relationships across a small set of important features.

## 5. ML / AI connection

Spot clusters, class separation and relationships across a small set of important features.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Pair plots become slow and cluttered with many columns or rows; sample or select features first.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** A pair plot displays pairwise relationships between selected numeric columns and their individual distributions.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Spot clusters, class separation and relationships across a small set of important features.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Data Visualization chapter index](README.md) · [Master Notes home](../README.md)
