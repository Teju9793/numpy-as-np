# 04 — Array Shape, Reshaping and Transposing

> **Goal:** Understand array dimensions, reshape data without changing its values, and recognize when a shape mismatch causes an error.

## 1. Why shape matters

A machine-learning model expects data in a particular arrangement. For example, a model may expect 100 examples with 3 features each. The feature array must therefore have shape `(100, 3)`.

Shape is not decoration. It tells Python how values are organized.

```python
import numpy as np

x = np.array([1, 2, 3, 4, 5, 6])
print(x.shape)  # (6,)
```

This is a 1-D array containing six values. It is not a row matrix of shape `(1, 6)`, nor a column matrix of shape `(6, 1)`.

## 2. Reshape an array

Syntax: `array.reshape(new_shape)`

```python
x = np.array([1, 2, 3, 4, 5, 6])
y = x.reshape(2, 3)

print(y)
# [[1 2 3]
#  [4 5 6]]
print(y.shape)  # (2, 3)
```

NumPy fills the new shape using the existing element order (by default, row-major/C-style order). It does not invent or remove values.

### The element-count rule

A reshape is possible only when the total number of elements stays the same.

For six elements:
- `(2, 3)` is valid because (2 \times 3=6).
- `(3, 2)` is valid because (3 \times 2=6).
- `(2, 2)` is invalid because (2 \times 2=4).

```python
x.reshape(3, 2)  # valid
# x.reshape(2, 2)  # ValueError: size does not match
```

## 3. Use -1 when one dimension can be inferred

You can let NumPy calculate one dimension:

```python
x = np.arange(12)
print(x.reshape(3, -1))
# [[ 0  1  2  3]
#  [ 4  5  6  7]
#  [ 8  9 10 11]]
```

NumPy knows there are 12 values and 3 rows, so it infers (12/3=4) columns.

Only one dimension may be inferred with `-1` in a reshape call.

## 4. Flatten and ravel — convert to 1-D

```python
m = np.array([[1, 2, 3], [4, 5, 6]])

print(m.flatten())  # [1 2 3 4 5 6]
print(m.ravel())    # [1 2 3 4 5 6]
```

- `flatten()` returns a copy.
- `ravel()` returns a flattened view where possible; it may need to make a copy depending on memory layout.

If you intend to edit the flattened result without affecting the original, `flatten()` is the safer choice.

## 5. Transpose — swap axes

For a 2-D array, transpose changes rows into columns and columns into rows.

```python
m = np.array([[1, 2, 3],
              [4, 5, 6]])

print(m.T)
# [[1 4]
#  [2 5]
#  [3 6]]
print(m.T.shape)  # (3, 2)
```

Original shape: `(2, 3)`. Transposed shape: `(3, 2)`.

The values are not sorted or reversed; the axes are exchanged. For a 1-D array, `x.T` remains 1-D. To turn a 1-D array into a column, use `x.reshape(-1, 1)`.

## 6. Add a dimension with `np.newaxis`

`np.newaxis` (an alias for `None` in indexing) adds a new axis.

```python
x = np.array([10, 20, 30])

column = x[:, np.newaxis]
row = x[np.newaxis, :]

print(column)
# [[10]
#  [20]
#  [30]]
print(column.shape)  # (3, 1)
print(row.shape)     # (1, 3)
```

This distinction matters when combining arrays or passing data to ML libraries.

## 7. Combine arrays with concatenate

`np.concatenate((a, b), axis=...)` joins arrays along an existing axis.

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[5, 6]])

print(np.concatenate((a, b), axis=0))
# [[1 2]
#  [3 4]
#  [5 6]]
```

For axis 0, the arrays must have matching sizes on all other axes. Here both have two columns.

Joining side by side:

```python
a = np.array([[1, 2], [3, 4]])
b = np.array([[5], [6]])

print(np.concatenate((a, b), axis=1))
# [[1 2 5]
#  [3 4 6]]
```

For axis 1, both arrays need the same number of rows.

## 8. Stack arrays — create a new axis

`np.stack` joins arrays along a **new** axis. The input arrays must have the same shape.

```python
a = np.array([1, 2])
b = np.array([3, 4])

print(np.stack((a, b), axis=0))
# [[1 2]
#  [3 4]]
print(np.stack((a, b), axis=1))
# [[1 3]
#  [2 4]]
```

Compare:
- `concatenate`: joins along an axis that already exists.
- `stack`: introduces a new axis.

## 9. Shape reasoning in machine learning

Suppose 5 students each have 3 features: attendance, assignment score and test score.

```python
X = np.array([
    [90, 80, 75],
    [85, 70, 82],
    [95, 90, 88],
    [60, 65, 58],
    [75, 78, 80]
])

print(X.shape)  # (5, 3)
```

Interpretation:
- 5 rows = 5 samples/students.
- 3 columns = 3 features per sample.

A model expecting 3 features should receive data with 3 columns. If you accidentally transpose this array, its shape becomes `(3, 5)`: now it appears to contain 3 samples with 5 features, which changes the meaning of the data.

## 10. Common shape debugging routine

When an operation fails:
1. Print each array's `.shape`.
2. Identify what each axis represents.
3. Check whether element counts match (for reshape).
4. Check whether non-joined axes match (for concatenate).
5. Check whether input shapes match (for stack).
6. Use a tiny array and calculate the expected arrangement by hand.

## 11. Quick revision

| Operation | Meaning |
|---|---|
| `reshape(2, 3)` | Rearrange into 2 rows, 3 columns |
| `reshape(-1, 1)` | Make a column; infer row count |
| `flatten()` | Flatten and return a copy |
| `ravel()` | Flatten; view where possible |
| `.T` | Transpose axes (2-D: rows ↔ columns) |
| `np.newaxis` | Insert a dimension |
| `concatenate` | Join along an existing axis |
| `stack` | Join along a new axis |

## 12. Practice

1. Reshape 24 values into shape `(4, 6)`.
2. Reshape the same values into 3 rows, letting NumPy infer the columns.
3. Convert a 1-D array of 5 values into shape `(5, 1)`.
4. Transpose a `(2, 4)` array and state the new shape.
5. Concatenate arrays of shapes `(2, 3)` and `(4, 3)` along axis 0. Is it valid?
6. Can arrays of shapes `(2, 3)` and `(2, 4)` be concatenated along axis 0? Explain which dimension prevents it.

**Checkpoint:** Always say the shape aloud as “samples by features” or “rows by columns” in the context of your data. Shape becomes meaningful when you attach a real-world meaning to each axis.
