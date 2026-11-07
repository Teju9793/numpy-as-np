# 06 — Reshaping, Transpose and Axis Operations

> **Goal:** Change the organization of array data while preserving values, and understand how axis-based reductions work.

## 1. Shape describes organization

An array with shape `(2, 3)` has two rows and three columns. Its total number of elements is (2\times3=6).

```python
import numpy as np
x = np.arange(6)
print(x.shape)  # (6,)
```

A 1-D array is not automatically a row or column matrix. Its shape is simply `(6,)`.

## 2. Reshape

```python
x = np.arange(1, 7)
print(x.reshape(2, 3))
# [[1 2 3]
#  [4 5 6]]
```

Reshape changes the arrangement, not the number of values. The product of the new dimensions must equal the original size.

Valid shapes for 12 elements include `(3, 4)`, `(2, 6)`, `(12, 1)` and `(2, 2, 3)`.

## 3. Infer one dimension with -1

```python
x = np.arange(12)
print(x.reshape(3, -1).shape)  # (3, 4)
print(x.reshape(-1, 2).shape)  # (6, 2)
```

NumPy calculates the missing dimension from the total size. Only one dimension can be inferred with `-1`.

## 4. Flatten and ravel

```python
m = np.array([[1, 2, 3], [4, 5, 6]])
print(m.flatten())  # [1 2 3 4 5 6]
print(m.ravel())    # [1 2 3 4 5 6]
```

- `flatten()` returns a copy.
- `ravel()` returns a view when possible; otherwise it creates a copy.

## 5. Transpose

```python
m = np.array([[1, 2, 3], [4, 5, 6]])
print(m.T)
# [[1 4]
#  [2 5]
#  [3 6]]
```

For a 2-D array, transpose swaps rows and columns. A shape of `(2, 3)` becomes `(3, 2)`. A 1-D array remains 1-D after `.T`.

To create a column from a 1-D array, use `x.reshape(-1, 1)` or `x[:, np.newaxis]`.

## 6. Understand axis with a concrete example

```python
scores = np.array([[10, 20, 30],
                   [40, 50, 60]])

print(scores.sum(axis=0))  # [50 70 90]
print(scores.sum(axis=1))  # [ 60 150]
```

Imagine rows are students and columns are subjects:
- `axis=0` collapses the student axis, leaving one total per subject.
- `axis=1` collapses the subject axis, leaving one total per student.

Memory aid: the axis named in a reduction is the direction being collapsed. Check the output shape to verify.

## 7. Keep dimensions with keepdims

```python
x = np.array([[1, 2, 3], [4, 5, 6]])
print(x.mean(axis=1).shape)                 # (2,)
print(x.mean(axis=1, keepdims=True).shape)  # (2, 1)
```

`keepdims=True` keeps the reduced axis with length 1. This can make later broadcasting easier.

## 8. Add an axis

```python
x = np.array([10, 20, 30])
print(x[:, np.newaxis].shape)  # (3, 1)
print(x[np.newaxis, :].shape)  # (1, 3)
```

This is useful when an ML library expects a column feature matrix instead of a 1-D vector.

## 9. Common errors and debugging

- Reshape fails: check that the product of new dimensions equals `size`.
- Transpose seems wrong: write down what each axis represents before and after.
- Axis reduction returns an unexpected shape: identify which axis was removed.
- A 1-D array does not become a column using `.T`: explicitly add a dimension.
- Flattening may allocate a copy; do not assume it shares memory.

## 10. Practice

1. Reshape 18 values into `(3, 6)`.
2. Use `-1` to reshape 18 values into 2 columns.
3. Transpose an array with shape `(4, 2)`.
4. For a 3-by-4 array, predict the shapes of `sum(axis=0)` and `sum(axis=1)`.
5. Repeat the previous sums with `keepdims=True`.

**Checkpoint:** Explain both the numerical result and the output shape of every axis operation.
