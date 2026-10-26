# Pandas DataFrame Basic Operations and Applying Functions — Complete Notes

> Beginner-friendly notes for understanding DataFrame structure, basic inspection, statistics, Series operations, `apply()`, and `lambda`, with worked examples, tricks, common mistakes, practice, and summary tables.

## Contents

1. What is a DataFrame?
2. Create the example DataFrame
3. `.shape`
4. `.columns`
5. `.info()`
6. `.describe()`
7. Selecting a column
8. Vectorized operations
9. Creating and updating columns
10. Functions, `apply()`, and `lambda`
11. Common mistakes
12. Practice exercises
13. Final summary table

---

## 1. What is a DataFrame?

A **DataFrame** is a two-dimensional labelled table in Pandas. It looks similar to a spreadsheet.

- **Rows** run horizontally and usually represent records.
- **Columns** run vertically and represent fields.
- **Index** labels rows.
- **Values** are the data stored in the table.

For example, a student DataFrame may have columns like Name, Java, Python, and Maths.

## 2. Import Pandas and create a DataFrame

```python
import numpy as np
import pandas as pd

df1 = pd.DataFrame({
    "A": [1, 2, 3, 4, 5],
    "B": [10, 20, 30, 40, 50],
    "C": [100, 200, 300, 400, 500]
})

print(df1)
```

Output:

| Index | A | B | C |
|---:|---:|---:|---:|
| 0 | 1 | 10 | 100 |
| 1 | 2 | 20 | 200 |
| 2 | 3 | 30 | 300 |
| 3 | 4 | 40 | 400 |
| 4 | 5 | 50 | 500 |

**Import trick:** `pd` is the conventional alias for Pandas; `np` is the conventional alias for NumPy. The shown examples use Pandas. NumPy is imported here but is not needed for every operation in these notes.

---

## 3. `df1.shape` — find the table dimensions

### What does it do?

`shape` tells you the number of rows and columns. Its output is a tuple of the form:

`(number_of_rows, number_of_columns)`

```python
df1.shape
```

Output:

```text
(5, 3)
```

This means the table contains 5 rows and 3 columns.

### Get each dimension separately

```python
df1.shape[0]  # 5 rows
df1.shape[1]  # 3 columns
```

### Memory trick

**Shape = Rows first, Columns second (R-C).**

### Important detail

`shape` is an **attribute**, not a method. Do not add parentheses.

```python
df1.shape     # Correct
# df1.shape() # Incorrect: shape is not callable
```

**When to use it:** Check the size of a dataset after loading data or after filtering rows and columns.

---

## 4. `df1.columns` — inspect column names

### What does it do?

Returns the labels of all columns.

```python
df1.columns
```

Output:

```text
Index(['A', 'B', 'C'], dtype='object')
```

### Rename columns

```python
df1.columns = ["X", "Y", "Z"]
```

This replaces the current column labels. The number of new labels must match the number of columns. If you rename columns this way, later examples that use A, B, and C will need to be adjusted or the original DataFrame recreated.

Another way to rename selected columns is:

```python
df1 = df1.rename(columns={"A": "Marks", "B": "Attendance"})
```

### Memory trick

**Columns tells you what fields the table has.**

**When to use it:** Discover field names before selecting a column or writing a calculation.

---

## 5. `df1.info()` — inspect the DataFrame structure

### What does it do?

```python
df1.info()
```

It prints a compact report including:

- The index range and row count.
- The number of columns.
- Each column name.
- How many values in each column are non-missing.
- The data type of each column.
- Approximate memory usage.

Example of key output:

```text
RangeIndex: 5 entries, 0 to 4
Data columns (total 3 columns):
 #   Column  Non-Null Count  Dtype
 0   A       5 non-null      int64
 1   B       5 non-null      int64
 2   C       5 non-null      int64
dtypes: int64(3)
```

### Understand the terms

| Term | Meaning |
|---|---|
| `5 entries` | There are 5 rows. |
| `5 non-null` | Five values are present in that column; none are missing in this example. |
| `int64` | Integer data type. |
| `float64` | Floating-point / decimal-number data type. |
| `object` | Often text or mixed Python objects in a column. |
| `memory usage` | Approximate memory occupied by the DataFrame. |

### Does `info()` return a DataFrame?

No. It prints information directly and normally returns `None`.

```python
df1.info()
```

