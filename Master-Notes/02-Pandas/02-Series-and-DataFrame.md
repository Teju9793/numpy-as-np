# 02 — Series and DataFrame in Detail

> **Goal:** Build Series and DataFrames from common Python objects, understand labels and inspect their structure.

## 1. Series: one labeled dimension

A Series is a one-dimensional collection of values with an index.

```python
import pandas as pd

marks = pd.Series([80, 90, 75], index=["Asha", "Ravi", "Maya"])
print(marks)
```

Output:
```text
Asha    80
Ravi    90
Maya    75
dtype: int64
```

The left side contains index labels; the right side contains values.

## 2. Create Series in different ways

From a list:
```python
pd.Series([10, 20, 30])
```

From a dictionary (keys become index labels):
```python
pd.Series({"Math": 90, "Python": 85, "AI": 95})
```

With a custom index:
```python
pd.Series([10, 20], index=["first", "second"])
```

## 3. DataFrame: a table of labeled columns

```python
students = pd.DataFrame({
    "Name": ["Asha", "Ravi", "Maya"],
    "Age": [19, 20, 19],
    "Marks": [80, 90, 75]
})
print(students)
```

Each column has its own name and dtype. A DataFrame can contain numerical, text, Boolean, date and other data types in different columns.

## 4. Create a DataFrame from a list of dictionaries

```python
records = [
    {"Name": "Asha", "Marks": 80},
    {"Name": "Ravi", "Marks": 90},
    {"Name": "Maya", "Marks": 75}
]
df = pd.DataFrame(records)
print(df)
```

Each dictionary describes one row. If a key is absent in one record, Pandas fills that position with a missing value.

## 5. Understand index and columns

```python
print(df.index)
print(df.columns)
print(df.values)
```

- `index`: row labels.
- `columns`: column labels.
- `values`: underlying values as an array-like representation.

For mixed dtypes, `df.to_numpy()` may produce an object array or a common dtype. Prefer selecting a specific numeric column if you need a clean numeric NumPy array.

## 6. Select a Series or DataFrame

```python
df["Marks"]       # Series
df[["Marks"]]     # DataFrame
df[["Name", "Marks"]]  # DataFrame with two columns
```

The number of square brackets changes the output type:
- one column label in one bracket -> Series,
- a list of labels inside brackets -> DataFrame.

## 7. Set and reset an index

```python
df = df.set_index("Name")
print(df)
```

The Name column becomes the row index. By default, it is removed from the ordinary columns.

Restore a default integer index:

```python
df = df.reset_index()
```

Use `drop=True` if you want to discard the old index instead of adding it as a column.

## 8. DataFrame shape and dimensions

```python
print(df.shape)  # (rows, columns)
print(df.ndim)   # 2
print(df.size)   # rows * columns
```

A DataFrame with 5 rows and 3 columns has shape `(5, 3)` and 15 total cells.

## 9. Data types

```python
print(df.dtypes)
```

A DataFrame does not have one universal dtype. Each column can have its own dtype. Use `astype()` to convert a column when the conversion is valid.

## 10. Copying a DataFrame

```python
copy_df = df.copy()
```

A copy is useful when you want to experiment without modifying the original DataFrame. Pandas has different copy/view behaviors depending on the operation and version; use explicit copies when independent data is important.

## 11. Common mistakes

- Expecting `df["col"]` and `df[["col"]]` to have the same type.
- Assuming dictionary keys always become columns when the data is shaped differently.
- Forgetting that `set_index` returns a new DataFrame unless assigned or used with an in-place option.
- Treating `values` as guaranteed to preserve every original column dtype.
- Assuming an index must be unique.

## 12. Practice

1. Create a Series of five subject marks with subject names as index.
2. Create a DataFrame from a dictionary of lists.
3. Create the same table from a list of dictionaries.
4. Select one column as a Series and as a DataFrame.
5. Set a student ID column as the index and reset it.

**Checkpoint:** You should be able to choose the correct structure for one column versus a full table.
