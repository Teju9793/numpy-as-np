# 10 — Merging, Joining and Concatenating DataFrames

> **Goal:** Combine tables correctly and understand keys, join types and row multiplication.

## 1. Why combine DataFrames?

Real datasets are often stored in separate tables. A student table may contain student IDs and names, while a marks table contains IDs and exam scores. You combine them using a shared key.

## 2. Sample tables

```python
import pandas as pd

students = pd.DataFrame({
    "student_id": [1, 2, 3],
    "name": ["Asha", "Ravi", "Maya"]
})

marks = pd.DataFrame({
    "student_id": [1, 2, 4],
    "score": [85, 72, 90]
})
```

The common key is `student_id`.

## 3. Inner join

An inner merge keeps only keys found in both tables:

```python
pd.merge(students, marks, on="student_id", how="inner")
```

Only student IDs 1 and 2 appear because they exist in both tables.

## 4. Left join

A left merge keeps every row from the left table and adds matching right-table values:

```python
pd.merge(students, marks, on="student_id", how="left")
```

Maya remains in the result, with a missing score because ID 3 was not found in the marks table.

## 5. Right and outer joins

- `how="right"`: keep all keys from the right table.
- `how="outer"`: keep all keys from both tables; unmatched fields become missing.

Choose the join based on which records you must preserve.

## 6. Different key names

```python
pd.merge(
    students,
    marks,
    left_on="id",
    right_on="student_id",
    how="inner"
)
```

Use `left_on` and `right_on` when the key columns have different names.

## 7. Validate relationships

If each student should have exactly one row in each table, use `validate`:

```python
pd.merge(students, marks, on="student_id", validate="one_to_one")
```

Other useful relationship checks include `one_to_many`, `many_to_one` and `many_to_many`. Validation can catch unexpected duplicate keys.

## 8. Why row counts sometimes increase

If a key appears twice in the left table and three times in the right table, a merge on that key can produce six matching combinations. This is a many-to-many join.

Always inspect key uniqueness and output row counts. A merge that runs without an error can still produce an incorrect analytical result.

## 9. Concatenate — stack tables

`pd.concat` combines objects along an axis:

```python
jan = pd.DataFrame({"Sales": [100, 200]})
feb = pd.DataFrame({"Sales": [150, 250]})

all_sales = pd.concat([jan, feb], ignore_index=True)
```

This stacks rows. Use `axis=1` to place objects side by side by index.

Concatenation aligns columns by their labels. Columns absent from one input receive missing values.

## 10. Merge versus concat

| Function | Main purpose |
|---|---|
| `merge` | Match rows using key columns or indexes |
| `join` | Convenient index-based joining |
| `concat` | Stack or place objects along an axis |

Use merge when records are related by a key. Use concat when you are combining similarly structured chunks or aligning objects by an axis.

## 11. Common mistakes

- Merging on the wrong key.
- Forgetting duplicate keys can multiply rows.
- Using inner join when unmatched records must be preserved.
- Forgetting to inspect missing values created by unmatched keys.
- Using concat when a key-based merge is required.

## 12. Practice

Create customer and order tables. Perform inner, left, right and outer merges. Count rows after each merge. Add a duplicate customer ID and observe how the result changes. Then concatenate two monthly transaction tables.

**Checkpoint:** Before merging, identify the key, expected relationship and which unmatched records should remain.