Don't write `result = df1.info()` expecting `result` to contain the report as a DataFrame.

### Memory trick

**Info = Identity and internals:** rows, columns, types, missing-value counts, and memory details.

**When to use it:** Immediately after loading a dataset, especially a CSV file, to check for unexpected data types or missing values.

---

## 6. `df1.describe()` — statistical summary

### What does it do?

```python
df1.describe()
```

By default, `describe()` summarises numeric columns with common descriptive statistics.

| Statistic | A | B | C |
|---|---:|---:|---:|
| `count` | 5 | 5 | 5 |
| `mean` | 3 | 30 | 300 |
| `std` | 1.581139 | 15.811388 | 158.113883 |
| `min` | 1 | 10 | 100 |
| `25%` | 2 | 20 | 200 |
| `50%` | 3 | 30 | 300 |
| `75%` | 4 | 40 | 400 |
| `max` | 5 | 50 | 500 |

### Understand every statistic

#### `count` — number of non-missing values

Column A has 5 values, so its count is 5.

#### `mean` — average

Formula:

`Mean = Sum of values / Number of values`

For A:

`(1 + 2 + 3 + 4 + 5) / 5 = 3`

#### `std` — standard deviation

Standard deviation describes how spread out numeric values are around their mean. A smaller standard deviation usually means values are closer to the mean; a larger one means more spread.

Pandas `describe()` reports the **sample** standard deviation for numeric columns by default (equivalent to `Series.std(ddof=1)`). This is why column A's displayed value is about 1.581 rather than the population standard deviation.

#### `min` and `max`

- `min`: the smallest value.
- `max`: the largest value.

For A, minimum is 1 and maximum is 5.

#### `25%`, `50%`, and `75%` — quartiles

- `25%`: first quartile; 25% of observations are at or below this point.
- `50%`: median, or middle point.
- `75%`: third quartile; 75% of observations are at or below this point.

For [1, 2, 3, 4, 5], the median is 3. Pandas calculates the quartiles using its quantile method, so for other datasets the answers can sometimes fall between observed values.

### Useful variants

```python
df1["A"].describe()            # Statistics for one Series
df1.describe(include="all")    # Include more column types where supported
df1.describe().round(2)        # Round displayed statistics to 2 decimals
```

### Difference between `info()` and `describe()`

- `info()` explains the table structure and data types.
- `describe()` summarises the data statistically.

**Memory trick:** Info tells you what the data looks like; describe tells you what the numeric data looks like statistically.

---

## 7. Select a column: `df1["A"]`

```python
df1["A"]
```

This returns a Pandas **Series** containing column A:

```text
0    1
1    2
2    3
3    4
4    5
Name: A, dtype: int64
```

A Series is similar to one labelled column of a table.

Useful selections:

```python
df1["A"]             # One column: Series
df1[["A", "C"]]      # Multiple columns: DataFrame
```

Notice the double brackets in `df1[["A", "C"]]`: the inner list contains the names of multiple columns.

---

## 8. Vectorized operations — operate on an entire column

### Example: add 10

```python
df1["A"] + 10
```

Output values:

```text
0    11
1    12
2    13
3    14
4    15
```

Pandas adds 10 to every element in column A.

| Original A | A + 10 |
|---:|---:|
| 1 | 11 |
| 2 | 12 |
| 3 | 13 |
| 4 | 14 |
| 5 | 15 |

This is called a **vectorized operation**. It performs an operation on a whole Series without requiring you to write a Python loop.

### More examples

```python
df1["A"] + 10   # Add 10
df1["A"] - 1    # Subtract 1
df1["A"] * 2    # Multiply by 2
df1["A"] / 2    # Divide by 2
df1["A"] ** 2   # Square each value
```

### Does this change the original DataFrame?

No. `df1["A"] + 10` creates a result but does not save it back into `df1`.

To update column A:

```python
df1["A"] = df1["A"] + 10
```

To create a new column instead:

```python
df1["A_plus_10"] = df1["A"] + 10
```

**Memory trick:** A calculation by itself shows a result. Assignment using `=` stores the result in a variable or column.

---

## 9. Creating a new column with a calculated result

Your class example:

```python
df1["D"] = df1["B"].apply(lambda x: x**2)
```

Before running this, the original DataFrame has columns A, B, and C. The statement creates column D from the square of each value in B.

### Step-by-step

