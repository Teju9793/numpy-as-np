# 03 — Reading and Inspecting Data

> **Goal:** Load data from files, understand common read options and inspect a dataset before analysis.

## 1. Why loading data is a skill

In practical data science, data usually comes from a CSV, Excel workbook, database or another system—not from a Python dictionary you typed manually. Reading a file correctly is the first step in analysis.

Start with:

```python
import pandas as pd
```

## 2. Read a CSV file

```python
df = pd.read_csv("students.csv")
print(df.head())
```

Pandas reads the file and creates a DataFrame. The path may be relative to the current working directory or an absolute path.

Common parameters:
- `filepath_or_buffer`: file path or supported file-like object.
- `sep`: delimiter, default comma.
- `header`: row used as column names.
- `names`: custom column names.
- `index_col`: column to use as row index.
- `usecols`: columns to read.
- `dtype`: requested column types.
- `na_values`: extra strings to interpret as missing values.
- `parse_dates`: columns to parse as dates.

## 3. Read a file with a different separator

A tab-separated file:

```python
df = pd.read_csv("students.tsv", sep="\t")
```

A semicolon-separated file:

```python
df = pd.read_csv("students.csv", sep=";")
```

If the separator is wrong, the entire row may appear in one column. Always inspect `df.head()` and `df.columns` after loading.

## 4. Read selected columns

```python
df = pd.read_csv("students.csv", usecols=["Name", "Marks"])
```

This can reduce memory use and make processing faster when a large file contains many irrelevant columns.

## 5. Read Excel files

```python
df = pd.read_excel("students.xlsx", sheet_name="Sheet1")
```

You may need an Excel engine package installed, depending on the file type and environment. To inspect available sheets, use `pd.ExcelFile(path).sheet_names`.

## 6. Inspect the first and last rows

```python
df.head()       # first 5 rows by default
df.head(10)     # first 10 rows
df.tail()       # last 5 rows
df.sample(5)    # 5 random rows
```

A random sample can reveal issues that are not visible at the top of a file.

## 7. Understand the structure

```python
df.shape
df.columns
df.index
df.dtypes
df.info()
```

Interpretation:
- `shape`: rows and columns.
- `columns`: column names.
- `index`: row labels.
- `dtypes`: data type per column.
- `info()`: non-null counts, dtypes and memory estimate.

## 8. Summary statistics

```python
df.describe()
df.describe(include="all")
```

By default, `describe()` summarizes numeric columns. `include="all"` requests summaries for other types too, though the statistics differ by dtype.

For numeric columns, common values include count, mean, standard deviation, minimum, quartiles and maximum.

## 9. Check missing values and duplicates

```python
df.isna().sum()
df.duplicated().sum()
```

These are diagnostic steps, not automatic cleaning. A duplicate row may be valid in some datasets; missing values may have a meaningful reason.

## 10. Check unique values

```python
df["Department"].unique()
df["Department"].nunique()
df["Department"].value_counts()
```

- `unique()`: distinct values.
- `nunique()`: count of distinct non-missing values by default.
- `value_counts()`: frequency of each value.

This is useful for checking spelling inconsistencies such as "CSE", "cse" and "Computer Science".

## 11. Common mistakes

- Using the wrong file path or working directory.
- Forgetting the separator.
- Assuming the first row is always a header.
- Assuming dates are automatically parsed exactly as needed.
- Starting analysis without checking dtypes, missing values and duplicate rows.

## 12. A reliable loading checklist

1. Load a small preview or the full file.
2. Inspect the first and last rows.
3. Check shape and column names.
4. Check data types.
5. Check missing values and duplicates.
6. Inspect category values and summary statistics.
7. Only then begin cleaning and analysis.

## 13. Practice

Read a CSV file and answer:
1. How many rows and columns are present?
2. Which columns are numeric?
3. Which columns contain missing values?
4. Which category values exist?
5. Are there duplicated rows?
6. Do the summary statistics look reasonable?

**Checkpoint:** Never assume a dataset is clean just because `read_csv` completed without an error.
