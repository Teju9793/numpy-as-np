# 08 — Vectorization and Performance

> **Goal:** Replace unnecessary Python loops with array operations, understand why vectorization helps, and measure performance fairly.

## 1. What is vectorization?

**Vectorization** means expressing an operation on an entire array rather than manually processing one element at a time in Python.

Loop version:

```python
values = [10, 20, 30, 40]
result = []
for value in values:
    result.append(value * 2)
print(result)
# [20, 40, 60, 80]
```

NumPy version:

```python
import numpy as np
values = np.array([10, 20, 30, 40])
result = values * 2
print(result)
# [20 40 60 80]
```

The NumPy expression is concise and the numerical loop is handled by optimized low-level code.

## 2. Why can vectorization be faster?

A Python loop repeatedly executes interpreter-level operations for each element. A NumPy operation can process a block of typed numerical data in compiled code and may use optimized CPU instructions.

The speed advantage depends on array size, operation, memory access, dtype and hardware. For tiny arrays, setup overhead can make the difference small or even favor a simple loop.

## 3. A real example: calculate total prices

```python
prices = np.array([100, 250, 400])
quantity = np.array([2, 1, 3])

total = prices * quantity
print(total)       # [ 200  250 1200]
print(total.sum()) # 1650
```

Each price is multiplied by the matching quantity. Then `sum()` adds all line totals.

## 4. Conditional vectorized operations with where

`np.where(condition, value_if_true, value_if_false)` selects values based on a condition.

```python
marks = np.array([35, 72, 28, 90])
status = np.where(marks >= 40, "Pass", "Fail")
print(status)
# ['Fail' 'Pass' 'Fail' 'Pass']
```

It is useful when you want to create a new result array rather than modify the original.

## 5. Avoid unnecessary loops, but keep code readable

Vectorized:
```python
temperatures = np.array([20, 25, 30])
fahrenheit = temperatures * 9 / 5 + 32
```

A loop is still appropriate when the task is inherently sequential, involves complex Python objects, or is clearer as a loop. The goal is not “never use loops”; it is to avoid slow element-by-element Python loops for straightforward numerical array work.

## 6. Measure with timeit

Do not claim that one method is faster based on a single run. Use repeated measurements:

```python
import timeit
import numpy as np

values = np.arange(1_000_000)

loop_time = timeit.timeit(
    "sum(int(x) * 2 for x in values)",
    globals={"values": values},
    number=3
)

numpy_time = timeit.timeit(
    "values * 2",
    globals={"values": values},
    number=3
)

print("Loop:", loop_time)
print("NumPy:", numpy_time)
```

This is a basic demonstration. For rigorous benchmarking, repeat tests, compare equivalent work, account for warm-up and avoid other heavy processes on the machine.

## 7. Memory is part of performance

Vectorized operations may create temporary arrays. For example, a long expression with several intermediate results can use substantial memory. For very large data, consider:
- processing in chunks,
- reusing output arrays with supported `out=` parameters,
- choosing an appropriate dtype,
- avoiding unnecessary copies.

Do not optimize prematurely. First write correct, readable code; then measure the real bottleneck.

## 8. Common mistakes

- Assuming vectorization is always faster for every array size.
- Comparing different amounts of work in a benchmark.
- Creating many large temporary arrays without noticing memory use.
- Replacing a clear loop with a complicated expression that is harder to maintain.

## 9. Practice

1. Multiply every value in an array by 3.
2. Convert Celsius values to Fahrenheit in one expression.
3. Use `np.where` to label values above 50 as High and the rest as Low.
4. Compare a Python loop and NumPy operation on 10,000 and 1,000,000 values.

**Checkpoint:** Explain vectorization in your own words and know when measurement is more useful than guessing.
