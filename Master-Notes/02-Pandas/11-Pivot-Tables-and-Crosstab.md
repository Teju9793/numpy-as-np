# 11 — Pivot Tables and Crosstab in Pandas

> **Goal:** Summarize data across categories using pivot tables and frequency tables.

## 1. Why pivot tables?

A long transaction table may contain one row per sale. You may want a compact report showing total sales by city and product. A pivot table turns row-level records into a summary matrix.

## 2. Sample data

```python
import pandas as pd

df = pd.DataFrame({
    "City": ["Bengaluru", "Bengaluru", "Tumkur", "Tumkur", "Mysuru"],
    "Product": ["Book", "Pen", "Book", "Pen", "Book"],
    "Sales": [500, 200, 300, 100, 400]
})
```

## 3. Create a pivot table

```python
table = pd.pivot_table(
    df,
    values="Sales",
    index="City",
    columns="Product",
    aggfunc="sum"
)
print(table)
```

Meaning of parameters:
- `data`: source DataFrame.
- `values`: values to summarize.
- `index`: categories displayed as rows.
- `columns`: categories displayed as columns.
- `aggfunc`: calculation, such as sum, mean or count.

## 4. Change the aggregation

```python
pd.pivot_table(
    df,
    values="Sales",
    index="City",
    columns="Product",
    aggfunc="mean"
)
```

The same layout can show average sales rather than total sales.

## 5. Handle missing combinations

Not every city may sell every product. A pivot table can contain missing cells for combinations with no records.

```python
pd.pivot_table(
    df,
    values="Sales",
    index="City",
    columns="Product",
    aggfunc="sum",
    fill_value=0
)
```

Use `fill_value=0` only if an absent combination should logically be represented as zero. Missing data and a true zero are not always the same thing.

## 6. Add margins

```python
pd.pivot_table(
    df,
    values="Sales",
    index="City",
    columns="Product",
    aggfunc="sum",
    margins=True
)
```

Margins add row and column totals, commonly labeled "All".

## 7. Crosstab — frequency counts

`pd.crosstab` counts combinations of categories:

```python
students = pd.DataFrame({
    "Department": ["CSE", "CSE", "ECE", "ECE", "CSE"],
    "Result": ["Pass", "Fail", "Pass", "Pass", "Pass"]
})

print(pd.crosstab(students["Department"], students["Result"]))
```

Rows represent Department, columns represent Result, and each cell counts observations.

## 8. Normalize crosstab

```python
pd.crosstab(
    students["Department"],
    students["Result"],
    normalize="index"
)
```

This shows row-wise proportions. Other normalization choices include columns or the whole table. Use percentages when comparing groups of different sizes.

## 9. Pivot versus pivot_table

- `pivot()` reshapes data and requires each index/column combination to identify one value. It does not aggregate duplicates.
- `pivot_table()` can aggregate multiple rows for the same combination using `aggfunc`.

If duplicate combinations exist, `pivot_table` is usually the appropriate summary tool.

## 10. Common mistakes

- Confusing `pivot` with `pivot_table`.
- Forgetting to specify the aggregation function.
- Filling missing combinations with zero without checking their meaning.
- Interpreting raw counts when group sizes differ substantially.
- Forgetting that a pivot table can produce hierarchical indexes or columns.

## 11. Practice

1. Create a sales pivot table by city and product.
2. Change sum to mean.
3. Add grand totals.
4. Create a crosstab of department and pass/fail.
5. Normalize the crosstab by row and explain the result.

**Checkpoint:** Use pivot tables to summarize numeric values and crosstab to count category combinations.
