# Pandas GroupBy, Pivot Tables and Crosstabs — Complete Notes

> Beginner-friendly class notes with explanations, worked examples, memory tricks, common mistakes, and a revision table.

## Contents
1. What problem do these tools solve?
2. Sample dataset
3. `groupby()`
4. Aggregation functions
5. Grouping by multiple columns
6. Pivot tables
7. Crosstabs
8. How to choose the right tool
9. Common mistakes and shortcuts
10. Practice questions and answers
11. Final summary table

---

## 1. What problem do these tools solve?

Imagine a shop records every sale. You have many rows, but you want answers such as:

- How much money did each product category earn?
- How much did each store earn for each category?
- How many students selected Python or Java?
- How can categories and stores be compared in a compact table?

Pandas provides three related tools:

| Tool | Main idea | Think of it as |
|---|---|---|
| `groupby()` | Split rows into groups, then calculate a result | Group and calculate |
| `pivot_table()` | Summarise values into a row-and-column table | Rearrange a summary |
| `crosstab()` | Count combinations of categories by default | Count combinations |

## 2. Create the example DataFrame

```python
import pandas as pd

df = pd.DataFrame({
    "Category": ["Food", "Clothes", "Food", "Clothes", "Food", "Clothes"],
    "Store":    ["S1",   "S1",      "S2",   "S2",      "S1",   "S2"],
    "Sales":    [100,    200,       300,    400,       150,    250]
})

print(df)
```

| Index | Category | Store | Sales |
|---:|---|---|---:|
| 0 | Food | S1 | 100 |
| 1 | Clothes | S1 | 200 |
| 2 | Food | S2 | 300 |
| 3 | Clothes | S2 | 400 |
| 4 | Food | S1 | 150 |
| 5 | Clothes | S2 | 250 |

Read each row as one sale. For example, row 0 means the Food category earned 100 at store S1.

## 3. `groupby()` — group rows before calculating

### 3.1 Basic syntax

```python
df.groupby("column_to_group_by")["column_to_calculate"].sum()
```

A useful mental model is:

1. **Split** the rows by the chosen group column.
2. **Apply** a calculation to each group.
3. **Combine** the results into a summary.

### 3.2 Example: total sales for each category

```python
df.groupby("Category")["Sales"].sum()
```

Output:

```text
Category
Clothes    850
Food       550
Name: Sales, dtype: int64
```

Why?

- Food: 100 + 300 + 150 = **550**
- Clothes: 200 + 400 + 250 = **850**

Pandas collects the Food rows together, adds their Sales, then does the same for Clothes.

### 3.3 Understand each part

For `df.groupby("Category")["Sales"].sum()`:

| Part | Meaning |
|---|---|
| `df` | The original DataFrame |
| `.groupby("Category")` | Create groups based on Category |
| `["Sales"]` | Choose the numeric column to calculate |
| `.sum()` | Add Sales values in each group |

### 3.4 Aggregation functions

```python
df.groupby("Category")["Sales"].sum()     # Total sales
df.groupby("Category")["Sales"].mean()    # Average sale
df.groupby("Category")["Sales"].median()   # Middle sale
df.groupby("Category")["Sales"].min()      # Smallest sale
df.groupby("Category")["Sales"].max()      # Largest sale
df.groupby("Category")["Sales"].count()    # Non-missing sales count
df.groupby("Category")["Sales"].std()      # Sample standard deviation
```

**Important:** `count()` counts non-missing values in the selected column. To count rows in each group even if that column has missing values, consider `size()`.

```python
df.groupby("Category").size()  # Number of rows in each category
```

### 3.5 Multiple aggregations with `agg()`

Use `agg()` when you want several statistics in one result.

```python
df.groupby("Category")["Sales"].agg(
    ["sum", "mean", "min", "max", "count"]
)
```

You get total, average, minimum, maximum and count for each category in a single summary.

You can also aggregate different columns using a dictionary:

```python
df.groupby("Category").agg({
    "Sales": ["sum", "mean"],
    "Store": "count"
})
```

This calculates more than one type of summary from selected columns. Note that `Store.count` counts non-missing Store values, not unique stores. To count unique stores, use `nunique()`.

```python
df.groupby("Category")["Store"].nunique()
```

### 3.6 Group by two or more columns

Question: How much did each **category at each store** earn?

```python
df.groupby(["Category", "Store"])["Sales"].sum()
```

Output:

| Category | Store | Sales |
|---|---|---:|
| Clothes | S1 | 200 |
| Clothes | S2 | 650 |
| Food | S1 | 250 |
| Food | S2 | 300 |

Explanation:

- Clothes at S1: 200
- Clothes at S2: 400 + 250 = 650
- Food at S1: 100 + 150 = 250
- Food at S2: 300

The result typically uses a **MultiIndex**: the summary is indexed by both Category and Store.

**Memory trick:** One column in `groupby()` means group by one characteristic. A list such as `["Category", "Store"]` means group by the combination of two characteristics.

