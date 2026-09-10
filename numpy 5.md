# NumPy – Lecture 5 Notes

## 1. `np.arange()`

Used when we want numbers with a **fixed step/gap**.

```python
np.arange(start, stop, step)
```

- `start` → where to begin
- `stop` → where to stop (**not included**)
- `step` → gap between values

### Examples

```python
np.arange(5, 17, 4)
# [ 5  9 13]

np.arange(5, 17, 2)
# [ 5  7  9 11 13 15]

np.arange(0, 10, 2.5)
# [0.  2.5 5.  7.5]

np.arange(50, 0, -5)
# [50 45 40 35 30 25 20 15 10  5]
```

You can also specify the data type:

```python
np.arange(5, 10, dtype=np.float32)
```

**Remember:** `arange` = fixed step.

---

## 2. `np.linspace()`

Used when we want a **fixed number of evenly spaced values** between two numbers.

```python
np.linspace(start, stop, num)
```

Example:

```python
np.linspace(1, 5, 5)
# [1. 2. 3. 4. 5.]
```

Here `num=5` means we want **5 values**.

### Important parameters

```python
np.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)
```

- `endpoint=True` → includes `stop`
- `endpoint=False` → does not include `stop`
- `retstep=True` → also gives the gap between values
- `dtype` → choose the data type

Example:

```python
np.linspace(0, 10, 5, retstep=True)
```

Output:

```text
(array([ 0. ,  2.5,  5. ,  7.5, 10. ]), 2.5)
```

### `linspace` vs `arange`

| `arange` | `linspace` |
|---|---|
| Decide the **step** | Decide the **number of values** |
| `np.arange(0,10,2)` | `np.linspace(0,10,6)` |

**ML use:** useful for testing different values, such as trying different **K values in K-Means**.

---

## 3. `np.logspace()`

Similar to `linspace`, but it equally increases the **exponents**.

By default, the base is `10`.

```python
np.logspace(start, stop, num)
```

Example:

```python
np.logspace(0, 4, 5)
```

Output:

```text
[1.e+00 1.e+01 1.e+02 1.e+03 1.e+04]
```

This means:

```text
10^0 = 1
10^1 = 10
10^2 = 100
10^3 = 1000
10^4 = 10000
```

### Different base

```python
np.logspace(0, 10, 6, base=2)
```

This gives values based on:

```text
2^0, 2^2, 2^4, 2^6, 2^8, 2^10
```

### `linspace` vs `logspace`

```text
linspace → equal difference
logspace → equal ratio / exponential growth
```

**ML use:** useful when testing values across a very large range, such as **learning rates and other hyperparameters**.

---

# 4. `np.zeros()`

Creates an array filled with `0`.

### 1D array

```python
np.zeros(5)
```

Output:

```text
[0. 0. 0. 0. 0.]
```

### Matrix

```python
np.zeros((3, 3))
```

Output:

```text
[[0. 0. 0.]
 [0. 0. 0.]
 [0. 0. 0.]]
```

For a rectangular matrix:

```python
np.zeros((2, 4))
```

means:

```text
2 rows × 4 columns
```

---

# 5. `np.ones()`

Same idea as `zeros()`, but fills everything with `1`.

```python
np.ones(5)
```

Output:

```text
[1. 1. 1. 1. 1.]
```

Matrix:

```python
np.ones((3, 3))
```

### Choosing dtype

```python
np.ones((3, 3), dtype=np.int32)
```

Now the values are integers instead of floats.

---

# 6. Creating a Matrix with a Specific Value

NumPy has `zeros()` and `ones()`, but not a direct `np.fives()`-type function.

Easy way:

```python
np.ones((3, 3)) * 5
```

Output:

```text
[[5. 5. 5.]
 [5. 5. 5.]
 [5. 5. 5.]]
```

For another value:

```python
np.ones((2, 4)) * 7
```

---

# 7. `np.empty()`

Creates an array by allocating memory, but **does not initialize the values**.

```python
np.empty((3, 3))
```

The values may look random or strange.

**Important:** Do not use `empty()` when you need the array to start with zeros.

```text
zeros() → memory + fill with 0
ones()  → memory + fill with 1
empty() → memory only; values are not initialized
```

---

# 8. Diagonal Matrix

A diagonal matrix has values on the **main diagonal**, and the other positions are `0`.

Example:

```text
[[5 0 0]
 [0 8 0]
 [0 0 2]]
```

Main diagonal:

```text
5 8 2
```

---

# 9. `np.diag()`

### Get the diagonal

```python
A = np.array([
    [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
])

np.diag(A)
```

Output:

```text
[1 5 9]
```

### Create a diagonal matrix

```python
np.diag([1, 5, 9])
```

Output:

```text
[[1 0 0]
 [0 5 0]
 [0 0 9]]
```

