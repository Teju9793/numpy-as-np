# 11 — Random Numbers and Sampling

> **Goal:** Generate repeatable random data, understand common distributions and select samples from a dataset.

## 1. Why random numbers in data science?

Randomness is used to:
- split data into training and testing sets,
- initialize model parameters,
- sample a subset of a large dataset,
- simulate uncertain events,
- run experiments.

NumPy provides a random-number generator (RNG). Prefer the modern `default_rng` interface.

## 2. Create a generator

```python
import numpy as np
rng = np.random.default_rng(seed=42)
```

A **seed** initializes the generator. The same seed and same sequence of calls produce repeatable results in the same compatible NumPy setup. Reproducibility is useful when debugging or comparing experiments.

If you omit the seed, the generated sequence will normally differ between runs.

## 3. Random integers

```python
rng = np.random.default_rng(42)
dice = rng.integers(1, 7, size=5)
print(dice)
```

The low value 1 is included and high value 7 is excluded, so possible results are 1 through 6.

- `low`: lower boundary, included.
- `high`: upper boundary, excluded.
- `size`: output shape.

For values from 0 through 9, use `rng.integers(0, 10, size=8)`.

## 4. Uniform random decimals

```python
rng = np.random.default_rng(42)
x = rng.random((2, 3))
print(x)
```

Values are sampled from a uniform distribution on the interval [0, 1). Each interval of equal width has equal probability.

## 5. Normal distribution

```python
rng = np.random.default_rng(42)
heights = rng.normal(loc=170, scale=8, size=1000)
```

- `loc`: mean (center).
- `scale`: standard deviation (spread).
- `size`: output shape.

A normal distribution is bell-shaped and symmetric. Many natural measurements are approximately normal, although real datasets must be checked rather than assumed to follow it.

## 6. Choose samples from an existing array

```python
rng = np.random.default_rng(42)
students = np.array(["Asha", "Ravi", "Maya", "John", "Sara"])
sample = rng.choice(students, size=3, replace=False)
print(sample)
```

- `size`: number of selections.
- `replace=True`: an item may be selected more than once.
- `replace=False`: selections are without replacement.

Without replacement, the requested sample size cannot exceed the population size.

## 7. Shuffle and permutation

```python
rng = np.random.default_rng(42)
x = np.array([1, 2, 3, 4, 5])

shuffled = rng.permutation(x)
print(shuffled)
print(x)  # original remains unchanged

rng.shuffle(x)
print(x)  # x is modified in place
```

- `permutation`: returns a shuffled copy (for an array input).
- `shuffle`: shuffles the array in place.

This distinction matters if you need to preserve the original ordering.

## 8. Probability-weighted choice

```python
rng = np.random.default_rng(42)
result = rng.choice(
    ["A", "B", "C"],
    size=10,
    p=[0.6, 0.3, 0.1]
)
```

The probabilities must be non-negative and sum to 1 (within numerical tolerance). Category A is more likely than B or C, but one small sample may not reflect the exact percentages.

## 9. Train-test split idea

A basic random permutation can help create shuffled indexes:

```python
rng = np.random.default_rng(42)
X = np.arange(20).reshape(10, 2)
indices = rng.permutation(len(X))

split = int(0.8 * len(X))
train_idx = indices[:split]
test_idx = indices[split:]

X_train = X[train_idx]
X_test = X[test_idx]
```

This creates an 80/20 split for illustration. In real ML work, split features and labels with the same indexes, consider stratification for imbalanced classes, and avoid data leakage.

## 10. Common mistakes

- Forgetting that the high boundary in `integers` is excluded.
- Using a new generator without a fixed seed when trying to reproduce a result.
- Expecting `shuffle` to return a shuffled copy; it modifies in place.
- Sampling without replacement more items than exist.
- Assuming a small random sample will match the population percentages exactly.

## 11. Practice

1. Generate 10 integers from 1 to 6 with a fixed seed.
2. Generate a 3-by-4 array of uniform random values.
3. Generate 1,000 normal values with mean 50 and standard deviation 10.
4. Select 5 unique values from an array of 20.
5. Shuffle indexes and split them into 80% and 20%.

**Checkpoint:** Explain why a seed helps reproducibility and the difference between sampling with and without replacement.
