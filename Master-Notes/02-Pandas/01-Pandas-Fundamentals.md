# 01 — Pandas Fundamentals

> **Goal:** Understand what Pandas does, why it is useful after NumPy, and how tabular data is represented.

## 1. Why do we need Pandas?

NumPy is excellent for numerical arrays. But real datasets often contain column names, dates, text, missing values and different types of information in the same table.

Imagine a student dataset:

| Name | Age | Marks | Department |
|---|---:|---:|---|
| Asha | 19 | 85 | CSE |
| Ravi | 20 | 72 | ECE |
| Maya | 19 | 91 | CSE |

You want to select only CSE students, calculate average marks, fill missing values and combine data from another table. Pandas is designed to make these data-analysis tasks convenient.

## 2. What is Pandas?

**Pandas** is a Python library for data manipulation and analysis. Its two main data structures are:
- **Series:** a one-dimensional labeled collection.
- **DataFrame:** a two-dimensional labeled table with rows and columns.

Import it using the common alias:

```python
import pandas as pd
```

The alias `pd` is a convention used in most Pandas examples.

## 3. Create a DataFrame

```python
import pandas as pd

data = {
    "Name": ["Asha", "Ravi", "Maya"],
    "Age": [19, 20, 19],
    "Marks": [85, 72, 91]
}

df = pd.DataFrame(data)
print(df)
```

Output:
```text
   Name  Age  Marks
0  Asha   19     85
1  Ravi   20     72
2  Maya   19     91
```

Explanation:
- Dictionary keys become column names.
- Each list supplies the values for that column.
- Pandas creates a row index automatically: 0, 1, 2.

## 4. What is an index?

An index labels rows. By default, Pandas creates a RangeIndex starting at 0, but you can use meaningful labels.

```python
df = pd.DataFrame(
    {"Marks": [85, 72, 91]},
    index=["S01", "S02", "S03"]
)
print(df)
```

An index is not necessarily a unique student ID unless you enforce that rule. It is a row label used for selection and alignment.

## 5. Series versus DataFrame

| Feature | Series | DataFrame |
|---|---|---|
| Dimensions | 1-D | 2-D |
| Concept | One labeled column | Labeled table |
| Labels | Index | Row index and column labels |
| Example | Marks column | Student table |

Selecting one column usually returns a Series:

```python
marks = df["Marks"]
print(type(marks))
```

Selecting it with double brackets returns a DataFrame:

```python
marks_table = df[["Marks"]]
print(type(marks_table))
```

This small difference matters because downstream operations may expect a 1-D Series or a 2-D DataFrame.

## 6. Create a Series

```python
marks = pd.Series([85, 72, 91], index=["Asha", "Ravi", "Maya"], name="Marks")
print(marks)
```

A Series contains values plus an index. You can think of it as one labeled column.

## 7. Pandas and NumPy relationship

Pandas is built to work naturally with NumPy and the wider Python data ecosystem. Numeric columns can be converted to NumPy arrays:

```python
marks = df["Marks"].to_numpy()
print(marks)
```

But do not assume every DataFrame is a single homogeneous NumPy matrix: different columns may have different data types.

## 8. A first inspection routine

```python
print(df.head())
print(df.shape)
print(df.columns)
print(df.index)
print(df.dtypes)
print(df.info())
print(df.describe())
```

What each tells you:
- `head()`: first rows.
- `shape`: (number of rows, number of columns).
- `columns`: column labels.
- `index`: row labels.
- `dtypes`: data type of each column.
- `info()`: concise structure, non-null counts and memory information.
- `describe()`: summary statistics for applicable columns.

## 9. Why Pandas is important for ML

A common ML workflow is:
1. Load a CSV file into a DataFrame.
2. Inspect rows, columns and data types.
3. Handle missing values and duplicates.
4. Select useful features.
5. Convert categorical values into model-ready numbers.
6. Separate features and target.
7. Pass the prepared data to a machine-learning library.

Pandas helps with the data preparation before model training.

## 10. Common beginner mistakes

- Confusing a Series with a DataFrame.
- Assuming the index is always a unique ID.
- Forgetting that `df.shape` returns (rows, columns).
- Treating all columns as numeric.
- Using `print(df.info())`: `info()` prints its report and returns None, so this can display an extra None.

## 11. Practice

1. Create a DataFrame with Name, Age and Marks for five students.
2. Print its shape, columns, index and dtypes.
3. Select the Marks column and check its type.
4. Select Marks using double brackets and compare the result.
5. Convert the Marks Series to a NumPy array.

**Checkpoint:** Explain the difference between a Series, a DataFrame and an index before continuing.
