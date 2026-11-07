# 04 — Indexing, Slicing and Filtering

> **Goal:** Select values precisely from 1-D and 2-D arrays, filter using conditions, and understand when selections share memory.

## 1. Indexing starts at zero

```python
import numpy as np
a = np.array([10, 20, 30, 40, 50])
print(a[0])   # 10
print(a[2])   # 30
print(a[-1])  # 50
```

The first element has index 0. Negative indexes count backward from the end.

## 2. Slicing: start, stop and step

Syntax: `a[start:stop:step]`
- start is included.
- stop is excluded.
- step is the distance between selected indexes.

```python
a = np.array([10, 20, 30, 40, 50, 60])
print(a[1:4])   # [20 30 40]
print(a[:3])    # [10 20 30]
print(a[3:])    # [40 50 60]
print(a[::2])   # [10 30 50]
print(a[::-1])  # [60 50 40 30 20 10]
```

For `a[1:4]`, select indexes 1, 2 and 3. Stop before index 4.

## 3. Indexing a 2-D array

```python
m = np.array([[10, 20, 30],
              [40, 50, 60],
              [70, 80, 90]])
print(m[1, 2])  # 60: row 1, column 2
print(m[2, 0])  # 70
```

Use `m[row, column]`. Remember that both row and column indexes start at zero.

## 4. Select rows, columns and blocks

```python
print(m[1, :])     # second row: [40 50 60]
print(m[:, 1])     # second column: [20 50 80]
print(m[0:2, 1:3])
# [[20 30]
#  [50 60]]
```

The colon by itself means “take all values along this axis.” In `m[:, 1]`, take every row and only column 1.

## 5. Boolean filtering

A comparison creates a Boolean mask:

```python
marks = np.array([35, 72, 48, 90, 61])
mask = marks >= 40
print(mask)
# [False  True  True  True  True]
print(marks[mask])
# [72 48 90 61]
```

You can write `marks[marks >= 40]` directly. This is useful for filtering out-of-range measurements, selecting customers or finding students who passed.

## 6. Combine conditions

Use `&` for AND, `|` for OR, and `~` for NOT. Put each comparison in parentheses.

```python
marks = np.array([35, 72, 48, 90, 61])
print(marks[(marks >= 40) & (marks < 75)])
# [72 48 61]
print(marks[(marks < 40) | (marks >= 90)])
# [35 90]
```

Do not use Python's `and` and `or` between arrays: an array has multiple truth values.

## 7. Fancy indexing

Pass a list or array of integer indexes:

```python
a = np.array([100, 200, 300, 400, 500])
print(a[[0, 2, 4]])
# [100 300 500]
```

Fancy indexing selects the exact positions you list. Unlike basic slicing, it returns a copy.

## 8. Views and copies

A basic slice usually creates a **view**, which shares data with the original array:

```python
a = np.array([10, 20, 30, 40])
part = a[1:3]
part[0] = 999
print(a)  # [ 10 999  30  40]
```

Use `.copy()` when you need independent data:

```python
a = np.array([10, 20, 30, 40])
part = a[1:3].copy()
part[0] = 999
print(a)     # [10 20 30 40]
print(part)  # [999  30]
```

Basic slicing generally returns views; integer-array and Boolean indexing return copies. Use `.copy()` explicitly when ownership matters.

## 9. Conditional assignment

```python
marks = np.array([35, 72, 48, 90])
marks[marks < 40] = 40
print(marks)
# [40 72 48 90]
```

This replaces every value selected by the condition. It is often simpler than writing a loop.

## 10. One-dimensional versus column shape

```python
m = np.array([[1, 2], [3, 4], [5, 6]])
print(m[:, 1].shape)    # (3,)
print(m[:, 1:2].shape)  # (3, 1)
```

The first expression returns a 1-D array. The second preserves a 2-D column. This difference often matters when passing data to machine-learning libraries.

## 11. Common mistakes

- Forgetting that the stop index is excluded.
- Mixing up `m[1, :]` (row) and `m[:, 1]` (column).
- Using `and` instead of `&`.
- Forgetting parentheses around comparisons.
- Changing a view and unintentionally changing the original array.
- Assuming a selected column is always 2-D.

## 12. Practice

For `a = np.array([5, 10, 15, 20, 25, 30])`, select 15, the first four values, every second value, the reversed array and values greater than 15.

For `m = np.arange(1, 13).reshape(3, 4)`, select the last column, first two rows, middle two columns and all values greater than 6.

**Checkpoint:** Trace the selected indexes before running the expression. This is the fastest way to become confident with slicing.
