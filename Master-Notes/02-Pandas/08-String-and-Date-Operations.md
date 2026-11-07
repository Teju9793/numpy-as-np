# 08 — String and Date Operations in Pandas

> **Goal:** Clean text columns and extract useful information from date/time columns.

## 1. The .str accessor

Pandas provides vectorized string operations through `.str`. This lets you apply a string method to every value in a Series.

```python
import pandas as pd

names = pd.Series([" Asha ", "RAVI", "maya"])
print(names.str.strip())
# 0    Asha
# 1    RAVI
# 2    maya
```

The values should be string-like. Missing values are generally preserved as missing.

## 2. Common string methods

```python
s = pd.Series([" Data Science ", "machine learning", "PYTHON"])

s.str.strip()       # remove surrounding whitespace
s.str.lower()       # lowercase
s.str.upper()       # uppercase
s.str.title()       # title case
s.str.replace(" ", "_", regex=False)
s.str.len()         # string length
```

Use `regex=False` when you want literal text replacement rather than a regular expression.

## 3. Search within text

```python
emails = pd.Series(["a@example.com", "b@gmail.com", "c@example.com"])
mask = emails.str.contains("example", case=False, na=False)
print(emails[mask])
```

- `case=False`: ignore upper/lowercase differences.
- `na=False`: treat missing entries as not matching.

You can also use `str.startswith()` and `str.endswith()`.

## 4. Split text into parts

```python
names = pd.Series(["Asha Kumar", "Ravi Rao"])
parts = names.str.split(" ", expand=True)
print(parts)
```

With `expand=True`, the pieces are returned as separate columns. This is useful for parsing names or structured text, but check for missing or multi-part values.

## 5. Extract with regular expressions

```python
codes = pd.Series(["ID-102", "ID-205", "XX-300"])
numbers = codes.str.extract(r"(\d+)")
print(numbers)
```

The expression `\d+` means one or more digits. Regex is powerful, but always test it on representative examples.

## 6. Convert to datetime

```python
df = pd.DataFrame({
    "Date": ["2026-01-10", "2026-02-15", "2026-03-20"]
})
df["Date"] = pd.to_datetime(df["Date"])
```

A proper datetime dtype enables date-aware sorting, filtering and calculations.

## 7. Extract date components with .dt

```python
df["Year"] = df["Date"].dt.year
df["Month"] = df["Date"].dt.month
df["Day"] = df["Date"].dt.day
df["Weekday"] = df["Date"].dt.day_name()
```

The `.dt` accessor is used for datetime-like Series, just as `.str` is used for strings.

## 8. Filter by date range

```python
start = "2026-02-01"
end = "2026-02-28"

february = df[df["Date"].between(start, end)]
```

For timestamps that include time-of-day, be clear about whether the ending boundary includes the whole final day. An exclusive next-day boundary is often safer for timestamp filtering.

## 9. Date differences

```python
df["Days_since"] = (pd.Timestamp("2026-04-01") - df["Date"]).dt.days
```

Datetime subtraction produces a Timedelta. The `.dt.days` accessor extracts the whole-day component.

## 10. Resampling time series

When a datetime column is the index, `resample` groups observations into time intervals:

```python
daily = df.set_index("Date").resample("MS").size()
```

Here `MS` means month start. Resampling is useful for monthly, weekly or daily summaries. The appropriate frequency depends on the question and Pandas version's supported frequency aliases.

## 11. Common mistakes

- Calling ordinary Python string methods directly on a Series instead of using `.str`.
- Forgetting `na=False` when missing strings should not match.
- Using `.dt` before converting the column to datetime.
- Misreading dates where day and month order is ambiguous.
- Filtering timestamps without considering the time portion.
- Applying a regex without testing its matching behavior.

## 12. Practice

1. Remove extra spaces from a name column.
2. Convert all department names to uppercase.
3. Find email addresses containing a chosen domain.
4. Split full names into separate columns.
5. Convert a date column to datetime.
6. Extract year, month and weekday.
7. Filter records from one month.

**Checkpoint:** Use `.str` for text, `.dt` for dates and inspect the dtype before applying either accessor.
