# 07 — Pandas Data Types and Conversion

> **Goal:** Inspect column types, convert values safely and understand why incorrect dtypes cause analysis problems.

## 1. Why data types matter

A column containing numbers may be stored as text. If you calculate with it, the result may be wrong or the operation may fail.

Example: values `"100"`, `"200"` and `"300"` look numeric but are strings. A reliable workflow checks dtypes before analysis.

## 2. Inspect dtypes

```python
import pandas as pd

df = pd.DataFrame({
    "Age": [18, 19, 20],
    "Marks": [75.5, 80.0, 92.5],
    "Name": ["Asha", "Ravi", "Maya"]
})
print(df.dtypes)
```

Common types include integer, floating point, Boolean, string/object, datetime and categorical.

## 3. Convert with astype

```python
df["Age"] = df["Age"].astype("int64")
df["Name"] = df["Name"].astype("string")
```

Use `astype` when the values can be converted safely. A non-numeric string cannot be converted directly to an integer.

## 4. Convert text to numbers with to_numeric

```python
df = pd.DataFrame({"Marks": ["80", "90", "not entered", "75"]})
df["Marks"] = pd.to_numeric(df["Marks"], errors="coerce")
print(df)
```

`errors="coerce"` converts invalid values to missing values (NaN). This is useful when you plan to inspect and handle invalid entries.

Other options:
- `errors="raise"`: raise an error for invalid values (default).
- `errors="ignore"`: deprecated in recent Pandas versions; avoid relying on it.

## 5. Convert values to dates

```python
df = pd.DataFrame({"Date": ["2026-01-10", "2026-02-15"]})
df["Date"] = pd.to_datetime(df["Date"])
print(df.dtypes)
```

If the source uses a known format, specify it:

```python
pd.to_datetime(df["Date"], format="%d-%m-%Y", errors="coerce")
```

This avoids ambiguous date interpretation. Use `errors="coerce"` to turn invalid dates into `NaT` (Not a Time).

## 6. Nullable integer types

Ordinary NumPy integer dtypes cannot represent NaN. Pandas provides nullable integer types such as `Int64` (capital I):

```python
s = pd.Series([1, 2, None], dtype="Int64")
print(s)
```

This preserves integer values while allowing missing entries represented by `<NA>`.

## 7. Category dtype

For repeated labels such as department names:

```python
df["Department"] = df["Department"].astype("category")
```

Categorical dtype can save memory and preserve category information for suitable columns. It is especially useful for repeated, limited sets of labels, not arbitrary free-form text.

## 8. Check values before and after conversion

```python
print(df["Marks"].unique())
print(df["Marks"].dtype)
```

After conversion, check how many values became missing:

```python
df["Marks"].isna().sum()
```

Never assume conversion succeeded exactly as intended.

## 9. Common mistakes

- Using `astype(int)` on strings containing invalid entries.
- Converting dates with an ambiguous day/month order.
- Forgetting to inspect values coerced to missing.
- Confusing Pandas nullable `Int64` with NumPy `int64`.
- Treating category dtype as a replacement for every string column.

## 10. Practice

Create columns containing numeric strings, invalid numeric text and dates. Convert each column appropriately, inspect the resulting dtypes, and count invalid values that became missing.

**Checkpoint:** Choose `astype` for straightforward known conversions, `to_numeric` for messy numeric text and `to_datetime` for dates.
