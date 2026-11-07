# 13 — NumPy in a Machine Learning Workflow

> **Goal:** Connect the NumPy concepts to a small end-to-end ML-style workflow: represent features, inspect shapes, clean data, normalize values and calculate predictions.

## 1. Represent a dataset

A typical tabular ML dataset has:
- rows = observations or samples,
- columns = features,
- target = the value or class we want to predict.

```python
import numpy as np

# Columns: study hours, attendance percentage
X = np.array([
    [2.0, 70.0],
    [4.0, 80.0],
    [6.0, 90.0],
    [1.0, 60.0]
])

# Target: sample exam score
y = np.array([45.0, 65.0, 85.0, 35.0])

print(X.shape)  # (4, 2)
print(y.shape)  # (4,)
```

There are four samples and two features. There is one target value per sample.

## 2. Inspect before calculating

```python
print(X.ndim)
print(X.dtype)
print(X.min(axis=0))
print(X.max(axis=0))
```

Checking shape, dtype and value ranges helps detect mistakes before model training.

## 3. Handle missing values

```python
data = np.array([10.0, 20.0, np.nan, 40.0])
missing_mask = np.isnan(data)
print(missing_mask)
# [False False  True False]

mean_value = np.nanmean(data)
data[missing_mask] = mean_value
print(data)
# [10.         20.         23.33333333 40.        ]
```

This illustrates mean imputation for one numerical column. In a real workflow, calculate imputation values using training data only, then apply the same values to validation/test data to avoid data leakage.

## 4. Split features and labels consistently

If you shuffle the feature rows, shuffle the target using the exact same indexes:

```python
rng = np.random.default_rng(42)
indices = rng.permutation(len(X))

X_shuffled = X[indices]
y_shuffled = y[indices]

split = int(0.75 * len(X))
X_train, X_test = X_shuffled[:split], X_shuffled[split:]
y_train, y_test = y_shuffled[:split], y_shuffled[split:]
```

If you shuffle X and y independently, the feature rows may no longer match their correct labels.

## 5. Feature scaling: standardization

Features can use different units and ranges. For example, study hours may range from 0 to 10 while attendance ranges from 0 to 100. Standardization transforms each feature:

[
z=\frac{x-\mu}{\sigma}
]

where (mu) is the feature mean and (sigma) is its standard deviation.

```python
mean = X_train.mean(axis=0)
std = X_train.std(axis=0)

# Avoid division by zero for a constant feature
std[std == 0] = 1

X_train_scaled = (X_train - mean) / std
X_test_scaled = (X_test - mean) / std
```

Important: use training-set mean and standard deviation to transform both training and test data. Do not calculate test statistics separately.

## 6. Calculate a simple linear prediction

```python
weights = np.array([5.0, 0.4])
bias = 2.0

predictions = X @ weights + bias
print(predictions)
```

The model calculates a weighted sum of features plus a bias. This is the core shape of many linear models.

## 7. Calculate an error metric

Mean absolute error (MAE) is the average absolute difference between true values and predictions:

[
MAE=\frac{1}{n}\sum_{i=1}^{n}|y_i-\hat y_i|
]

```python
actual = np.array([45.0, 65.0, 85.0, 35.0])
predicted = np.array([44.0, 68.0, 80.0, 40.0])

mae = np.mean(np.abs(actual - predicted))
print(mae)  # 3.75
```

This tells us the average absolute prediction error is 3.75 score points for this example.

## 8. NumPy and other ML libraries

NumPy is a foundation for the Python data-science ecosystem:
- pandas uses NumPy-backed numerical structures in many operations.
- scikit-learn accepts NumPy arrays for features and targets.
- many scientific and deep-learning tools use array/tensor concepts.

You do not need to implement every ML algorithm with NumPy. Learning NumPy helps you understand the data shapes and numerical operations that happen underneath.

## 9. Data leakage warning

**Data leakage** occurs when information that should not be available during training influences the model. Examples:
- calculating normalization statistics using the entire dataset before splitting,
- imputing missing values using test-set information,
- allowing future information into features for a prediction task.

Keep preprocessing steps fitted on training data and apply the learned transformation to held-out data.

## 10. Final NumPy checklist

You should be comfortable with:
- creating arrays and choosing dtypes,
- reading `shape`, `ndim` and `size`,
- indexing, slicing and Boolean filtering,
- reshaping and transposing,
- broadcasting and vectorization,
- summary statistics,
- random sampling and reproducibility,
- dot products and matrix multiplication,
- using arrays for ML features, targets and predictions.

## 11. Mini project: student score analysis

Create an array with at least 10 students and two features (study hours and attendance). Then:
1. Print the shape and dtype.
2. Find the mean of each feature.
3. Select students with attendance above 75.
4. Standardize the two features.
5. Create a simple weight vector and calculate a score estimate.
6. Calculate MAE against a target array you define.
7. Explain what each output means.

**Checkpoint:** NumPy is not just a collection of functions. It is the numerical foundation for representing, transforming and calculating with data in many ML workflows.
