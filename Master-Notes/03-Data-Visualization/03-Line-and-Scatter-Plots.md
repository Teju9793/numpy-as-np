# Line and Scatter Plots

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Line plots show ordered trends; scatter plots show relationships between two numeric variables.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import matplotlib.pyplot as plt

hours = [1, 2, 3, 4]
marks = [45, 55, 68, 75]
fig, ax = plt.subplots()
ax.scatter(hours, marks, alpha=0.8)
ax.set(xlabel="Study hours", ylabel="Marks")
plt.show()
```

## 4. Real-world use

Inspect possible relationships between a feature and a target; identify clusters and nonlinear patterns.

## 5. ML / AI connection

Inspect possible relationships between a feature and a target; identify clusters and nonlinear patterns.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- A scatter plot shows association, not proof of causation. Use a line when x has meaningful order.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Line plots show ordered trends; scatter plots show relationships between two numeric variables.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Inspect possible relationships between a feature and a target; identify clusters and nonlinear patterns.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Data Visualization chapter index](README.md) · [Master Notes home](../README.md)
