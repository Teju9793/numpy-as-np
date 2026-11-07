# 03 — Array Attributes and Data Types (dtype)

> **Goal:** Inspect an array, understand its data type, and choose a suitable type without losing information.

## 1. Why inspect an array?

Before calculating with data, check what you actually received. A dataset may contain the wrong shape, an unexpected data type, missing values or a much larger memory requirement than expected.

```python
import numpy as np
x = np.array([[10, 20, 30], [40, 50, 60]])

print(x.ndim)   # 2
print(x.shape)  # (2, 3)
print(x.size)   # 6
print(x.dtype)  # e.g. int64
print(x.itemsize) # bytes used by one element
print(x.nbytes)   # total bytes used by array elements
```

## 2. The core attributes

| Attribute | Meaning | Example |
|---|---|---|
| `ndim` | Number of axes | 2 |
| `shape` | Length along each axis | `(2, 3)` |
| `size` | Total number of elements | 6 |
| `dtype` | Type of each element | `int64` |
| `itemsize` | Bytes per element | often 8 for int64 |
| `nbytes` | Bytes for all array elements | `size * itemsize` |

For the example above, if each integer occupies 8 bytes, `nbytes` is (6 \times 8=48). The exact byte count depends on the dtype.

## 3. What is dtype?

A **data type** tells NumPy what kind of value an element stores and how that value is represented in memory.

Common types:
- `int32`, `int64`: signed integers.
- `float32`, `float64`: floating-point numbers.
- `bool_`: True or False.
- `complex64`, `complex128`: complex numbers.
- `str_` / Unicode string dtypes: text values.
- `object`: Python objects; flexible but often less efficient for numerical work.

```python
a = np.array([1, 2, 3])
b = np.array([1.5, 2.5, 3.5])
c = np.array([True, False, True])

print(a.dtype)
print(b.dtype)
print(c.dtype)
```

Default integer width may depend on platform. If the width matters, specify it explicitly.

## 4. Choose a dtype while creating an array

```python
a = np.array([1, 2, 3], dtype=np.int32)
b = np.array([1, 2, 3], dtype=np.float32)

print(a.dtype)  # int32
print(b.dtype)  # float32
```

Why use a smaller type? It may reduce memory use. But a smaller type has a smaller representable range or less precision. Do not choose a dtype only because its name looks efficient.

## 5. Convert an existing array with astype

`astype()` creates a converted array:

```python
scores = np.array([70, 80, 90])
decimal_scores = scores.astype(np.float64)

print(decimal_scores)       # [70. 80. 90.]
print(decimal_scores.dtype) # float64
```

A dangerous conversion is floating point to integer:

```python
values = np.array([2.9, 3.7, -1.8])
print(values.astype(int))
# [ 2  3 -1]
```

The fractional part is discarded (truncated toward zero), not rounded to the nearest integer. If rounding is intended, use `np.round(values).astype(int)`.

## 6. Integer overflow and precision

An integer dtype has a limited range. For example, a signed 8-bit integer can represent values from -128 through 127. Values outside the range cannot be represented correctly in that dtype.

Floating-point values also have finite precision. Many decimal fractions, such as 0.1, cannot be represented exactly in binary floating point.

```python
x = np.array([0.1, 0.2, 0.3])
print(x[0] + x[1] == x[2])
# commonly False
print(np.isclose(x[0] + x[1], x[2]))
# True
```

For approximate numerical comparisons, use `np.isclose` or `np.allclose`, not exact equality.

## 7. Missing and special numerical values

Floating-point arrays can represent:
- `np.nan`: not-a-number, often used for missing numerical data.
- `np.inf`: positive infinity.
- `-np.inf`: negative infinity.

```python
x = np.array([10.0, np.nan, 30.0, np.inf])
print(np.isnan(x))  # [False  True False False]
print(np.isinf(x))  # [False False False  True]
```

Ordinary integer dtypes do not have a built-in NaN value. Data analysis libraries may use nullable integer types or other missing-value representations.

## 8. Practical dtype checklist

1. Is the data numeric, Boolean or text?
2. Does the chosen type cover the full value range?
3. Do you need decimal precision?
4. Are missing values possible?
5. Does reducing memory matter for this dataset?
6. Could conversion truncate or overflow values?

## 9. Common mistakes

- Assuming every computer uses the same default integer dtype.
- Converting floats to integers and silently losing decimal parts.
- Comparing floating-point calculations with `==`.
- Assuming `nbytes` includes every Python object or all surrounding overhead; it reports the array element buffer size.
- Using `object` dtype for numerical data without a reason.

## 10. Practice

1. Create an array of 12 float values and inspect its `dtype`, `shape` and `nbytes`.
2. Convert it to `float32`. Compare memory use.
3. Convert `[1.2, 2.8, 3.5]` to integers. Explain what happened to the decimals.
4. Create an array containing NaN and identify the missing position using `np.isnan`.

**Checkpoint:** You should be able to explain what dtype means and why converting a dtype can change the information stored.