---

# 10. Lower Triangular Matrix – `np.tril()`

Keeps the values **on and below the main diagonal**.

```python
A = np.arange(1, 10).reshape(3, 3)

np.tril(A)
```

Output:

```text
[[1 0 0]
 [4 5 0]
 [7 8 9]]
```

---

# 11. Upper Triangular Matrix – `np.triu()`

Keeps the values **on and above the main diagonal**.

```python
np.triu(A)
```

Output:

```text
[[1 2 3]
 [0 5 6]
 [0 0 9]]
```

---

# 12. `k` in `diag()`, `tril()`, and `triu()`

`k` tells NumPy which diagonal to use.

```text
k = 0  → main diagonal
k > 0  → diagonal above main diagonal
k < 0  → diagonal below main diagonal
```

Examples:

```python
np.triu(A, k=1)
```

Starts from the diagonal **above** the main diagonal.

```python
np.tril(A, k=-1)
```

Starts from the diagonal **below** the main diagonal.

Quick memory:

```text
k = 0  → main
k = 1  → above
k = -1 → below
```

---

# 13. Number of Diagonals

For an `m × n` matrix:

```text
Total diagonals = m + n - 1
```

Examples:

```text
3 × 3 → 3 + 3 - 1 = 5 diagonals
2 × 4 → 2 + 4 - 1 = 5 diagonals
```

---

# 14. `reshape()`

Changes the **shape** of an array without changing the number of elements.

Example:

```python
a = np.arange(9)

a.reshape(3, 3)
```

Output:

```text
[[0 1 2]
 [3 4 5]
 [6 7 8]]
```

### Important rule

The number of elements must stay the same.

```text
9 elements → 3 × 3 = 9 ✅
9 elements → 2 × 4 = 8 ❌
```

---

# 15. `np.eye()`

Creates an **identity matrix**.

```python
np.eye(4)
```

Output:

```text
[[1. 0. 0. 0.]
 [0. 1. 0. 0.]
 [0. 0. 1. 0.]
 [0. 0. 0. 1.]]
```

Main diagonal → `1`

Everything else → `0`

For a compatible matrix `A`:

```text
A × I = A
```

Think of identity matrix as the **1 of matrix multiplication**.

---

# 16. `np.random.rand()`

Generates random floating-point values between `0` and `1`.

```python
np.random.rand(5)
```

Example:

```text
[0.42 0.13 0.87 0.31 0.65]
```

The exact values change each time.

For a matrix:

```python
np.random.rand(3, 3)
```

---

# 17. `np.random.randn()`

Generates random values following a **standard normal distribution**.

```python
np.random.randn(5)
```

The values are centered around:

```text
mean = 0
standard deviation = 1
```

They can be positive or negative.

---

# 18. `np.random.randint()`

Generates random integers.

```python
np.random.randint(low, high, size)
```

Important:

```text
low  → included
high → excluded
```

Example:

```python
np.random.randint(1, 7, 10)
```

Generates 10 random integers from:

```text
1, 2, 3, 4, 5, 6
```

### Matrix

```python
np.random.randint(1, 100, (4, 4))
```

Creates a `4 × 4` matrix of random integers from `1` to `99`.

---

# 19. Dice Simulation 🎲

A dice has values:

```text
1 2 3 4 5 6
```

So:

```python
np.random.randint(1, 7, 20)
```

simulates **20 dice rolls**.

Remember:

```text
1 → included
7 → excluded
```

So possible values are only `1` to `6`.

---

# 20. Random Numbers in ML

Random numbers are commonly used for:

- Initializing model weights
- Simulations
- Generating sample data
- Testing algorithms

---

# 🔥 Quick Revision

| Function | Easy way to remember |
|---|---|
| `np.arange()` | Fixed **step** |
| `np.linspace()` | Fixed **number of values** |
| `np.logspace()` | Exponential/log scale |
| `np.zeros()` | Fill with `0` |
| `np.ones()` | Fill with `1` |
| `np.empty()` | Memory allocated, values not initialized |
| `np.diag()` | Get/create diagonal |
| `np.tril()` | Lower triangle |
| `np.triu()` | Upper triangle |
| `reshape()` | Change shape, same elements |
| `np.eye()` | Identity matrix |
| `np.random.rand()` | Random floats `0–1` |
| `np.random.randn()` | Standard normal random values |
| `np.random.randint()` | Random integers |

## 🧠 Most Important Things to Remember

```text
arange   → step
linspace → number of values
logspace → powers/exponential scale

zeros → 0
ones  → 1
empty → uninitialized

diag → diagonal
tril → lower triangle
triu → upper triangle
eye  → identity matrix

rand    → random floats 0–1
randn   → normal distribution
randint → random integers
```
