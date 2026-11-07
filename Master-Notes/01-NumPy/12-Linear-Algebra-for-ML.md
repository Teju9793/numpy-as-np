# 12 — Linear Algebra with NumPy for Machine Learning

> **Goal:** Understand vectors, matrices, dot products, matrix multiplication and a few essential linear algebra operations used in ML.

## 1. What is linear algebra?

Linear algebra is the mathematics of vectors and matrices. Machine learning uses it to represent datasets, combine features with weights and transform numerical information.

- **Scalar:** one number, such as 5.
- **Vector:** an ordered collection of numbers, such as [2, 4, 6].
- **Matrix:** a rectangular arrangement of numbers in rows and columns.
- **Shape:** the dimensions of an array.

NumPy represents these structures using `ndarray`.

## 2. Create vectors and matrices

```python
import numpy as np
v = np.array([2, 4, 6])
A = np.array([[1, 2],
              [3, 4]])
print(v.shape)  # (3,)
print(A.shape)  # (2, 2)
```

A 1-D NumPy vector has one axis. A 2-D matrix has two axes.

## 3. Dot product of two vectors

The dot product multiplies matching elements and adds the results:

[
[2,3]\cdot[4,5] = 2\times4 + 3\times5 = 23
]

```python
a = np.array([2, 3])
b = np.array([4, 5])
print(np.dot(a, b))  # 23
print(a @ b)         # 23
```

For 1-D vectors, `@` gives the dot product.

## 4. Matrix multiplication

For matrix multiplication, the number of columns in the first matrix must equal the number of rows in the second.

If A has shape `(m, n)` and B has shape `(n, p)`, the result has shape `(m, p)`.

```python
A = np.array([[1, 2],
              [3, 4]])
B = np.array([[5, 6],
              [7, 8]])

print(A @ B)
# [[19 22]
#  [43 50]]
```

Trace the top-left value:
(1\times5 + 2\times7 = 19).

Trace the top-right value:
(1\times6 + 2\times8 = 22).

Use `@` or `np.matmul` for matrix multiplication. `A * B` is element-wise multiplication.

## 5. Matrix transpose

```python
A = np.array([[1, 2, 3],
              [4, 5, 6]])
print(A.T)
# [[1 4]
#  [2 5]
#  [3 6]]
```

Transpose swaps rows and columns. It is frequently used to align dimensions for matrix operations.

## 6. Identity matrix

An identity matrix has ones on its main diagonal and zeros elsewhere:

```python
I = np.eye(3)
print(I)
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]
```

For compatible matrices, multiplying by the identity leaves the matrix unchanged: (AI=A) and (IA=A).

## 7. Determinant and inverse

```python
A = np.array([[4.0, 7.0],
              [2.0, 6.0]])

print(np.linalg.det(A))  # approximately 10
print(np.linalg.inv(A))
```

The determinant indicates whether a square matrix is singular. A square matrix has an inverse only when it is non-singular (determinant is non-zero in exact mathematics).

In practical numerical work, avoid calculating an inverse just to solve (Ax=b). Prefer:

```python
b = np.array([1.0, 2.0])
solution = np.linalg.solve(A, b)
print(solution)
```

This is generally more numerically appropriate and efficient than explicitly computing `inv(A) @ b`.

## 8. Norms and vector length

A norm measures the size or length of a vector.

```python
v = np.array([3, 4])
print(np.linalg.norm(v))  # 5.0
```

For the Euclidean norm: (sqrt{3^2+4^2}=5).

Norms are used in distance calculations and regularization in machine learning.

## 9. How ML uses matrix multiplication

A simple linear model can be written:

[
\hat{y}=Xw+b
]

- (X): feature matrix, shape ((n\_samples,n\_features)).
- (w): weight vector, shape ((n\_features,)).
- (b): one bias value.
- (hat y): predicted value for each sample.

```python
X = np.array([[1, 2],
              [3, 4],
              [5, 6]])
w = np.array([0.5, 2.0])
b = 1.0

predictions = X @ w + b
print(predictions)
# [ 5.5 10.5 15.5]
```

For the first sample: (1\times0.5 + 2\times2 + 1 = 5.5).

## 10. Common mistakes

- Using `*` instead of `@` for matrix multiplication.
- Forgetting the inner-dimension compatibility rule.
- Assuming every square matrix has an inverse.
- Using an explicit inverse when `np.linalg.solve` is the better tool.
- Forgetting that a 1-D vector and a 2-D column matrix have different shapes.

## 11. Practice

1. Calculate the dot product of `[1, 2, 3]` and `[4, 5, 6]`.
2. Multiply a `(2, 3)` matrix by a `(3, 2)` matrix.
3. Explain why a `(2, 3)` matrix cannot multiply a `(2, 2)` matrix in that order.
4. Use `np.linalg.solve` to solve a small system of linear equations.
5. Calculate the length of vector `[6, 8]`.

**Checkpoint:** Before using `@`, check the two matrix shapes and confirm that the inner dimensions match.
