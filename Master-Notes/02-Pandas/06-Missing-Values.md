# 06 — Handling Missing Values in Pandas

> **Goal:** Detect missing values, understand why they occur, and choose whether to remove or fill them.

## 1. What is a missing value?

A missing value means that a field has no recorded value. It may occur because a person skipped a question, a sensor failed, a value was not collected or two datasets did not match during a join.

Pandas commonly represents missing data with `NaN`, `None` or `pd.NA`, depending on the dtype.

## 2. Create a DataFrame with missing values

```python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "Name": ["Asha", "Ravi", "Maya", "John"],
    "Age": [19, np.nan, 20, np.nan],
    "Marks": [85, 72, np.nan, 90]
})
```

## 3. Detect missing values

```python
df.isna()
df.isnull()          # alias of isna()
df.isna().sum()      # missing count per column
df.isna().sum().sum()  # total missing cells
```

To find rows with at least one missing value:

```python
df[df.isna().any(axis=1)]
```

To find complete rows:

```python
df[df.notna().all(axis=1)]
```

## 4. Remove missing values with dropna

```python
df.dropna()
```

By default, rows containing at least one missing value are removed.

Useful options:
- `axis=0`: drop rows (default).
- `axis=1`: drop columns.
- `how="any"`: drop if any selected value is missing.
- `how="all"`: drop only if all selected values are missing.
- `subset=[...]`: check only specified columns.
- `thresh=n`: keep rows/columns with at least n non-missing values.

Example:

```python
df.dropna(subset=["Marks"])
```

This removes rows only when Marks is missing.

## 5. Fill missing values with fillna

A simple constant fill:

```python
df["Age"] = df["Age"].fillna(0)
```

But zero may be an incorrect age. Choose a fill value based on what the column means.

## 6. Mean, median and mode imputation

For a numerical column:

```python
df["Marks"] = df["Marks"].fillna(df["Marks"].median())
```

- **Mean:** useful for roughly symmetric numeric data without strong outliers.
- **Median:** often more robust when data is skewed or contains outliers.
- **Mode:** most frequent value; can be useful for categorical columns.

```python
df["Department"] = df["Department"].fillna(
    df["Department"].mode()[0]
)
```

Do not blindly fill every missing column with its mean. The choice depends on the meaning and distribution of the data.

## 7. Forward fill and backward fill

```python
df["Temperature"] = df["Temperature"].ffill()
df["Temperature"] = df["Temperature"].bfill()
```

- `ffill()`: use the previous valid value.
- `bfill()`: use the next valid value.

These can be useful for ordered time-series data, but they can be misleading if values change quickly or the order is not meaningful.

## 8. Interpolation

For numerical sequences where intermediate values are meaningful:

```python
df["Reading"] = df["Reading"].interpolate()
```

Interpolation estimates missing values from neighboring observations. Choose the interpolation method based on the data and time spacing.

## 9. Missing-value indicators

Sometimes the fact that a value was missing contains information. Create an indicator before filling:

```python
df["Age_was_missing"] = df["Age"].isna()
df["Age"] = df["Age"].fillna(df["Age"].median())
```

This lets a model or analysis distinguish original values from imputed values.

## 10. Avoid data leakage in ML

When preparing training and test data, calculate imputation values using the training set only. Then use the same learned values to fill both training and test data. Calculating the mean from the full dataset allows test information to influence training.

In scikit-learn projects, a preprocessing pipeline with an imputer is often a safer approach.

## 11. Common mistakes

- Treating zero or an empty string as automatically equivalent to missing.
- Dropping too many rows without checking how much data is lost.
- Using the mean for skewed data with strong outliers.
- Filling a time series without sorting by time.
- Calculating imputation statistics using test data.

## 12. Practice

1. Count missing values in each column.
2. Find all rows containing missing values.
3. Remove rows where a target column is missing.
4. Fill a numeric column using its median.
5. Fill a category using its mode.
6. Create a missingness indicator before filling.

**Checkpoint:** Explain why missing values exist and justify your chosen handling method.