### 3.7 Keep group columns as regular columns

If you prefer a regular DataFrame instead of grouped index levels:

```python
df.groupby(["Category", "Store"], as_index=False)["Sales"].sum()
```

Or:

```python
df.groupby(["Category", "Store"])["Sales"].sum().reset_index()
```

Both are common ways to convert index levels back into columns.

---

## 4. Pivot tables — compare groups in a grid

### 4.1 Why use a pivot table?

The GroupBy result is correct, but sometimes it is easier to compare stores side by side. A pivot table turns categories into row and column labels.

### 4.2 Basic syntax

```python
pd.pivot_table(
    df,
    index="row_category",
    columns="column_category",
    values="numeric_column",
    aggfunc="sum"
)
```

Example:

```python
pd.pivot_table(
    df,
    index="Category",
    columns="Store",
    values="Sales",
    aggfunc="sum"
)
```

Output:

| Category | S1 | S2 |
|---|---:|---:|
| Clothes | 200 | 650 |
| Food | 250 | 300 |

### 4.3 Understand the arguments

| Argument | Easy meaning | This example |
|---|---|---|
| `data` | Source table | `df` |
| `index` | Category displayed as rows | `"Category"` |
| `columns` | Category used as column headings | `"Store"` |
| `values` | Numbers to summarise | `"Sales"` |
| `aggfunc` | How duplicates are combined | `"sum"` |

**Shortcut to remember:** **I-C-V-A** = **Index, Columns, Values, Aggregation**.

Ask four questions:
1. What should the rows be?
2. What should the column headings be?
3. What numbers do I need?
4. How should the numbers be combined?

### 4.4 Why do we need `aggfunc`?

There are multiple Food sales at S1: 100 and 150. The pivot table combines them into one cell.

- `aggfunc="sum"`: 100 + 150 = 250
- `aggfunc="mean"`: (100 + 150) / 2 = 125
- `aggfunc="count"`: 2 sales
- `aggfunc="max"`: 150
- `aggfunc="min"`: 100

```python
pd.pivot_table(df, index="Category", columns="Store",
               values="Sales", aggfunc="mean")

pd.pivot_table(df, index="Category", columns="Store",
               values="Sales", aggfunc="count")

pd.pivot_table(df, index="Category", columns="Store",
               values="Sales", aggfunc="max")
```

For numeric values, the default `aggfunc` of `pivot_table()` is `"mean"`. For clarity, explicitly specify the aggregation you intend to use.

### 4.5 Missing combinations and `fill_value`

If a category-store pair does not appear in the original data, the result may contain `NaN`.

```python
pd.pivot_table(
    df,
    index="Category",
    columns="Store",
    values="Sales",
    aggfunc="sum",
    fill_value=0
)
```

`fill_value=0` displays 0 for missing result cells. Be careful: a missing combination is not always the same as a true measured zero.

---

## 5. Crosstabs — count combinations of categories

### 5.1 The easiest way to understand it

Imagine asking students which programming language they prefer. You want to count how many First Year and Second Year students selected each language.

```python
survey = pd.DataFrame({
    "Year": ["First", "First", "First", "Second", "Second", "Second"],
    "Language": ["Python", "Java", "Python", "Java", "Python", "Java"]
})
```

Count combinations:

```python
pd.crosstab(survey["Year"], survey["Language"])
```

Output:

| Year | Java | Python |
|---|---:|---:|
| First | 1 | 2 |
| Second | 2 | 1 |

Interpretation:
- First Year: 1 student selected Java, 2 selected Python.
- Second Year: 2 students selected Java, 1 selected Python.

By default, `crosstab()` counts how often each combination appears.

### 5.2 Syntax

```python
pd.crosstab(
    index=survey["Year"],
    columns=survey["Language"]
)
```

| Argument | Meaning |
|---|---|
| `index` | Categories displayed as rows |
| `columns` | Categories displayed as column headings |

Unlike a typical pivot-table exercise, a crosstab does not need a separate numeric values column to count records.

### 5.3 Add totals

```python
pd.crosstab(
    survey["Year"],
    survey["Language"],
    margins=True
)
```

`margins=True` adds row and column totals, often labelled `All`.

### 5.4 Crosstab can also aggregate numeric values

```python
pd.crosstab(
    index=df["Category"],
    columns=df["Store"],
    values=df["Sales"],
    aggfunc="sum",
    margins=True
)
```

For numeric aggregation, provide `values` and `aggfunc` together.

---

## 6. GroupBy vs Pivot Table vs Crosstab

| Question | Best starting point |
|---|---|
| Total Sales for each Category? | `groupby()` |
| Total for each Category and Store? | `groupby()` |
| Compare stores side by side for each Category? | `pivot_table()` |
| Count students by Year and preferred Language? | `crosstab()` |
| Count records for every Category-Store combination? | `groupby().size()` or `crosstab()` |
| Need different statistics in a row-and-column grid? | `pivot_table()` |

