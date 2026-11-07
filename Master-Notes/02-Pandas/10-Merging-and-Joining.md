# Merging and Joining

> **Level:** Beginner → Intermediate · **Priority:** Core

## 1. Concept

Combine related tables using shared keys or stack compatible tables.

## 2. Why it matters

This topic helps you write clearer, safer data code and understand what happens to your data before it reaches a model.

## 3. Syntax and small example

```python
import pandas as pd

students = pd.DataFrame({"id": [1, 2], "name": ["Asha", "Ravi"]})
marks = pd.DataFrame({"id": [1, 2], "score": [88, 91]})
print(students.merge(marks, on="id", how="left"))
```

## 4. Real-world use

Join customer, transaction, product or lookup tables to build a modelling dataset.

## 5. ML / AI connection

Join customer, transaction, product or lookup tables to build a modelling dataset.

## 6. Tips and shortcuts

- Inspect the result immediately with `print()`, `.shape`, `.dtype` or a small sample.
- Prefer readable expressions over clever one-liners.
- Test assumptions on a tiny example before applying an operation to a full dataset.

## 7. Common mistakes

- Check key uniqueness and row counts after merging; duplicate keys can multiply rows.
- Forgetting to check the shape, type or index of the result.
- Applying a learned transformation before splitting train/test data can cause data leakage.

## 8. Quick revision

- **Remember:** Combine related tables using shared keys or stack compatible tables.
- **Use it when:** you need the operation described in this chapter.
- **ML relevance:** Join customer, transaction, product or lookup tables to build a modelling dataset.

## 9. Practice

1. Explain this concept in your own words without looking at the definition.
2. Change the example values or data shape and predict the output before running it.
3. Identify one place this operation could appear in a real ML preprocessing workflow.

---

[← Back to Pandas chapter index](README.md) · [Master Notes home](../README.md)
