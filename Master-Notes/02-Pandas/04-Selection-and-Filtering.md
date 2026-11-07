# 04 — Selecting and Filtering Data in Pandas

> **Goal:** Select columns, rows and cells using labels, positions and conditions.

## 1. Start with a small DataFrame

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["Asha", "Ravi", "Maya", "John"],
    "Department": ["CSE", "ECE", "CSE", "ISE"],
    "Marks": [85, 72, 91, 65]
}, index=["S1", "S2", "S3", "S4"])
```

## 2. Select columns

```python
df["Name"]                  # one Series
df[["Name", "Marks"]]       # DataFrame with two columns
```

Use double brackets when you want to preserve a DataFrame result.

## 3. loc — label-based selection

`loc` selects by row and column labels:

```python
print(df.loc["S1"])
print(df.loc["S1", "Marks"])   # 85
print(df.loc["S1":"S3", ["Name", "Marks"]])
```

Important: label slices with `loc` include the ending label when it exists. This differs from ordinary Python slicing.

## 4. iloc — position-based selection

`iloc` selects by integer position:

```python
print(df.iloc[0])       # first row
print(df.iloc[0, 2])    # first row, third column
print(df.iloc[0:2, 0:2])
```

Ordinary positional slicing excludes the stop position, like Python lists.

## 5. loc versus iloc

| | loc | iloc |
|---|---|---|
| Selects by | Labels | Integer positions |
| Row example | `loc["S1"]` | `iloc[0]` |
| Column example | `loc[:, "Marks"]` | `iloc[:, 2]` |
| Slice stop | Included for label slices | Excluded |

Memory trick: **loc = label**, **iloc = integer location**.

## 6. Filter rows using one condition

```python
print(df[df["Marks"] >= 80])
```

The expression `df["Marks"] >= 80` creates a Boolean Series. Passing it to the DataFrame selects rows where the condition is True.

## 7. Combine multiple conditions

Use `&` for AND and `|` for OR. Put each comparison in parentheses.

```python
high_cse = df[(df["Department"] == "CSE") & (df["Marks"] >= 80)]
print(high_cse)
```

Do not use Python's `and` and `or` between Pandas Series.

## 8. Use isin for a list of categories

```python
selected = df[df["Department"].isin(["CSE", "ISE"])]
```

This is clearer than writing several OR conditions when you want to match one of many values.

## 9. Use between for ranges

```python
middle_scores = df[df["Marks"].between(70, 90)]
```

By default, both boundaries are included. You can control inclusivity with the `inclusive` parameter.

## 10. Query method

```python
result = df.query("Marks >= 80 and Department == 'CSE'")
```

`query()` can make some filters easier to read. For dynamic or untrusted input, be careful about expression construction; ordinary Boolean indexing is often clearer and safer.

## 11. Select rows with missing values

```python
df[df["Marks"].isna()]
df[df["Marks"].notna()]
```

Use `isna()` and `notna()` rather than comparing a value to NaN using equality.

## 12. Common mistakes

- Confusing labels with positions.
- Forgetting that `loc` label slices include the end label.
- Forgetting parentheses around each condition.
- Using `and` instead of `&`.
- Using `== np.nan` instead of `isna()`.
- Selecting one column when a two-dimensional DataFrame is required.

## 13. Practice

1. Select the Name column.
2. Select Name and Marks together.
3. Use `loc` to select student S2's marks.
4. Use `iloc` to select the first two rows.
5. Filter students scoring at least 80.
6. Filter CSE and ISE students.
7. Select scores between 70 and 90.

**Checkpoint:** Before writing a selection, decide whether you are selecting by a label, a position, or a condition.
