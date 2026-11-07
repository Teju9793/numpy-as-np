# 07 — Broadcasting in NumPy

> **Goal:** Understand how NumPy performs operations on arrays with different but compatible shapes, without manually repeating values.

## 1. The problem broadcasting solves

Suppose every student's score needs a bonus of 5:

```python
import numpy as np
scores = np.array([60, 70, 80])
print(scores + 5)
# [65 75 85]
```

NumPy behaves as if the scalar 5 were available for every element. This is broadcasting.

Broadcasting is a set of shape rules. It does not mean that NumPy permanently creates repeated copies of the smaller array.

## 2. The two basic compatibility rules

Compare shapes from **right to left**. Two dimensions are compatible when:
1. They are equal, or
2. One of them is 1.

If one shape has fewer dimensions, imagine adding 1s to its left until the number of dimensions matches.

### Example A: scalar with array

- Shape of array: `(3,)`
- Shape of scalar: `()`
- Result: `(3,)`

```python
np.array([1, 2, 3]) + 10
# [11 12 13]
```

### Example B: (2, 3) with (3,)

Compare:
```text
(2, 3)
(1, 3)  <- left-pad the shorter shape
------
(2, 3)  compatible
```

```python
A = np.array([[1, 2, 3],
              [4, 5, 6]])
b = np.array([10, 20, 30])
print(A + b)
# [[11 22 33]
#  [14 25 36]]
```

The row vector is applied to each row.

### Example C: (2, 1) with (1, 3)

```text
(2, 1)
(1, 3)
------
(2, 3)
```

```python
column = np.array([[1], [2]])       # (2, 1)
row = np.array([[10, 20, 30]])      # (1, 3)
print(column + row)
# [[11 21 31]
#  [12 22 32]]
```

Each row-column combination produces one output value.

## 3. When broadcasting fails

Shapes `(2, 3)` and `(2,)` are not compatible:

```text
(2, 3)
(1, 2)
------
3 != 2  -> incompatible
```

The dimensions from the right are 3 and 2. Neither is 1, so NumPy raises a broadcasting error.

If you intended to add one value to each row, make the second array a column:

```python
A = np.array([[1, 2, 3], [4, 5, 6]])
row_values = np.array([10, 20])
print(A + row_values[:, np.newaxis])
# [[11 12 13]
#  [24 25 26]]
```

## 4. Broadcasting for normalization

Suppose each feature has a different mean. Subtract the mean of each column from every row:

```python
X = np.array([[10, 100],
              [20, 200],
              [30, 300]])

column_means = X.mean(axis=0)
print(column_means)  # [ 20. 200.]

centered = X - column_means
print(centered)
# [[-10. -100.]
#  [  0.    0.]
#  [ 10.  100.]]
```

Here `X` has shape `(3, 2)` and `column_means` has shape `(2,)`. Broadcasting aligns the two feature columns.

## 5. A systematic way to solve shape questions

1. Write down both shapes.
2. Add leading 1s to the shorter shape.
3. Compare from right to left.
4. Every pair must be equal or contain a 1.
5. The output dimension at each position is the larger compatible value.

Example: `(5, 1, 4)` and `(1, 3, 4)` produce `(5, 3, 4)`.

## 6. Common mistakes

- Comparing shapes from left to right instead of right to left.
- Assuming any two arrays can be combined.
- Forgetting that `(n,)` and `(n, 1)` are different shapes.
- Using reshape blindly to fix an error without understanding what each axis means.
- Thinking broadcasting always allocates a full repeated copy.

## 7. Practice

For each pair, decide whether broadcasting works and state the output shape:
1. `(4, 3)` and `(3,)`
2. `(5, 1)` and `(1, 2)`
3. `(2, 3)` and `(2,)`
4. `(2, 1, 4)` and `(3, 4)`

Then verify using NumPy.

**Checkpoint:** Never guess broadcasting. Write the shapes, align from the right and apply the two rules.
