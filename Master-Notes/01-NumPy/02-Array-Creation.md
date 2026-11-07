# 02 — Creating NumPy Arrays

> **Goal:** Choose the correct array-creation function, understand its parameters, and predict the values and shape it produces.

## 1. Why are there different creation functions?

Sometimes you already have data and want to convert it into an array. At other times, you need a sequence, a matrix filled with zeros, or random values for an experiment. NumPy provides separate functions because each task has a different meaning.

Start with:

```python
import numpy as np
```

## 2. `np.array()` — convert existing data

**Purpose:** Create an ndarray from a list, tuple or nested sequence.

Syntax: `np.array(object, dtype=None)`

- `object`: the input data.
- `dtype`: optional data type to request.

```python
a = np.array([10, 20, 30])
b = np.array([[1, 2], [3, 4]])
c = np.array([1, 2, 3], dtype=float)

print(a)  # [10 20 30]
print(b)  # [[1 2]
          #  [3 4]]
print(c)  # [1. 2. 3.]
```

Use nested lists with consistent lengths to create a regular multidimensional array. Ragged nested sequences are not a normal rectangular numeric matrix; current NumPy versions generally require explicitly requesting `dtype=object` for such data.

## 3. `np.arange()` — create a sequence using a step

Syntax: `np.arange(start, stop, step, dtype=None)`

- `start`: first value (default 0).
- `stop`: stopping boundary, excluded.
- `step`: difference between successive values (default 1).

```python
print(np.arange(5))
# [0 1 2 3 4]

print(np.arange(2, 10, 2))
# [2 4 6 8]

print(np.arange(10, 1, -2))
# [10  8  6  4  2]
```

**Important:** the stop value is not included. A useful mental model is “start here, keep adding step, stop before reaching the boundary.”

For floating-point steps, rounding can make the number of values surprising. If you need a fixed number of evenly spaced samples, prefer `np.linspace()`.

## 4. `np.linspace()` — create a fixed number of evenly spaced values

Syntax: `np.linspace(start, stop, num=50, endpoint=True)`

- `start`: first value.
- `stop`: final value when `endpoint=True`.
- `num`: number of samples, not the step size.
- `endpoint`: whether to include the stop value.

```python
x = np.linspace(0, 10, 5)
print(x)
# [ 0.   2.5  5.   7.5 10. ]
```

Step-by-step:
1. The interval length is (10-0=10).
2. Five points including both endpoints create four gaps.
3. Gap size is (10/4=2.5).
4. Values: 0, 2.5, 5, 7.5, 10.

If `endpoint=False`, the stop value is excluded and the spacing changes.

## 5. `arange` versus `linspace`

| Question | Use |
|---|---|
| “Give me values increasing by 2” | `arange` |
| “Give me exactly 8 samples from 0 to 1” | `linspace` |
| Need reliable fixed sample count | `linspace` |
| Need a known step size | `arange` |

## 6. Arrays filled with a constant

### `np.zeros(shape)`

Creates an array filled with zeros.

```python
print(np.zeros((2, 3)))
# [[0. 0. 0.]
#  [0. 0. 0.]]
```

### `np.ones(shape)`

Creates an array filled with ones.

```python
print(np.ones((2, 2), dtype=int))
# [[1 1]
#  [1 1]]
```

### `np.full(shape, fill_value)`

Creates an array filled with your chosen value.

```python
print(np.full((2, 3), 7))
# [[7 7 7]
#  [7 7 7]]
```

The shape is a tuple. `(2, 3)` means two rows and three columns. The default dtype for `zeros` and `ones` is floating point unless you specify another type.

## 7. `np.empty(shape)` — allocate without initializing values

```python
a = np.empty((2, 2))
print(a)
```

The displayed values are **not predictable**. `empty` reserves memory but does not fill it with zeros. It can be useful when you will immediately overwrite every element and want to avoid initialization work.

Do not use `empty` when you need known starting values. Use `zeros` or `ones` instead.

## 8. Identity and diagonal matrices

### `np.eye(n)`

Creates a 2-D array with ones on the main diagonal and zeros elsewhere.

```python
print(np.eye(3))
# [[1. 0. 0.]
#  [0. 1. 0.]
#  [0. 0. 1.]]
```

### `np.diag(values)`

When given a 1-D sequence, places its values on a diagonal:

```python
print(np.diag([4, 5, 6]))
# [[4 0 0]
#  [0 5 0]
#  [0 0 6]]
```

When given a 2-D array, `np.diag` extracts its main diagonal:

```python
m = np.array([[1, 2], [3, 4]])
print(np.diag(m))  # [1 4]
```

## 9. Random arrays

Use NumPy's modern random generator:

```python
rng = np.random.default_rng(seed=42)

print(rng.integers(1, 7, size=5))
print(rng.random((2, 3)))
print(rng.normal(loc=0, scale=1, size=4))
```

- `default_rng(seed)`: creates a random-number generator. A fixed seed makes results reproducible.
- `integers(low, high, size)`: random integers from low (included) to high (excluded).
- `random(size)`: uniform random values from 0 up to but not including 1.
- `normal(loc, scale, size)`: values from a normal distribution with mean `loc` and standard deviation `scale`.

Avoid relying on random output copied from another run unless the same generator, seed and calls are used.

## 10. Triangular matrices

`np.tril(a)` keeps the lower triangle (including the main diagonal); values above it become zero.

`np.triu(a)` keeps the upper triangle (including the main diagonal); values below it become zero.

```python
m = np.array([[1, 2, 3],
              [4, 5, 6],
              [7, 8, 9]])

print(np.tril(m))
# [[1 0 0]
#  [4 5 0]
#  [7 8 9]]

print(np.triu(m))
# [[1 2 3]
#  [0 5 6]
#  [0 0 9]]
```

## 11. Quick function chooser

| Need | Function |
|---|---|
| Convert existing data | `np.array` |
| Known step | `np.arange` |
| Known sample count | `np.linspace` |
| All zeros / all ones | `np.zeros` / `np.ones` |
| All one chosen value | `np.full` |
| Allocate uninitialized memory | `np.empty` |
| Identity matrix | `np.eye` |
| Diagonal values or extraction | `np.diag` |
| Random integers / decimals | `rng.integers` / `rng.random` |

## 12. Common mistakes

- Treating the third argument of `arange` as the number of values. It is the step.
- Treating the third argument of `linspace` as the step. It is the number of samples.
- Expecting `empty` to contain zeros.
- Forgetting that the upper boundary of `arange` and `rng.integers` is excluded.
- Using random values without a seed when you need repeatable experiments.

## 13. Practice

1. Create even numbers from 2 to 20 using `arange`.
2. Create exactly 6 values from -1 to 1 using `linspace`.
3. Create a 3-by-4 array filled with 9.
4. Create a 4-by-4 identity matrix.
5. Generate 10 reproducible integers from 1 through 100 using `default_rng`.

**Checkpoint:** You should be able to explain the difference between a step size and a sample count before moving on.
