# 01 — NumPy Fundamentals: Understand Arrays Before Using Them

> **Goal:** Understand what NumPy is, why arrays matter in data science, how an ndarray stores data, and how to inspect an array confidently.

## 1. Start with the problem

Python already has lists. So why do data scientists use NumPy?

Imagine you have marks for 1,000 students and want to add 5 marks to every student. With a normal list, you usually write a loop:

```python
marks = [60, 72, 81, 55]
updated = []
for mark in marks:
    updated.append(mark + 5)
print(updated)
# [65, 77, 86, 60]
```

NumPy lets you express the same operation directly:

```python
import numpy as np

marks = np.array([60, 72, 81, 55])
updated = marks + 5
print(updated)
# [65 77 86 60]
```

The second version is shorter, and NumPy performs the operation efficiently over the whole array. This style is called **vectorization**.

## 2. What is NumPy?

**NumPy (Numerical Python)** is a Python library for working with numerical data. Its central object is the **ndarray**, short for *N-dimensional array*.

An array is a collection of values arranged in a regular structure:
- 1-D: a line of values
- 2-D: rows and columns, like a table or matrix
- 3-D: a stack of 2-D arrays
- Higher dimensions: more axes, useful for images, batches and tensors

```python
import numpy as np

one_d = np.array([10, 20, 30])
two_d = np.array([[10, 20, 30],
                  [40, 50, 60]])
three_d = np.array([
    [[1, 2], [3, 4]],
    [[5, 6], [7, 8]]
])
```

## 3. Python list versus NumPy array

| Feature | Python list | NumPy ndarray |
|---|---|---|
| Typical use | General collections | Numerical computation |
| Data types | Can mix types | Usually one common dtype |
| Arithmetic | Often needs loops | Vectorized operations |
| Dimensions | Nested lists | Explicit axes and shape |
| Numerical performance | More overhead | Optimized numerical operations |

A NumPy array normally stores elements of one data type. This makes its memory layout predictable and calculations efficient. If you mix integers and floats, NumPy may promote the values to a common type.

```python
a = np.array([1, 2, 3])
b = np.array([1, 2.5, 3])
print(a.dtype)  # commonly int64 (platform-dependent)
print(b)        # [1.  2.5 3. ]
print(b.dtype)  # commonly float64
```

Do not memorize a particular integer width from one computer: the exact default integer type can depend on the platform and NumPy build.

## 4. Create your first arrays

```python
a = np.array([2, 4, 6, 8])
b = np.array([[1, 2], [3, 4]])

print(a)
print(b)
```

Output:
```text
[2 4 6 8]
[[1 2]
 [3 4]]
```

The outer square brackets describe the collection. In a 2-D array, each inner list becomes one row.

## 5. Four properties you must learn

Use these properties whenever you receive an unfamiliar array.

```python
data = np.array([[10, 20, 30],
                 [40, 50, 60]])

print(data.ndim)   # 2
print(data.shape)  # (2, 3)
print(data.size)   # 6
print(data.dtype)  # e.g. int64
```

- **ndim:** number of dimensions (number of axes).
- **shape:** length along each axis. `(2, 3)` means 2 rows and 3 columns.
- **size:** total number of elements. Here, (2 \times 3 = 6).
- **dtype:** data type of the elements.

### Shape-reading trick

Read a shape from left to right, outermost dimension first. For `(4, 3, 2)`:
- 4 groups
- each group contains 3 rows
- each row contains 2 values

Total elements: (4 \times 3 \times 2 = 24).

## 6. What does an axis mean?

An **axis** is a direction along an array.

For a 2-D array:
- axis 0 moves down the rows. Reducing along axis 0 combines values vertically.
- axis 1 moves across the columns. Reducing along axis 1 combines values horizontally.

```python
x = np.array([[1, 2, 3],
              [4, 5, 6]])

print(x.sum(axis=0))  # [5 7 9]  column totals
print(x.sum(axis=1))  # [ 6 15]  row totals
```

Trace it:
- axis 0: (1+4=5), (2+5=7), (3+6=9).
- axis 1: (1+2+3=6), (4+5+6=15).

For a 3-D array, there are three axes. Do not rely on phrases such as “axis 0 is always rows”; first inspect the shape and identify what each axis represents in your data.

## 7. Vectorized arithmetic

```python
a = np.array([10, 20, 30])
b = np.array([1, 2, 3])

print(a + b)   # [11 22 33]
print(a - b)   # [ 9 18 27]
print(a * b)   # [10 40 90]
print(a / b)   # [10. 10. 10.]
print(a ** 2)  # [100 400 900]
```

These operations are element-by-element. The first element of `a` combines with the first element of `b`, and so on. This is not matrix multiplication; matrix multiplication is covered later.

Scalar operations apply to every element:

```python
temperature = np.array([21, 23, 25])
print((temperature * 9 / 5) + 32)
# [69.8 73.4 77. ]
```

## 8. Why NumPy matters in data science and ML

- **Data preparation:** clean, filter and transform numerical columns.
- **Statistics:** calculate mean, median, variance and standard deviation.
- **Machine learning:** represent feature matrices and target arrays.
- **Images:** store pixel intensities as multidimensional arrays.
- **Scientific computing:** perform linear algebra and numerical simulations.

A common ML convention is:
- (X): feature matrix with shape ((n\_samples, n\_features))
- (y): target values, often shape ((n\_samples,))

For example, 100 students and 4 measured features gives `X.shape == (100, 4)`.

## 9. Common mistakes

1. **Confusing size and shape:** `size` is one total count; `shape` is a tuple describing each dimension.
2. **Assuming every array is 2-D:** a single feature column might have shape `(n,)` or `(n, 1)`; these are different.
3. **Calling element-wise multiplication matrix multiplication:** use `@ ` or `np.matmul` for matrix multiplication.
4. **Ignoring dtype:** integer arrays cannot always represent decimal results when values are assigned back into them.
5. **Guessing axes:** verify with a tiny example and calculate the expected result manually.

## 10. Quick revision

- NumPy's main structure is the N-dimensional `ndarray`.
- `ndim` = number of axes; `shape` = length of each axis; `size` = total elements; `dtype` = element type.
- Vectorization applies operations to whole arrays without writing an explicit Python loop.
- For a 2-D array, axis 0 is vertical (rows are combined); axis 1 is horizontal (columns are combined).

## 11. Practice

1. Create a 1-D array containing 5, 10, 15, 20. Print its `ndim`, `shape`, `size` and `dtype`.
2. Create a 3-by-2 array. How many elements does it contain?
3. For `[[2, 4], [6, 8], [10, 12]]`, calculate the result of `sum(axis=0)` and `sum(axis=1)` by hand before running the code.
4. Convert Celsius values `[0, 20, 37]` to Fahrenheit using one vectorized expression.

**Checkpoint:** If you can explain why a shape of `(3, 2)` has six values and trace both axis sums, you have the foundation needed for the next chapter.
