# 15 — Pandas Practical Examples with Outputs

> 🟢 **DATA CLEANING LAB** · The Pandas operations used repeatedly in real data analysis and ML preparation.

## 1. Create and inspect a DataFrame

~~~python
import pandas as pd
import numpy as np

df = pd.DataFrame({
    "Name": ["Asha", "Ravi", "Meena", "Arun", "John"],
    "Hours": [2, 4, 5, 1, 3],
    "Attendance": [70, 85, 90, 60, 75],
    "Marks": [45, 68, 82, 35, 58],
    "Department": ["CSE", "ECE", "CSE", "ECE", "CSE"]
})

print(df.head(3))
print(df.shape)
~~~

**Output**

| | Name | Hours | Attendance | Marks | Department |
|---:|---|---:|---:|---:|---|
| 0 | Asha | 2 | 70 | 45 | CSE |
| 1 | Ravi | 4 | 85 | 68 | ECE |
| 2 | Meena | 5 | 90 | 82 | CSE |

~~~text
(5, 5)
~~~

Five rows and five columns. Use head, shape, info, describe and dtypes before modifying data.

## 2. Select columns and filter rows

~~~python
print(df[df["Marks"] >= 60][["Name", "Marks"]])
~~~

**Output**

| | Name | Marks |
|---:|---|---:|
| 1 | Ravi | 68 |
| 2 | Meena | 82 |

The condition creates a Boolean mask. Only rows where it is True are returned.

## 3. Handle missing values

~~~python
data = pd.DataFrame({
    "Hours": [2, 4, np.nan, 6],
    "Marks": [40, np.nan, 70, 90]
})
print(data.isna().sum())
~~~

**Output**

~~~text
Hours    1
Marks    1
dtype: int64
~~~

Fill each column with its mean:

~~~python
data["Hours"] = data["Hours"].fillna(data["Hours"].mean())
data["Marks"] = data["Marks"].fillna(data["Marks"].mean())
print(data.round(2))
~~~

**Output**

| | Hours | Marks |
|---:|---:|---:|
| 0 | 2.00 | 40.00 |
| 1 | 4.00 | 66.67 |
| 2 | 4.00 | 70.00 |
| 3 | 6.00 | 90.00 |

**ML warning:** learn imputation values from training data only. Do not calculate them from the full dataset before splitting.

## 4. loc versus iloc

~~~python
print(df.loc[1, "Name"])
print(df.iloc[0:2, 0:3])
~~~

**Output**

~~~text
Ravi
~~~

| | Name | Hours | Attendance |
|---:|---|---:|---:|
| 0 | Asha | 2 | 70 |
| 1 | Ravi | 4 | 85 |

loc is label-based. iloc is integer-position-based.

## 5. GroupBy: compare departments

~~~python
print(df.groupby("Department")["Marks"].mean())
~~~

**Output**

~~~text
Department
CSE    61.666667
ECE    51.500000
Name: Marks, dtype: float64
~~~

GroupBy splits rows into groups, calculates within each group and combines the results.

## 6. Create a feature

~~~python
df["Performance"] = np.where(
    df["Marks"] >= 60, "Good", "Needs Improvement"
)
print(df[["Name", "Marks", "Performance"]])
~~~

**Output**

| Name | Marks | Performance |
|---|---:|---|
| Asha | 45 | Needs Improvement |
| Ravi | 68 | Good |
| Meena | 82 | Good |
| Arun | 35 | Needs Improvement |
| John | 58 | Needs Improvement |

Feature engineering creates useful input columns from existing information.

## 7. Sort and select top records

~~~python
print(df.sort_values("Marks", ascending=False)[["Name", "Marks"]].head(3))
~~~

**Output**

| | Name | Marks |
|---:|---|---:|
| 2 | Meena | 82 |
| 1 | Ravi | 68 |
| 4 | John | 58 |

## 8. Encode a categorical feature

~~~python
encoded = pd.get_dummies(df, columns=["Department"], dtype=int)
print(encoded[["Department_CSE", "Department_ECE"]])
~~~

**Output**

| | Department_CSE | Department_ECE |
|---:|---:|---:|
| 0 | 1 | 0 |
| 1 | 0 | 1 |
| 2 | 1 | 0 |
| 3 | 0 | 1 |
| 4 | 1 | 0 |

One-hot encoding creates indicator columns. For production ML, prefer a fitted encoder inside a scikit-learn Pipeline to handle train/test consistency and unseen categories.

## 9. Separate features and target

~~~python
X = df[["Hours", "Attendance"]]
y = df["Marks"]

print("X shape:", X.shape)
print("y shape:", y.shape)
~~~

**Output**

~~~text
X shape: (5, 2)
y shape: (5,)
~~~

X contains model inputs. y contains the value to predict. Never include the target inside X.

## 10. ML dataset inspection routine

~~~python
print("Shape:", df.shape)
print("Missing values:\n", df.isna().sum())
print("Duplicate rows:", df.duplicated().sum())
print(df.describe())
~~~

This compact routine helps you understand a dataset before cleaning or modeling.

## Quick revision

| Task | Pandas code |
|---|---|
| First rows | df.head() |
| Dimensions | df.shape |
| Data types | df.dtypes |
| Missing values | df.isna().sum() |
| Duplicate rows | df.drop_duplicates() |
| Filter rows | df[df["Marks"] > 60] |
| Group and calculate | df.groupby("Department")["Marks"].mean() |
| Sort | df.sort_values("Marks") |
| Encode categories | pd.get_dummies(df) |
| Separate X and y | X = df[features]; y = df[target] |

**Practice:** Load a student CSV, inspect it, handle missing values, filter high scores, calculate department averages, create a pass/fail feature and separate X and y.

**ML connection:** Pandas prepares real-world tabular data before it reaches a machine-learning model.
