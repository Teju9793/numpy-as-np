# 09 — Statistical Operations in NumPy

> **Goal:** Calculate common summary statistics, understand axis-based statistics and avoid misleading results caused by missing values.

## 1. Why statistics?

A dataset may contain thousands of numbers. Summary statistics help describe its center, spread and range.

```python
import numpy as np
marks = np.array([60, 70, 80, 90, 100])
```

## 2. Sum, minimum, maximum and mean

```python
print(np.sum(marks))   # 400
print(np.min(marks))   # 60
print(np.max(marks))   # 100
print(np.mean(marks))  # 80.0
```

Mean is calculated as:

[
\text{Mean}=\frac{\text{sum of all values}}{\text{number of values}}
]

Here: ((60+70+80+90+100)/5=80).

The array methods also work: `marks.sum()`, `marks.mean()`, `marks.min()` and `marks.max()`.

## 3. Median

The **median** is the middle value after sorting. If there is an even number of values, it is the average of the two middle values.

```python
x = np.array([10, 90, 20, 30, 100])
print(np.median(x))  # 30.0
```

Sorted values: 10, 20, 30, 90, 100. The middle is 30.

Median is less affected by an extreme outlier than the mean.

## 4. Percentiles and quartiles

A percentile describes a position in a distribution. The 50th percentile is the median.

```python
scores = np.array([10, 20, 30, 40, 50, 60, 70])
print(np.percentile(scores, 25))  # 25.0
print(np.percentile(scores, 50))  # 40.0
print(np.percentile(scores, 75))  # 55.0
```

The exact percentile calculation uses an interpolation method. For small samples, different statistical conventions can produce different values. NumPy's default method is linear.

## 5. Variance and standard deviation

Variance measures average squared distance from the mean. Standard deviation is the square root of variance and is expressed in the original unit.

[
\text{Population variance}=\frac{\sum (x_i-\mu)^2}{N}
]

[
\text{Standard deviation}=\sqrt{\text{variance}}
]

```python
x = np.array([2, 4, 6, 8])
print(np.var(x))  # 5.0
print(np.std(x))  # about 2.236
```

NumPy's default `ddof=0` calculates population variance. For the common sample variance estimator, use `ddof=1`:

```python
print(np.var(x, ddof=1))
```

Choose population or sample statistics based on what your data represents; do not change `ddof` randomly.

## 6. Statistics along an axis

```python
scores = np.array([[70, 80, 90],
                   [60, 75, 85]])

print(scores.mean(axis=0))
# [65.  77.5 87.5]  mean per column
print(scores.mean(axis=1))
# [80.         73.33333333]  mean per row
```

If rows represent students and columns represent subjects:
- axis 0 gives the mean score for each subject.
- axis 1 gives the mean score for each student.

## 7. Missing values: mean versus nanmean

```python
x = np.array([10.0, 20.0, np.nan, 40.0])
print(np.mean(x))     # nan
print(np.nanmean(x))  # 23.333333333333332
```

Functions with the `nan` prefix generally ignore NaN values for the calculation. They do not fix or remove the missing data from the original array.

## 8. Cumulative statistics

```python
x = np.array([2, 4, 6, 8])
print(np.cumsum(x))  # [ 2  6 12 20]
print(np.cumprod(x)) # [  2   8  48 384]
```

Cumulative sum keeps a running total: 2, then 2+4, then 2+4+6, and finally 2+4+6+8.

## 9. Correlation

Correlation describes how two variables move together. `np.corrcoef` returns a correlation matrix:

```python
hours = np.array([1, 2, 3, 4, 5])
scores = np.array([40, 50, 60, 70, 80])
print(np.corrcoef(hours, scores))
```

The off-diagonal entries show the correlation between the two variables. Correlation ranges from -1 to +1:
- +1: perfect positive linear relationship.
- 0: no linear correlation.
- -1: perfect negative linear relationship.

**Correlation does not prove causation.** A third factor may influence both variables.

## 10. Common mistakes

- Confusing mean and median.
- Forgetting that variance squares the units.
- Using `ddof=1` without understanding sample versus population.
- Allowing NaN to make an ordinary mean return NaN.
- Misreading axis 0 and axis 1.
- Assuming correlation proves one variable causes another.

## 11. Practice

For `[2, 4, 4, 6, 9]`, calculate mean, median, minimum, maximum, variance and standard deviation. Then compare the mean and median after adding 1000 as an extra value.

**Checkpoint:** Be able to explain what each statistic tells you, not just remember its function name.
