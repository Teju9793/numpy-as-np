# Pandas `merge()` + `concat()` + `join()` --- Complete Notes

## 1. The Big Picture

Pandas provides different ways to combine DataFrames.

The three important methods are:

``` text
merge()
concat()
join()
```

The easiest way to remember them:

``` text
MERGE  → Match using a common column/key
CONCAT → Put DataFrames together
JOIN   → Match mainly using the index
```

------------------------------------------------------------------------

# 2. `merge()`

## What is `merge()`?

`merge()` combines DataFrames using one or more common columns.

Think of it like a database JOIN.

Example:

``` python
employees = pd.DataFrame({
    'employee_id': [1, 2, 3, 4, 5],
    'name': ['John', 'Anna', 'Peter', 'Linda', 'Bob'],
    'department': ['HR', 'IT', 'Finance', 'IT', 'HR']
})

salaries = pd.DataFrame({
    'employee_id': [1, 2, 3, 6, 7],
    'salary': [60000, 80000, 65000, 70000, 90000],
    'bonus': [5000, 10000, 7000, 8000, 12000]
})
```

Both DataFrames contain:

``` text
employee_id
```

So we can merge using that column.

------------------------------------------------------------------------

# 3. Basic `merge()` Syntax

``` python
pd.merge(df1, df2, on='column_name', how='inner')
```

Example:

``` python
pd.merge(
    employees,
    salaries,
    on='employee_id',
    how='inner'
)
```

------------------------------------------------------------------------

# 4. `how='inner'`

Inner merge keeps only rows whose key exists in **both** DataFrames.

Employees:

``` text
1, 2, 3, 4, 5
```

Salaries:

``` text
1, 2, 3, 6, 7
```

Common IDs:

``` text
1, 2, 3
```

Therefore:

``` python
pd.merge(
    employees,
    salaries,
    on='employee_id',
    how='inner'
)
```

keeps:

``` text
1
2
3
```

### Memory trick

> INNER = Common / Matching records

------------------------------------------------------------------------

# 5. `how='left'`

``` python
pd.merge(
    employees,
    salaries,
    on='employee_id',
    how='left'
)
```

Keeps everything from the **left DataFrame**.

Here:

``` python
employees
```

is on the left.

Employee IDs:

``` text
1, 2, 3, 4, 5
```

IDs 4 and 5 have no salary record, so their salary and bonus become
`NaN`.

### Memory trick

> LEFT = Keep everything from the left DataFrame.

------------------------------------------------------------------------

# 6. `how='right'`

``` python
pd.merge(
    employees,
    salaries,
    on='employee_id',
    how='right'
)
```

Keeps everything from the **right DataFrame**.

Salary IDs:

``` text
1, 2, 3, 6, 7
```

IDs 6 and 7 don't have employee information, so employee columns become
`NaN`.

### Memory trick

> RIGHT = Keep everything from the right DataFrame.

------------------------------------------------------------------------

# 7. `how='outer'`

``` python
pd.merge(
    employees,
    salaries,
    on='employee_id',
    how='outer'
)
```

Keeps all unique keys from both DataFrames.

IDs:

``` text
1, 2, 3, 4, 5, 6, 7
```

Missing information becomes `NaN`.

### Memory trick

> OUTER = Everyone from both DataFrames.

------------------------------------------------------------------------

# 8. `merge()` Summary

  `how`     What is kept?
  --------- --------------------------------
  `inner`   Matching keys only
  `left`    All left keys + matching right
  `right`   All right keys + matching left
  `outer`   All keys from both

### Visual memory

``` text
LEFT       RIGHT

1          1
2          2
3          3
4          6
5          7

INNER → 1,2,3

LEFT  → 1,2,3,4,5

RIGHT → 1,2,3,6,7

OUTER → 1,2,3,4,5,6,7
```

------------------------------------------------------------------------

# 9. `on=`

`on` tells Pandas which common column should be used for matching.

``` python
pd.merge(df1, df2, on='employee_id')
```

Think:

> "Match rows using `employee_id`."

------------------------------------------------------------------------

# 10. Different Column Names

Sometimes the key columns have different names.

Example:

``` python
students = pd.DataFrame({
    'student_id': [1, 2, 3],
    'name': ['A', 'B', 'C']
})

marks = pd.DataFrame({
    'id': [1, 2, 3],
    'marks': [80, 90, 70]
})
```

Use:

``` python
pd.merge(
    students,
    marks,
    left_on='student_id',
    right_on='id'
)
```

### Remember

``` text
left_on  → key name in left DataFrame
right_on → key name in right DataFrame
```

------------------------------------------------------------------------

# 11. Multiple Columns in `merge()`

You can merge using multiple columns:

``` python
pd.merge(
    df1,
    df2,
    on=['student_id', 'semester']
)
```

Both columns must match.

------------------------------------------------------------------------

# 12. Handling Duplicate Column Names

Suppose both DataFrames contain:

