# 05 — NumPy Array Operations

> **Goal:** Perform arithmetic, comparisons and mathematical functions on arrays, and distinguish element-wise operations from matrix multiplication.

## 1. Element-wise arithmetic

When two compatible arrays are added, subtracted, multiplied or divided, NumPy works position by position.

```python
import numpy as np
a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

print(a + b)   # [11 22 33]
print(a - b)   # [ 9 18 27]
print(a * b)   # [10 40 90]
print(a / b)   # [10. 10. 10.]
print(a ** 2)  # [100 400 900]
print(a % 4)   # [2 0 2]
```

The multiplication `a * b` is not matrix multiplication. It multiplies matching positions.

## 2. Scalar operations

A scalar is one single value. NumPy applies it to every element:

```python
prices = np.array([100, 200, 300])
discounted = prices * 0.9
print(discounted)
# [ 90. 180. 270.]
```

This is one of the most common ways to transform a full numerical column.

## 3. Comparison operations

Comparisons return Boolean arrays:

```python
scores = np.array([35, 60, 85, 45])
print(scores >= 50)
# [False  True  True False]
```

Other operators include `<`, `<=`, `>`, `==` and `!=`. Use the resulting mask for filtering.

## 4. Universal functions (ufuncs)

A **ufunc** is a NumPy function designed to operate element-wise over arrays.

```python
x = np.array([1, 4, 9, 16])
print(np.sqrt(x))  # [1. 2. 3. 4.]
print(np.exp(x))   # exponential of each value
print(np.log(x))   # natural logarithm of each value
print(np.abs([-3, 0, 5])) # [3 0 5]
```

Useful functions:
- `np.sqrt(x)`: square root.
- `np.abs(x)`: absolute value.
- `np.exp(x)`: (e^x).
- `np.log(x)`: natural logarithm.
- `np.sin(x)`, `np.cos(x)`: trigonometric functions (input in radians).
- `np.round(x, decimals=2)`: round for display or a chosen precision.

## 5. Element-wise minimum and maximum

```python
a = np.array([10, 50, 30])
b = np.array([20, 40, 60])

print(np.maximum(a, b))  # [20 50 60]
print(np.minimum(a, b))  # [10 40 30]
```

These compare matching positions. For one overall maximum or minimum, use `np.max` or `np.min`.

## 6. Element-wise multiplication versus matrix multiplication

```python
A = np.array([[1, 2], [3, 4]])
B = np.array([[5, 6], [7, 8]])

print(A * B)
# [[ 5 12]
#  [21 32]]

print(A @ B)
# [[19 22]
#  [43 50]]
```

For `A @ B`, each result cell is a row-by-column dot product. Top-left is (1\times5 + 2\times7 = 19). Matrix multiplication is covered in the linear algebra chapter.

## 7. Rounding and clipping

```python
x = np.array([1.234, 2.567, 3.891])
print(np.round(x, 2))
# [1.23 2.57 3.89]

marks = np.array([-5, 40, 120])
print(np.clip(marks, 0, 100))
# [  0  40 100]
```

Clipping limits values to a chosen interval. It is useful for keeping percentages between 0 and 100, but do not clip data unless the domain rules justify it.

## 8. Handling invalid numerical results

Division by zero and invalid logarithms can produce infinity or NaN, sometimes with a warning.

```python
x = np.array([1.0, 0.0, -1.0])
print(np.isfinite(x))  # [ True  True  True]
```

Use `np.isfinite`, `np.isnan` and `np.isinf` to detect special values. For logarithms, the natural logarithm is defined for positive real inputs; zero and negative values need deliberate handling.

## 9. Common mistakes

- Assuming `*` performs matrix multiplication.
- Forgetting that trigonometric functions use radians.
- Treating rounded display as proof that the stored float is exact.
- Ignoring NaN or infinity after calculations.
- Applying clipping without understanding whether out-of-range values are errors or meaningful observations.

## 10. Practice

1. Apply a 10% discount to `[250, 500, 750]`.
2. Find which values in `[12, 35, 48, 60]` are at least 40.
3. Apply square root to `[0, 1, 4, 9, 16]`.
4. Compare `A * B` and `A @ B` for two 2-by-2 arrays.
5. Clip `[-10, 30, 105]` to the interval 0–100.

**Checkpoint:** Know whether an operation is element-wise, scalar-to-array, or matrix multiplication before predicting its output.