1. `df1["B"]` selects B: `10, 20, 30, 40, 50`.
2. `.apply(...)` applies the supplied function to the selected Series values.
3. `lambda x: x**2` squares each input value `x`.
4. `df1["D"] = ...` saves the results in a new column D.

| B | Calculation | D |
|---:|---|---:|
| 10 | `10 ** 2` | 100 |
| 20 | `20 ** 2` | 400 |
| 30 | `30 ** 2` | 900 |
| 40 | `40 ** 2` | 1600 |
| 50 | `50 ** 2` | 2500 |

Resulting DataFrame:

| Index | A | B | C | D |
|---:|---:|---:|---:|---:|
| 0 | 1 | 10 | 100 | 100 |
| 1 | 2 | 20 | 200 | 400 |
| 2 | 3 | 30 | 300 | 900 |
| 3 | 4 | 40 | 400 | 1600 |
| 4 | 5 | 50 | 500 | 2500 |

---

## 10. Functions, `apply()`, and `lambda`

### 10.1 What is a function?

A function is reusable code that performs a task. Python has built-in functions such as `len()`, and you can create your own with `def`.

```python
def square(x):
    return x ** 2

square(5)  # 25
```

The function receives 5 as `x`, calculates `5 ** 2`, and returns 25.

### 10.2 What is a lambda function?

A `lambda` creates a small anonymous function, often for a simple one-line calculation.

```python
lambda x: x ** 2
```

Read it as: "take input x and return x squared."

| Part | Meaning |
|---|---|
| `lambda` | Begin a small anonymous function |
| `x` | The input parameter |
| `:` | Separates the input from the expression |
| `x ** 2` | The result expression |

For example:

```python
square = lambda x: x ** 2
square(5)  # 25
```

A `lambda` expression returns the value of its expression automatically. It doesn't use a `return` statement.

### 10.3 What is `.apply()`?

For a Series, `.apply(function)` applies the supplied function to its values and returns the results.

```python
marks = pd.Series([35, 65, 90, 45])

marks.apply(lambda x: x + 5)
```

Output values: `40, 70, 95, 50`.

The `x` changes for each call to the function:

- First call: x = 35 → 35 + 5 = 40
- Second call: x = 65 → 65 + 5 = 70
- Third call: x = 90 → 90 + 5 = 95
- Fourth call: x = 45 → 45 + 5 = 50

### 10.4 Example: square each number

```python
numbers = pd.Series([2, 3, 4])

numbers.apply(lambda x: x ** 2)
```

Output values: `4, 9, 16`.

### 10.5 Example: pass/fail classification

```python
marks = pd.Series([35, 65, 90, 45])

marks.apply(lambda x: "Pass" if x >= 40 else "Fail")
```

Output values: `Fail, Pass, Pass, Pass`.

Read the conditional expression as: if `x >= 40` is true, return `"Pass"`; otherwise return `"Fail"`.

### 10.6 Normal function vs lambda

Normal function:

```python
def add_five(x):
    return x + 5

marks.apply(add_five)
```

Equivalent lambda:

```python
marks.apply(lambda x: x + 5)
```

Both can perform the same calculation. A named function may be easier to read when the logic has a meaningful name or multiple steps.

### 10.7 Prefer vectorized expressions for simple numeric operations

For straightforward numeric calculations, you usually do not need `.apply()`.

Instead of:

```python
df1["B"].apply(lambda x: x ** 2)
```

write:

```python
df1["B"] ** 2
```

Both produce the squares. Vectorized Pandas/NumPy operations are often clearer and faster for standard numeric calculations. Use `.apply()` when a custom function or conditional logic makes the code easier to express.

### Memory trick

- **apply** = apply a function to each value (for a Series).
- **lambda x** = the value currently being passed in.
- **`**`** = power.
- **`=`** = save the result.

---

## 11. Common mistakes and how to avoid them

### Mistake 1: Adding parentheses to an attribute

```python
df1.shape    # Correct
df1.columns  # Correct
```

They are attributes, so do not call them like functions.

### Mistake 2: Expecting `info()` to return the report

```python
df1.info()
```

It prints the report. It does not return a DataFrame of the report.

### Mistake 3: Confusing `count` with total rows

`describe()`'s `count` and a Series `count()` count non-missing values. If a column contains missing values, the count can be lower than the number of rows. `shape[0]` counts rows in the DataFrame regardless of missing values.