### Remember it like this

- **GroupBy:** grouping and calculation.
- **Pivot table:** numeric summary in a grid.
- **Crosstab:** count category combinations by default.

These are guidelines, not strict limits. There is overlap: the three tools can sometimes produce similar summaries.

---

## 7. Common mistakes

### Mistake 1: Forgetting the column selected for calculation

```python
df.groupby("Category")["Sales"].sum()
```

The group column decides the groups. The Sales column provides the numbers to add.

### Mistake 2: Expecting `groupby()` alone to calculate a total

```python
df.groupby("Category")
```

This creates a GroupBy object; append a calculation such as `.sum()`, `.mean()`, or `.agg(...)` to obtain a summary.

### Mistake 3: Using the wrong pivot orientation

```python
pd.pivot_table(df, index="Category", columns="Store",
               values="Sales", aggfunc="sum")
```

Category is the row label; Store is the column heading. Swap `index` and `columns` to rotate the layout.

### Mistake 4: Assuming crosstab sums values by default

```python
pd.crosstab(df["Category"], df["Store"])
```

This counts combinations; it does not sum Sales. To sum sales, supply `values=df["Sales"]` and `aggfunc="sum"`.

### Mistake 5: Confusing count and unique count

```python
df.groupby("Category")["Store"].count()    # Non-missing Store entries
df.groupby("Category")["Store"].nunique()  # Distinct Store labels
```

### Mistake 6: Treating missing values as zero automatically

A missing cell may mean there are no records for that combination or that data is unavailable. Only fill it with 0 when that interpretation makes sense.

---

## 8. Quick shortcuts

```python
# Total sales per category
df.groupby("Category")["Sales"].sum()

# Multiple statistics per category
df.groupby("Category")["Sales"].agg(["sum", "mean", "min", "max"])

# Total sales per category and store
df.groupby(["Category", "Store"], as_index=False)["Sales"].sum()

# Summary grid
pd.pivot_table(df, index="Category", columns="Store",
               values="Sales", aggfunc="sum", fill_value=0)

# Count category-store combinations
pd.crosstab(df["Category"], df["Store"], margins=True)
```

---

## 9. Practice questions

Use the example `df` from the beginning.

1. Find total sales for each Store.
2. Find average Sales for each Category.
3. Find the maximum sale for each Category.
4. Summarise total Sales by Category and Store using GroupBy.
5. Create a pivot table with Category as rows, Store as columns, and sum of Sales as values.
6. Change the pivot table aggregation from `sum` to `mean`.
7. Count rows for each Category and Store combination using `crosstab()`.
8. Add totals to a crosstab using `margins=True`.

### Answer key

Try to solve them before reading the code.

```python
# 1
df.groupby("Store")["Sales"].sum()

# 2
df.groupby("Category")["Sales"].mean()

# 3
df.groupby("Category")["Sales"].max()

# 4
df.groupby(["Category", "Store"], as_index=False)["Sales"].sum()

# 5
pd.pivot_table(df, index="Category", columns="Store",
               values="Sales", aggfunc="sum")

# 6
pd.pivot_table(df, index="Category", columns="Store",
               values="Sales", aggfunc="mean")

# 7
pd.crosstab(df["Category"], df["Store"])

# 8
pd.crosstab(df["Category"], df["Store"], margins=True)
```

---

## 10. Final revision summary table

| Function / argument | Purpose | Memory trick |
|---|---|---|
| `groupby()` | Split rows into groups | Group |
| `sum()` | Add values | Total |
| `mean()` | Calculate average | Average |
| `median()` | Middle value | Middle |
| `min()` / `max()` | Smallest / largest value | Ends |
| `count()` | Count non-missing values | Filled values |
| `size()` | Count rows in each group | Row count |
| `std()` | Measure spread around the mean | Spread |
| `agg()` | Calculate several summaries | Many calculations |
| `nunique()` | Count distinct values | Unique |
| `as_index=False` | Keep group labels as ordinary columns | Flat table |
| `reset_index()` | Move index levels into columns | Reset layout |
| `pivot_table()` | Summarise values in a grid | Compare |
| `index` | Row categories in a pivot table | Rows |
| `columns` | Column headings in a pivot table | Headings |
| `values` | Values to summarise | Numbers |
| `aggfunc` | Aggregation used by a pivot table or crosstab | How to combine |
| `fill_value=0` | Replace missing result cells with 0 | Fill gaps |
| `crosstab()` | Count category combinations by default | Count |
| `margins=True` | Include row and column totals | Totals |

## One-minute recap

1. **GroupBy:** group similar rows and calculate a summary.
2. **Pivot table:** put a summary into a grid with row and column categories.
3. **Crosstab:** count combinations of categories by default.
4. Use `agg()` when you need several statistics.
5. Specify `aggfunc` intentionally; do not assume pivot tables always sum.
6. Choose the tool based on the question you need to answer.
