# Pandas Missing Data --- Complete Notes

## 1. What is Missing Data?

Missing data means a value is not available in a DataFrame.

In Pandas, missing numerical values are commonly represented by:

``` python
np.nan
```

Example:

``` python
import numpy as np
import pandas as pd

data = {
    'A': [1, 2, np.nan, 4, 5],
    'B': [1, 2, 3, 4, 5],
    'C': [1, 2, 3, np.nan, np.nan],
    'D': [1, np.nan, np.nan, np.nan, 5]
}

df = pd.DataFrame(data)
```

------------------------------------------------------------------------

# 2. Finding Missing Data

## `df.isna()`

Checks every cell and returns:

-   `True` → value is missing
-   `False` → value is present

``` python
df.isna()
```

### Memory trick

> `isna()` = "Is this value NA?"

------------------------------------------------------------------------

## `df.isna().sum()`

Counts missing values in every column.

``` python
df.isna().sum()
```

Example:

``` text
A    1
B    0
C    2
D    3
```

This is one of the most useful commands when inspecting a dataset.

### Meaning

> "How many missing values are there in each column?"

------------------------------------------------------------------------

## `df.isna().any()`

Checks whether each column contains at least one missing value.

``` python
df.isna().any()
```

Example:

``` text
A     True
B    False
C     True
D     True
```

### Meaning

> "Does this column contain any missing value?"

------------------------------------------------------------------------

# 3. Useful Missing-Data Pattern

When loading a new dataset, a useful first check is:

``` python
df.isna().sum()
```

Then investigate columns with many missing values.

A good general workflow is:

``` text
Find missing values
        ↓
Count missing values
        ↓
Understand why they are missing
        ↓
Decide whether to remove or fill them
```

------------------------------------------------------------------------

# 4. Removing Missing Data

## `df.dropna()`

Removes rows containing missing values.

``` python
df.dropna()
```

By default:

``` text
axis = 0
```

so rows are removed.

### Example

If:

``` text
A   B   C
1   2   3
4   NaN 6
7   8   9
```

then:

``` python
df.dropna()
```

gives:

``` text
A   B   C
1   2   3
7   8   9
```

### Memory trick

> `dropna()` = Drop rows with missing values.

------------------------------------------------------------------------

# 5. `dropna(thresh=...)`

`thresh` specifies the minimum number of **non-missing values**
required.

``` python
df.dropna(thresh=3)
```

means:

> Keep only rows having at least 3 non-missing values.

Example:

``` text
Row 0 → 4 valid values → KEEP
Row 1 → 3 valid values → KEEP
Row 2 → 2 valid values → REMOVE
```

### Important

``` python
df.dropna(thresh=1)
```

means every row with at least one valid value is kept.

### Memory trick

> `thresh = minimum number of valid values`

------------------------------------------------------------------------

# 6. Removing Columns Instead of Rows

You can specify:

``` python
df.dropna(axis=1)
```

This removes columns containing missing values.

Remember:

``` text
axis=0 → rows
axis=1 → columns
```

------------------------------------------------------------------------

# 7. Filling Missing Data

Instead of deleting rows, we can replace missing values.

## `fillna(0)`

``` python
df.fillna(0)
```

Every missing value becomes `0`.

Example:

``` text
NaN → 0
```

### Important

Do not blindly replace every missing value with zero.

For example:

``` text
Age = NaN
```

Changing it to:

``` text
Age = 0
```

may be meaningless.

The replacement should make sense for the data.

------------------------------------------------------------------------

# 8. Filling Different Columns with Different Values

Use a dictionary:

``` python
values = {
    'A': 0,
    'B': 100,
    'C': 300,
    'D': 400
}

df.fillna(value=values)
```

Meaning:

``` text
A missing → 0
B missing → 100
C missing → 300
D missing → 400
```

This is called column-specific filling.

------------------------------------------------------------------------

# 9. Filling With the Mean

A common technique for numerical data is replacing missing values with
the column mean.

``` python
df.fillna(df.mean())
```

First:

``` python
df.mean()
```

calculates the mean of each numerical column.

Example:

``` text
A → 3
B → 3
C → 2
D → 3
```

Then missing values are replaced using the corresponding column's mean.

For example:

``` text
A = [1, 2, NaN, 4, 5]

mean = (1 + 2 + 4 + 5) / 4
     = 3
```

So:

``` text
NaN → 3
```

------------------------------------------------------------------------

# 10. Mean vs Median vs Mode

Mean is not always the best choice.

### Mean

``` python
df['Age'].fillna(df['Age'].mean())
```

Useful when the numerical data is reasonably balanced and does not have
strong outliers.

### Median

``` python
df['Age'].fillna(df['Age'].median())
```

Often useful when data contains outliers or is strongly skewed.

### Mode

``` python
df['City'].fillna(df['City'].mode()[0])
```

Often useful for categorical data.

### Quick memory

``` text
Numerical → Mean / Median
Categorical → Mode
```

The correct choice depends on the dataset.

------------------------------------------------------------------------

# 11. Checking Missing Values After Filling

You can verify the result:

``` python
df.isna().sum()
```

If everything was handled:

``` text
A    0
B    0
C    0
D    0
```

------------------------------------------------------------------------

# 12. Original DataFrame Is Usually Not Changed

For example:

``` python
df.fillna(0)
```

returns a modified result but normally does not permanently replace
`df`.

To save the result:

``` python
df = df.fillna(0)
```

Similarly:

``` python
df = df.dropna()
```

is a simple way to store the cleaned DataFrame.

------------------------------------------------------------------------

# 13. `inplace=True`

Some Pandas operations support:

``` python
df.dropna(inplace=True)
```

or:

``` python
df.fillna(0, inplace=True)
```

This modifies the existing DataFrame.

For learning and readable code, assigning the result is often clearer:

``` python
df = df.fillna(0)
```

------------------------------------------------------------------------

# 14. Complete Quick Reference

  -----------------------------------------------------------------------
  Code                                Meaning
  ----------------------------------- -----------------------------------
  `df.isna()`                         Find missing cells

  `df.isna().sum()`                   Count missing values per column

  `df.isna().any()`                   Check whether missing values exist

  `df.dropna()`                       Remove rows containing missing
                                      values

  `df.dropna(axis=1)`                 Remove columns containing missing
                                      values

  `df.dropna(thresh=3)`               Keep rows with at least 3
                                      non-missing values

  `df.fillna(0)`                      Fill missing values with 0

  `df.fillna(value=dict)`             Fill columns with specified values

  `df.fillna(df.mean())`              Fill numerical missing values with
                                      column means

  `df['A'].median()`                  Calculate median

  `df['A'].mode()`                    Calculate mode
  -----------------------------------------------------------------------

------------------------------------------------------------------------

# 15. Most Important Memory Trick

``` text
isna()
  ↓
Find missing

isna().sum()
  ↓
Count missing

dropna()
  ↓
Remove missing

fillna()
  ↓
Fill missing
```

And:

``` text
axis=0 → rows
axis=1 → columns

thresh → minimum valid values
```

------------------------------------------------------------------------

# 16. Practice Checklist

1.  Find all missing cells.
2.  Count missing values in every column.
3.  Check whether each column has missing data.
4.  Remove rows containing missing values.
5.  Remove columns containing missing values.
6.  Keep rows with at least 3 valid values.
7.  Fill missing values with 0.
8.  Fill different columns with different values.
9.  Fill numerical columns using mean.
10. Decide when median or mode would be more appropriate.
