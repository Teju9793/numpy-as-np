# 12 — apply, map and Vectorization in Pandas

> **Goal:** Transform values with the right tool and avoid slow or unnecessary row-wise Python operations.

## 1. Why transform columns?

Data preparation often requires new columns: convert marks into grades, calculate tax, standardize text or combine information. Pandas offers several approaches, and the right choice depends on whether the transformation is element-wise, column-wise or row-wise.

## 2. Series.map

`map` is useful for mapping each value in a Series through a dictionary or function.

```python
import pandas as pd

df = pd.DataFrame({"Grade": ["A", "B", "A", "C"]})
points = {"A": 10, "B": 8, "C": 6}
df["Points"] = df["Grade"].map(points)
print(df)
```

Values not present in the mapping dictionary become missing. Check for unexpected categories before relying on the output.

## 3. Series.apply

`apply` can apply a Python function to each Series value:

```python
marks = pd.Series([35, 60, 85])
def grade(score):
    if score >= 80:
        return "A"
    elif score >= 40:
        return "Pass"
    return "Fail"

print(marks.apply(grade))
```

This is flexible, but for simple arithmetic and comparisons, vectorized expressions are often faster and clearer.

## 4. DataFrame.apply

`DataFrame.apply` applies a function along an axis:

```python
df = pd.DataFrame({
    "Math": [80, 90],
    "Science": [70, 85]
})

df["Total"] = df[["Math", "Science"]].apply(sum, axis=1)
```

- `axis=0`: function receives each column.
- `axis=1`: function receives each row.

Row-wise apply can be slower for large data because it invokes Python code per row.

## 5. Vectorized arithmetic

Instead of:

```python
# Avoid this for simple column arithmetic
df["Total"] = df.apply(lambda row: row["Math"] + row["Science"], axis=1)
```

Prefer:

```python
df["Total"] = df["Math"] + df["Science"]
```

This uses optimized column operations and is easier to read.

## 6. Vectorized conditions with np.where

```python
import numpy as np

df["Result"] = np.where(df["Total"] >= 150, "High", "Other")
```

For multiple conditions, consider `np.select`:

```python
conditions = [
    df["Total"] >= 170,
    df["Total"] >= 140
]
choices = ["Excellent", "Good"]
df["Category"] = np.select(conditions, choices, default="Needs work")
```

The first matching condition is selected. Order conditions from most specific to least specific.

## 7. DataFrame.assign

`assign` returns a DataFrame with new or updated columns:

```python
result = df.assign(
    Average=lambda x: x["Total"] / 2
)
```

This can make transformation pipelines easier to chain without repeatedly assigning intermediate variables.

## 8. When to use each tool

| Tool | Best suited for |
|---|---|
| `map` | Map Series values through a dictionary/function |
| `Series.apply` | Flexible Series-level Python function |
| `DataFrame.apply` | Function along rows or columns |
| Vectorized operations | Arithmetic and comparisons over columns |
| `np.where` / `np.select` | Conditional output arrays |
| `assign` | Add or update columns in a pipeline |

## 9. Common mistakes

- Using row-wise apply for simple addition or multiplication.
- Forgetting that `map` can create missing values for unmapped categories.
- Confusing `axis=0` and `axis=1`.
- Writing conditions in the wrong order in `np.select`.
- Assuming every custom Python function is automatically vectorized.

## 10. Practice

1. Map letter grades to numeric points.
2. Write a function to classify marks using Series.apply.
3. Create a total column using vectorized addition.
4. Use np.where to create a pass/fail column.
5. Use np.select for three grade bands.
6. Compare a row-wise apply expression with a vectorized expression on a larger DataFrame.

**Checkpoint:** Prefer built-in vectorized operations when they express the task clearly; use apply when you genuinely need a custom function.