### Mistake 4: Forgetting to save a calculation

```python
df1["A"] + 10  # Shows a result but does not update df1
df1["A"] = df1["A"] + 10  # Saves the updated values
```

### Mistake 5: Using `^` for powers

In Python, use `**` for exponentiation.

```python
5 ** 2  # 25
```

`^` is bitwise XOR, not exponentiation.

### Mistake 6: Giving a new column list with the wrong length

When using `df1.columns = [...]`, provide exactly as many new labels as there are columns.

### Mistake 7: Using `.apply()` for every simple calculation

For simple numeric operations, prefer vectorized syntax like `df1["B"] ** 2`. It is often simpler and faster.

---

## 12. Practice exercises

Use the original `df1` with columns A, B, and C. Run exercises in order and create a fresh copy if you have modified the columns.

1. Display the number of rows and columns.
2. Display only the number of rows.
3. Display all column names.
4. Show the DataFrame structure and data types.
5. Generate descriptive statistics for all numeric columns.
6. Select column B.
7. Add 5 to each value in column A without changing the original DataFrame.
8. Create a new column called `B_double` by doubling B.
9. Create a new column called `B_square` by squaring B.
10. Apply a lambda function to add 10 to each value in a Series.
11. Classify marks below 40 as Fail and marks 40 or above as Pass.
12. Write the square operation once with `def` and once with `lambda`.

### Answer key

```python
# 1
df1.shape

# 2
df1.shape[0]

# 3
df1.columns

# 4
df1.info()

# 5
df1.describe()

# 6
df1["B"]

# 7
df1["A"] + 5

# 8
df1["B_double"] = df1["B"] * 2

# 9
df1["B_square"] = df1["B"] ** 2

# 10
pd.Series([1, 2, 3]).apply(lambda x: x + 10)

# 11
pd.Series([35, 65, 90]).apply(
    lambda x: "Pass" if x >= 40 else "Fail"
)

# 12
def square(x):
    return x ** 2

square_lambda = lambda x: x ** 2
```

---

## 13. Final summary table

| Operation | Type | What it does | Example / shortcut |
|---|---|---|---|
| `pd.DataFrame()` | Constructor | Creates a table | `pd.DataFrame({"A": [1, 2]})` |
| `.shape` | Attribute | Returns (rows, columns) | `df1.shape` |
| `.shape[0]` | Tuple indexing | Gets row count | `df1.shape[0]` |
| `.shape[1]` | Tuple indexing | Gets column count | `df1.shape[1]` |
| `.columns` | Attribute | Lists column labels | `df1.columns` |
| `.info()` | Method | Prints structure, types, non-null counts, memory info | `df1.info()` |
| `.describe()` | Method | Produces a statistical summary of numeric columns by default | `df1.describe()` |
| `count` | Statistic | Counts non-missing values | `df1["A"].count()` |
| `mean` | Statistic | Calculates the average | `df1["A"].mean()` |
| `std` | Statistic | Measures spread using standard deviation | `df1["A"].std()` |
| `min` / `max` | Statistic | Finds smallest / largest value | `df1["A"].min()` |
| `df1["A"]` | Selection | Selects one column as a Series | `df1["A"]` |
| `+`, `-`, `*`, `/` | Operators | Arithmetic on Series values | `df1["A"] + 10` |
| `**` | Operator | Exponentiation / power | `df1["B"] ** 2` |
| `=` | Assignment | Saves a result | `df1["D"] = ...` |
| `.apply()` | Method | Applies a supplied function to Series values | `series.apply(func)` |
| `lambda` | Python expression | Defines a small anonymous function | `lambda x: x**2` |
| `def` | Python statement | Defines a named function | `def square(x): ...` |
| `np` | Alias | Conventional NumPy alias | `import numpy as np` |
| `pd` | Alias | Conventional Pandas alias | `import pandas as pd` |

## One-minute recap

- **shape:** how many rows and columns?
- **columns:** what are the column names?
- **info():** what are the structure and data types?
- **describe():** what do the numeric statistics tell me?
- **Vectorized operation:** perform a calculation on a whole Series.
- **apply():** apply a function to Series values.
- **lambda:** write a small function in one expression.
- **Assignment:** use `=` to save the result.
- For simple arithmetic, prefer expressions such as `df1["B"] ** 2` unless a custom function is genuinely useful.
