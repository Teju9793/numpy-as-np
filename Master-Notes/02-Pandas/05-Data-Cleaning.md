# 05 — Data Cleaning with Pandas

> **Goal:** Detect and correct common data-quality problems without accidentally destroying useful information.

## 1. What is data cleaning?

Real-world data may contain inconsistent spelling, extra spaces, duplicated records, incorrect values, wrong data types and missing entries. **Data cleaning** is the process of finding and handling these issues before analysis.

Always inspect first. Do not delete rows just because they look unusual.

## 2. Start with a sample dataset

```python
import pandas as pd

df = pd.DataFrame({
    "Name": [" Asha ", "RAVI", "Maya", "Maya"],
    "Age": [19, 20, None, None],
    "Department": ["CSE", "cse", "ECE", "ECE"],
    "Marks": [85, 72, 91, 91]
})
```

## 3. Remove unwanted spaces

```python
df["Name"] = df["Name"].str.strip()
```

- `strip()`: removes spaces at both ends.
- `lstrip()`: removes spaces from the left.
- `rstrip()`: removes spaces from the right.

This avoids treating "Asha" and " Asha " as different categories.

## 4. Standardize text case

```python
df["Name"] = df["Name"].str.title()
df["Department"] = df["Department"].str.upper()
```

Other common string methods include `lower()`, `upper()`, `capitalize()`, `replace()` and `contains()`. Use them through the Series string accessor `.str`.

## 5. Replace inconsistent values

```python
df["Department"] = df["Department"].replace({
    "COMPUTER SCIENCE": "CSE",
    "CS": "CSE"
})
```

Replacement is useful for standardizing known variations. First inspect actual unique values so you do not replace a legitimate category by mistake.

## 6. Detect duplicate rows

```python
df.duplicated()
df.duplicated().sum()
```

To remove duplicate rows:

```python
clean = df.drop_duplicates()
```

By default, Pandas considers all columns when checking duplicates and keeps the first occurrence. You can use `subset=["Name", "Department"]` to check selected columns and `keep="last"` to keep the last occurrence.

Before dropping duplicates, decide what makes a record genuinely duplicate. Two people can share the same name.

## 7. Rename columns

```python
df = df.rename(columns={
    "Name": "student_name",
    "Marks": "score"
})
```

Clear and consistent column names make code easier to read. You can also standardize all names using string operations on `df.columns`.

## 8. Remove irrelevant columns or rows

```python
df = df.drop(columns=["Age"])
df = df.drop(index=[0])
```

`drop` returns a new object by default. Assign the result if you want to keep the change.

## 9. Correct invalid values

Suppose marks must be between 0 and 100:

```python
invalid = df[~df["Marks"].between(0, 100)]
print(invalid)
```

Do not automatically replace invalid values. Find the source of the problem, then decide whether to correct, mark as missing or remove the record.

## 10. Build a cleaning pipeline

```python
df["Name"] = df["Name"].str.strip().str.title()
df["Department"] = df["Department"].str.strip().str.upper()
df = df.drop_duplicates()
```

This is a small example. For larger projects, document each cleaning decision and keep the raw data unchanged.

## 11. Common mistakes

- Removing duplicates without deciding what defines a duplicate.
- Replacing categories before inspecting their unique values.
- Deleting unusual values without checking whether they are valid outliers.
- Forgetting to assign the result of `drop` or `rename`.
- Cleaning the original raw file rather than preserving an untouched copy.

## 12. Practice

Create a DataFrame with inconsistent spaces, text case, duplicate rows and invalid marks. Clean the text, identify duplicates, standardize categories and flag invalid marks. Explain every change you make.

**Checkpoint:** A good cleaning step should have a reason. Never clean data only to make the table look neat.
