# 03 — Array Indexing, Slicing and Filtering

> **Goal:** Select one value, a row, a column, a range or values matching a condition.

## 1. Understand positions

NumPy uses **zero-based indexing**: the first element is at index 0, the second at index 1, and so on.

```python
import numpy as np
a = np.array([10, 20, 30, 40, 50])

print(a[0])   # 10
print(a[2])   # 30
print(a[-1])  # 50
print(a[-2])  # 40
```

Negative indexes count from the end: `-1` is the last item.

## 2. Slicing a 1-D array

Syntax: `array[start:stop:step]`

- start is included.
- stop is excluded.
- step controls how far to move each time.

```python
a = np.array([10, 20, 30, 40, 50, 60])

print(a[1:4])   # [20 30 40]
print(a[:3])    # [10 20 30]
print(a[3:])    # [40 50 60]
print(a[::2])   # [10 30 50]
print(a[::-1])  # [60 50 40 30 20 10]
```

A reliable way to predict `a[1:4]`: start at index 1, include indexes 1, 2 and 3, stop before index 4.

## 3. Indexing a 2-D array

Consider:

```python
m = np.array([[10, 20, 30],
              [40, 50, 60],
              [70, 80, 90]])
```

Visualize the indexes:

| | column 0 | column 1 | column 2 |
|---|---:|---:|---:|
| row 0 | 10 | 20 | 30 |
| row 1 | 40 | 50 | 60 |
| row 2 | 70 | 80 | 90 |

Use `m[row, column]`:

```python
print(m[0, 1])  # 20
print(m[2, 0])  # 70
print(m[1, 2])  # 60
```

You can also write `m[1][2]`, but `m[1, 2]` is the usual NumPy style.

## 4. Select complete rows and columns

```python
print(m[1, :])  # [40 50 60] second row
print(m[:, 1])  # [20 50 80] second column
print(m[:, 0:2])
# [[10 20]
#  [40 50]
#  [70 80]]
```

The colon means “take all values along this axis.” In `m[:, 1]`, take every row and column index 1.

## 5. Select a subarray

```python
print(m[0:2, 1:3])
# [[20 30]
#  [50 60]]
```

Trace the two slices independently:
- rows `0:2` selects row 0 and row 1.
- columns `1:3` selects column 1 and column 2.

The result shape is `(2, 2)`.

## 6. Boolean filtering — select using a condition

A comparison creates a Boolean array:

```python
marks = np.array([35, 72, 48, 90, 61])
passed = marks >= 40
print(passed)
# [False  True  True  True  True]
```

Use that Boolean array as a filter:

```python
print(marks[passed])
# [72 48 90 61]
```

Or combine both steps:

```python
print(marks[marks >= 40])
# [72 48 90 61]
```

This is extremely useful in data cleaning: select rows or values that satisfy a rule.

## 7. Combine conditions correctly

Use `&` for AND, `|` for OR, and `~` for NOT. Put each comparison inside parentheses.

```python
marks = np.array([35, 72, 48, 90, 61])

print(marks[(marks >= 40) & (marks < 75)])
# [72 48 61]

print(marks[(marks < 40) | (marks >= 90)])
# [35 90]
```

Do not use Python's `and` or `or` between NumPy arrays. Those operators expect a single truth value, while an array contains many values.

## 8. Fancy indexing — select chosen positions

Pass a list or array of indexes:

```python
a = np.array([100, 200, 300, 400, 500])
print(a[[0, 2, 4]])
# [100 300 500]
```

For rows:

```python
m = np.array([[1, 2], [3, 4], [5, 6]])
print(m[[0, 2]])
# [[1 2]
#  [5 6]]
```

Unlike basic slicing, integer-array (fancy) indexing returns a copy rather than a view.

## 9. View versus copy — an important safety concept

Basic slices usually create a **view**: a new way to look at the same underlying data. Changing the view can change the original array.

```python
a = np.array([10, 20, 30, 40])
part = a[1:3]
part[0] = 999

print(a)
# [ 10 999  30  40]
```

If you need independent data, explicitly copy:

```python
a = np.array([10, 20, 30, 40])
part = a[1:3].copy()
part[0] = 999

print(a)     # [10 20 30 40]
print(part)  # [999  30]
```

Rule of thumb: basic slicing generally gives a view; fancy indexing and Boolean indexing give copies. When ownership matters, use `.copy()` and test your assumptions.

## 10. Change selected values

```python
marks = np.array([35, 72, 48, 90])
marks[marks < 40] = 40
print(marks)
# [40 72 48 90]
```

This is called **conditional assignment**. It is often cleaner than looping through every element.

## 11. Common mistakes

1. Forgetting that slice stop is excluded.
2. Writing `m[1, :]` when you intended the second column; use `m[:, 1]`.
3. Using `and` instead of `&` for array conditions.
4. Forgetting parentheses around comparisons when combining conditions.
5. Modifying a slice and unintentionally changing the original array.
6. Confusing a 1-D result with a 2-D column: `m[:, 1]` has shape `(rows,)`; `m[:, 1:2]` has shape `(rows, 1)`.

## 12. Quick revision

- `a[i]`: one element; `a[start:stop:step]`: a slice.
- `m[row, column]`: one 2-D element.
- `m[:, j]`: all rows from column j.
- `array[condition]`: Boolean filtering.
- `array[[indexes]]`: fancy indexing.
- Use `.copy()` when you need independent data.

## 13. Practice

Given `a = np.array([5, 10, 15, 20, 25, 30])`:
1. Select 15.
2. Select the first four values.
3. Select every second value.
4. Reverse the array.
5. Select values greater than 15.

Given `m = np.arange(1, 13).reshape(3, 4)`:
1. Select the value 7.
2. Select the last column.
3. Select the first two rows.
4. Select the middle two columns.
5. Select values greater than 6.

**Checkpoint:** Before running each expression, write down the indexes or condition that will be selected. This habit makes slicing much easier.
