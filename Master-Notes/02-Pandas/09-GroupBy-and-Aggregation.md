# 09 — GroupBy and Aggregation in Pandas

> **Goal:** Split data into groups, calculate summaries and understand the split–apply–combine pattern.

## 1. Why group data?

Suppose a sales table contains thousands of transactions. You may want total sales per city, average order value per product or number of orders per month. Instead of writing loops for each group, Pandas provides `groupby`.

## 2. Sample dataset

```python
import pandas as pd

df = pd.DataFrame({
    "City": ["Bengaluru", "Tumkur", "Bengaluru", "Tumkur", "Mysuru"],
    "Product": ["Book", "Pen", "Pen", "Book", "Book"],
    "Sales": [500, 100, 200, 300, 400]
})
```

## 3. Understand split–apply–combine

1. **Split:** divide rows into groups using one or more keys.
2. **Apply:** calculate something for each group.
3. **Combine:** assemble the results into a Series or DataFrame.

```python
result = df.groupby("City")["Sales"].sum()
print(result)
```

The result contains the total Sales for each City.

## 4. Common aggregation functions

```python
df.groupby("City")["Sales"].sum()
df.groupby("City")["Sales"].mean()
df.groupby("City")["Sales"].count()
df.groupby("City")["Sales"].min()
df.groupby("City")["Sales"].max()
df.groupby("City")["Sales"].median()
```

- `sum`: total.
- `mean`: average.
- `count`: non-missing values.
- `size`: number of rows in each group, including rows where selected values are missing.
- `min` / `max`: extremes.

## 5. Group by multiple columns

```python
df.groupby(["City", "Product"])["Sales"].sum()
```

This creates groups for each City–Product combination.

## 6. Aggregate multiple statistics

```python
summary = df.groupby("City")["Sales"].agg(["sum", "mean", "count"])
print(summary)
```

You can rename the output columns with named aggregation:

```python
summary = df.groupby("City").agg(
    total_sales=("Sales", "sum"),
    average_sales=("Sales", "mean"),
    transactions=("Sales", "size")
)
```

Named aggregation makes the output easier to understand.

## 7. Aggregate multiple columns

```python
df.groupby("City").agg({
    "Sales": ["sum", "mean"],
    "Product": "count"
})
```

Different columns can use different aggregation functions. Inspect the resulting column labels because multiple aggregations can create a MultiIndex on columns.

## 8. Transform — return values aligned to original rows

Aggregation reduces each group to a summary. `transform` returns a result aligned to the original DataFrame's rows.

```python
df["City_total"] = df.groupby("City")["Sales"].transform("sum")
```

Each row receives the total sales for its city. This is useful for comparing a row with its group average or total.

## 9. Filter groups

```python
large_cities = df.groupby("City").filter(
    lambda group: group["Sales"].sum() >= 500
)
```

`filter` keeps or removes whole groups based on a condition.

## 10. Reset the index

```python
summary = df.groupby("City", as_index=False)["Sales"].sum()
```

Or call `reset_index()` after grouping. This turns group labels back into ordinary columns.

## 11. Common mistakes

- Confusing `count()` with `size()`.
- Expecting aggregation to preserve every original row.
- Forgetting that grouping keys often become the result index.
- Using `apply` when `agg` or `transform` is simpler.
- Grouping on inconsistent category spelling.

## 12. Practice

1. Calculate total sales per city.
2. Calculate average sales per product.
3. Group by city and product.
4. Return sum, mean and transaction count.
5. Add each city's total back to every original row using `transform`.
6. Keep only cities whose total sales exceed a chosen threshold.

**Checkpoint:** Decide whether you need one row per group (`agg`), one result per original row (`transform`) or whole groups selected by a rule (`filter`).