``` text
name
```

Pandas may create suffixes such as:

``` text
name_x
name_y
```

You can control them:

``` python
pd.merge(
    df1,
    df2,
    on='id',
    suffixes=('_student', '_teacher')
)
```

Then you might get:

``` text
name_student
name_teacher
```

------------------------------------------------------------------------

# 13. `concat()`

`concat()` is mainly used to combine DataFrames by stacking them.

Basic syntax:

``` python
pd.concat([df1, df2])
```

------------------------------------------------------------------------

# 14. Vertical Concatenation

Example:

``` python
df1 = pd.DataFrame({
    'A': ['A0', 'A1', 'A2'],
    'B': ['B0', 'B1', 'B2']
})

df2 = pd.DataFrame({
    'A': ['A3', 'A4', 'A5'],
    'B': ['B3', 'B4', 'B5']
})
```

Use:

``` python
pd.concat([df1, df2])
```

Result:

``` text
A    B
A0   B0
A1   B1
A2   B2
A3   B3
A4   B4
A5   B5
```

### Memory trick

> CONCAT = Put one DataFrame after another.

------------------------------------------------------------------------

# 15. `axis=0`

By default:

``` python
pd.concat([df1, df2], axis=0)
```

means concatenate vertically.

``` text
df1
 ↓
df2
```

Remember:

``` text
axis=0 → rows
```

------------------------------------------------------------------------

# 16. `axis=1`

``` python
pd.concat([df1, df2], axis=1)
```

combines columns side by side.

``` text
df1 | df2
```

Remember:

``` text
axis=1 → columns
```

### Easy memory

``` text
axis=0 → ↓
axis=1 → →
```

------------------------------------------------------------------------

# 17. `ignore_index=True`

This is very important.

Suppose:

``` python
pd.concat([df1, df2])
```

produces:

``` text
0
1
2
0
1
2
```

because both original DataFrames had indexes starting from 0.

Use:

``` python
pd.concat(
    [df1, df2],
    ignore_index=True
)
```

Now the index becomes:

``` text
0
1
2
3
4
5
```

### Memory trick

> `ignore_index=True` = Forget old indexes and create a fresh index.

This is especially useful when stacking datasets such as:

``` text
January data
February data
March data
```

------------------------------------------------------------------------

# 18. `concat()` With Different Columns

Example:

``` python
df1 = pd.DataFrame({
    'Name': ['A', 'B'],
    'Age': [20, 21]
})

df2 = pd.DataFrame({
    'Name': ['C', 'D'],
    'Marks': [80, 90]
})
```

Now:

``` python
pd.concat([df1, df2], ignore_index=True)
```

will contain:

``` text
Name   Age   Marks
A      20    NaN
B      21    NaN
C      NaN   80
D      NaN   90
```

Pandas aligns columns by their names.

Missing columns become `NaN`.

------------------------------------------------------------------------

# 19. `join()`

`join()` combines DataFrames mainly using their indexes.

Example:

``` python
df1 = pd.DataFrame({
    'name': ['Alice', 'Bob', 'Charlie']
}, index=[1, 2, 3])

df2 = pd.DataFrame({
    'score': [85, 90, 75]
}, index=[2, 3, 4])
```

Here the indexes are:

``` text
df1 → 1, 2, 3
df2 → 2, 3, 4
```

------------------------------------------------------------------------

# 20. Basic `join()`

``` python
df1.join(df2)
```

By default, `join()` uses a left join.

So it keeps all indexes from `df1`:

``` text
1
2
3
```

Result:

``` text
   name     score
1  Alice    NaN
2  Bob      85
3  Charlie  90
```

------------------------------------------------------------------------

# 21. `join(how='outer')`

``` python
df1.join(df2, how='outer')
```

Keeps all indexes:

``` text
1, 2, 3, 4
```

Result:

``` text
       name  score
1      Alice  NaN
2      Bob    85
3      Charlie 90
4      NaN    75
```

------------------------------------------------------------------------

# 22. `join(how='inner')`

``` python
df1.join(df2, how='inner')
```

Keeps only common indexes:

``` text
2, 3
```

------------------------------------------------------------------------

# 23. `join()` From the Other Side

These are different:

``` python
df1.join(df2)
```

and:

``` python
df2.join(df1)
```

The DataFrame before `.join()` is the left DataFrame.

So:

``` python
df1.join(df2)
```

means:

``` text
df1 = left
df2 = right
```

while:

``` python
df2.join(df1)
```

means:

``` text
df2 = left
df1 = right
```

------------------------------------------------------------------------

# 24. `join()` With a Different Index

If you want to join using a column instead of the default index, you can
use:

``` python
df1.join(
    df2.set_index('student_id'),
    on='student_id'
)
```

For simple cases, however, remember:

> `join()` is mainly index-based.

------------------------------------------------------------------------

