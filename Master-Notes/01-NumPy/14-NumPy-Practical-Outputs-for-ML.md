# 14 — NumPy Practical Examples with Outputs

> 🔵 **ML PRACTICE LAB** · Small examples for data preparation and numerical ML foundations.

## 1. Create a feature matrix

~~~python
import numpy as np

# Rows = students; columns = study hours, attendance
X = np.array([[2, 70], [4, 80], [6, 90], [3, 75]])
y = np.array([45, 65, 85, 55])

print(X)
print("X shape:", X.shape)
print("y shape:", y.shape)
~~~

**Output**

~~~text
[[ 2 70]
 [ 4 80]
 [ 6 90]
 [ 3 75]]
X shape: (4, 2)
y shape: (4,)
~~~

There are 4 samples, 2 input features and 4 target values. In ML, X usually stores features and y stores the target.

## 2. Select columns and filter rows

~~~python
print("Study hours:", X[:, 0])
print("Attendance >= 80:")
print(X[X[:, 1] >= 80])
~~~

**Output**

~~~text
Study hours: [2 4 6 3]
Attendance >= 80:
[[ 4 80]
 [ 6 90]]
~~~

X[:, 0] means every row from the first column. Boolean filtering keeps rows where the condition is True.

## 3. Understand axis

~~~python
print(X.mean(axis=0))
print(X.mean(axis=1))
~~~

**Output**

~~~text
[ 3.75 78.75]
[36. 42. 48. 39.]
~~~

- axis=0: calculate down rows, giving one result per column.
- axis=1: calculate across columns, giving one result per row.

## 4. Min-max scaling

The formula maps values to a 0–1 range:

\[
x' = \frac{x-x_{min}}{x_{max}-x_{min}}
\]

~~~python
minimum = X.min(axis=0)
maximum = X.max(axis=0)
X_scaled = (X - minimum) / (maximum - minimum)
print(np.round(X_scaled, 2))
~~~

**Output**

~~~text
[[0.   0.  ]
 [0.5  0.67]
 [1.   1.  ]
 [0.25 0.33]]
~~~

Scaling can help distance-based and gradient-based algorithms. **ML warning:** calculate min and max using training data only, then reuse them for test data.

## 5. Broadcasting

~~~python
prices = np.array([100, 200, 300])
print(prices - 10)
~~~

**Output**

~~~text
[ 90 190 290]
~~~

NumPy applies the scalar value to every element automatically.

## 6. Matrix multiplication for predictions

~~~python
features = np.array([[2, 70], [4, 80], [6, 90]])
weights = np.array([5, 0.4])
bias = 2

predictions = features @ weights + bias
print(predictions)
~~~

**Output**

~~~text
[40. 54. 68.]
~~~

For the first row: 2 × 5 + 70 × 0.4 + 2 = 40. The @ operator performs matrix multiplication.

## 7. Find missing numeric values

~~~python
scores = np.array([45.0, 60.0, np.nan, 80.0])
print(np.isnan(scores))
print(np.nanmean(scores))
~~~

**Output**

~~~text
[False False  True False]
61.666666666666664
~~~

np.isnan identifies NaN values; np.nanmean calculates the mean while ignoring them.

## 8. Calculate MAE

~~~python
actual = np.array([50, 60, 70])
predicted = np.array([48, 65, 68])

mae = np.mean(np.abs(actual - predicted))
print(mae)
~~~

**Output**

~~~text
2.3333333333333335
~~~

MAE is the average absolute prediction error. Lower is better when comparing models on the same target and dataset.

## Quick revision

| Expression | Meaning |
|---|---|
| X.shape | Number of rows and columns |
| X[:, 0] | All rows from first column |
| X.mean(axis=0) | Mean of each column |
| X[X[:, 1] > 80] | Boolean filtering |
| X @ weights | Matrix multiplication |
| np.isnan(X) | Find NaN values |
| np.nanmean(X) | Mean ignoring NaN |

**Practice:** Create a 5-row feature array. Print its shape, filter attendance above 75, calculate column means, scale the features and multiply by a weight vector.

**ML connection:** These are core building blocks for feature preparation, numerical calculations and understanding model inputs.
