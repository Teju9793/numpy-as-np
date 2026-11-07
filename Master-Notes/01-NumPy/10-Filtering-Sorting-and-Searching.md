# 10 — Filtering, Sorting and Searching

> **Goal:** Select values by conditions, sort data, find positions and count occurrences.

## 1. Filter using a condition

```python
import numpy as np
values = np.array([12, 45, 7, 90, 32])
print(values[values > 30])
# [45 90 32]
```

A comparison creates a Boolean mask. Indexing with the mask returns only values where the condition is True.

## 2. Find positions with where

`np.where(condition)` returns the indexes where a condition is True:

```python
x = np.array([10, 25, 40, 15, 60])
print(np.where(x > 20))
# (array([1, 2, 4]),)
```

For a 1-D array, the result is a tuple containing the index array. For 2-D arrays, it returns one index array per axis.

The three-argument form chooses values:

```python
print(np.where(x > 20, "High", "Low"))
# ['Low' 'High' 'High' 'Low' 'High']
```

## 3. Sort values

```python
x = np.array([40, 10, 30, 20])
print(np.sort(x))
# [10 20 30 40]
print(x)
# [40 10 30 20]
```

`np.sort` returns a sorted copy; it does not change the original array.

To sort the original array in place:

```python
x.sort()
print(x)  # [10 20 30 40]
```

Descending order for numeric values:

```python
x = np.array([40, 10, 30, 20])
print(np.sort(x)[::-1])
# [40 30 20 10]
```

## 4. Sort along an axis

```python
m = np.array([[3, 1, 2],
              [9, 7, 8]])
print(np.sort(m, axis=1))
# [[1 2 3]
#  [7 8 9]]
```

- axis 1 sorts each row.
- axis 0 sorts each column.
- axis=None sorts the flattened values.

## 5. argsort — get the sorting order

Sometimes you need the positions that would sort the data, not just the sorted values.

```python
scores = np.array([70, 90, 60, 80])
order = np.argsort(scores)
print(order)          # [2 0 3 1]
print(scores[order])  # [60 70 80 90]
```

The smallest value is at index 2, next at index 0, then 3, then 1. This is useful when you need to reorder another array using the same ranking.

## 6. Find minimum and maximum indexes

```python
x = np.array([12, 50, 7, 90, 32])
print(np.argmax(x))  # 3
print(np.argmin(x))  # 2
```

These return the index of the maximum or minimum value. For multidimensional arrays, specify an axis if you want an index per row or column.

## 7. Unique values and counts

```python
x = np.array([2, 3, 2, 5, 3, 2])
print(np.unique(x))
# [2 3 5]
print(np.unique(x, return_counts=True))
# (array([2, 3, 5]), array([3, 2, 1]))
```

The second result tells us 2 occurs three times, 3 occurs twice and 5 occurs once.

## 8. Search in sorted arrays with searchsorted

`np.searchsorted` finds where a value should be inserted to keep a sorted array in order.

```python
x = np.array([10, 20, 30, 40])
print(np.searchsorted(x, 25))  # 2
```

Index 2 is before 30. By default, it uses the left insertion position. The input array should be sorted for the result to have the intended meaning.

## 9. Common mistakes

- Confusing values from `where` with their indexes.
- Expecting `np.sort` to modify the original.
- Forgetting that `argsort` returns positions.
- Using `searchsorted` on an unsorted array.
- Forgetting that `argmax` returns an index, not the maximum value itself.

## 10. Practice

1. Filter values greater than 50.
2. Find the indexes where values are even.
3. Sort an array without changing the original.
4. Use `argsort` to rank student scores.
5. Find unique values and their counts.
6. Find the index of the highest score.

**Checkpoint:** Know the difference between a value, its index and the order of indexes that would sort the array.