# 25. `merge()` vs `concat()` vs `join()`

  Method       Main purpose                 Matching
  ------------ ---------------------------- -------------------
  `merge()`    Match related records        Common column/key
  `concat()`   Stack/append DataFrames      Rows or columns
  `join()`     Combine related DataFrames   Mainly index

### The easiest memory trick

``` text
MERGE  → KEY
CONCAT → STACK
JOIN   → INDEX
```

------------------------------------------------------------------------

# 26. Important Options to Remember

## `merge()`

``` python
pd.merge(
    df1,
    df2,
    on='id',
    how='inner'
)
```

Important options:

``` text
on
how
left_on
right_on
suffixes
```

------------------------------------------------------------------------

## `concat()`

``` python
pd.concat(
    [df1, df2],
    axis=0,
    ignore_index=True
)
```

Important options:

``` text
axis
ignore_index
```

------------------------------------------------------------------------

## `join()`

``` python
df1.join(
    df2,
    how='outer'
)
```

Important option:

``` text
how
```

------------------------------------------------------------------------

# 27. Real-Life Examples

## Example 1 --- Merge

You have:

``` text
Student information
Student marks
```

Both contain:

``` text
student_id
```

Use:

``` python
pd.merge(...)
```

Why?

Because you are matching records using a key.

------------------------------------------------------------------------

## Example 2 --- Concat

You have:

``` text
January students
February students
March students
```

All have the same columns.

Use:

``` python
pd.concat(
    [january, february, march],
    ignore_index=True
)
```

Why?

Because you are stacking datasets.

------------------------------------------------------------------------

## Example 3 --- Join

You have two DataFrames whose indexes are:

``` text
student_id
```

and you want to combine their columns.

Use:

``` python
df1.join(df2)
```

Why?

Because the index is being used for alignment.

------------------------------------------------------------------------

# 28. Important Difference: `merge()` vs `concat()`

Suppose:

``` text
January:
Name Age Marks

February:
Name Age Marks
```

You want February below January.

Use:

``` python
pd.concat([january, february], ignore_index=True)
```

Do NOT use `merge()`.

But if you have:

``` text
Student:
ID Name

Marks:
ID Marks
```

and want:

``` text
ID Name Marks
```

use:

``` python
pd.merge(student, marks, on='ID')
```

------------------------------------------------------------------------

# 29. Important Difference: `merge()` vs `join()`

Both can combine related data, but their usual focus is different.

``` text
merge() → common column/key
join()  → index
```

Example:

``` python
pd.merge(
    students,
    marks,
    on='student_id'
)
```

versus:

``` python
students.join(marks)
```

where `student_id` is already the index.

------------------------------------------------------------------------

# 30. Common Mistakes

### Mistake 1

Thinking:

``` python
concat()
```

automatically matches IDs.

It does not work like a key-based merge.

------------------------------------------------------------------------

### Mistake 2

Forgetting `ignore_index=True`.

After vertical concatenation you may get:

``` text
0
1
2
0
1
2
```

Use:

``` python
ignore_index=True
```

when you want a fresh index.

------------------------------------------------------------------------

### Mistake 3

Confusing `axis`.

Remember:

``` text
axis=0 → vertical / rows
axis=1 → horizontal / columns
```

------------------------------------------------------------------------

### Mistake 4

Confusing `left` and `right`.

In:

``` python
pd.merge(df1, df2, how='left')
```

`df1` is the left DataFrame.

In:

``` python
df2.join(df1)
```

`df2` is the left DataFrame.

------------------------------------------------------------------------

# 31. Final Cheat Sheet

``` text
                 COMBINING DATAFRAMES
                         |
          ┌──────────────┼──────────────┐
          ↓              ↓              ↓
        MERGE          CONCAT          JOIN
          |              |              |
        Common          Stack          Index
         key           dataframes
          |              |
      how=inner       axis=0 / 1
      how=left        ignore_index
      how=right
      how=outer
```

## Remember in one line:

> **MERGE = Match, CONCAT = Stack, JOIN = Index**

------------------------------------------------------------------------

# 32. Quick Practice

### Q1

Two DataFrames have `student_id` in common. Combine their student and
marks information.

→ Use `merge()`.

### Q2

January and February datasets have identical columns. Put February below
January.

→ Use `concat()`.

### Q3

Two DataFrames use the same index and you want to combine their columns.

→ Use `join()`.

### Q4

Concatenate two DataFrames vertically and create a fresh index.

``` python
pd.concat([df1, df2], ignore_index=True)
```

### Q5

Merge and keep only matching IDs.

``` python
pd.merge(df1, df2, on='id', how='inner')
```

### Q6

Merge and keep every row from the first DataFrame.

``` python
pd.merge(df1, df2, on='id', how='left')
```

### Q7

Keep every key from both DataFrames.

``` python
pd.merge(df1, df2, on='id', how='outer')
```

### Q8

Concatenate two DataFrames horizontally.

``` python
pd.concat([df1, df2], axis=1)
```
