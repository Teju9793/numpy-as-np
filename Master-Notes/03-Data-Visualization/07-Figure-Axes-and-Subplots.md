# Figure, Axes and Subplots

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

A Figure can contain multiple Axes. Subplots make related comparisons easier to read together.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import matplotlib.pyplot as plt

fig, axes = plt.subplots(1, 2, figsize=(9, 3), sharey=True)
axes[0].hist(train_values)
axes[0].set_title("Train")
axes[1].hist(test_values)
axes[1].set_title("Test")
fig.tight_layout()
plt.show()
```

## 4. Real-world use

Compare train/test distributions and multiple features using consistent scales.

## 5. ML / AI connection

Compare train/test distributions and multiple features using consistent scales.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Use `axes.flat` or `axes.ravel()` when iterating over a grid of axes.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** A Figure can contain multiple Axes. Subplots make related comparisons easier to read together.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Compare train/test distributions and multiple features using consistent scales.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Data Visualization chapter index](README.md) · [Master Notes home](../README.md)
