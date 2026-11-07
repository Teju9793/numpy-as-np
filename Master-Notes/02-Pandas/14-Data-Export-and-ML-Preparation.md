# 14 — Exporting Data and Preparing for Machine Learning

> **Goal:** Save cleaned datasets, separate features and targets, and produce arrays with shapes expected by ML libraries.

## 1. Why export matters

After cleaning and transforming data, you may need to save it for another analysis, share it with a teammate or pass it to a model-training workflow.

Keep a copy of the original raw data. Exporting a cleaned file should not destroy the source.

## 2. Export to CSV

```python
import pandas as pd

df = pd.DataFrame({
    "Name": ["Asha", "Ravi"],
    "Marks": [85, 72]
})

df.to_csv("clean_students.csv", index=False)
```

The `index=False` option prevents Pandas from writing the row index as an extra column. If the index contains meaningful identifiers, decide whether to export it.

## 3. Export to Excel

```python
df.to_excel("clean_students.xlsx", index=False, sheet_name="Students")
```

Writing Excel files may require an engine package such as openpyxl. For multiple sheets, use an `ExcelWriter` context manager.

## 4. Read the exported file back

```python
check = pd.read_csv("clean_students.csv")
print(check.head())
print(check.dtypes)
```

Verify that the exported file contains the intended columns, values and data types. CSV does not preserve all Pandas dtype metadata, so some types may need to be parsed again when reading.

## 5. Separate features and target

```python
X = df[["StudyHours", "Attendance", "AssignmentScore"]]
y = df["FinalMarks"]
```

- `X`: feature matrix / input columns.
- `y`: target Series / output to predict.

Be careful not to include the target column inside X.

## 6. Convert to NumPy arrays when needed

```python
X_array = X.to_numpy()
y_array = y.to_numpy()

print(X_array.shape)
print(y_array.shape)
```

If there are 100 rows and 3 feature columns, X should have shape `(100, 3)`; y should have 100 target values.

## 7. Check missing values and data types

```python
print(X.isna().sum())
print(y.isna().sum())
print(X.dtypes)
```

Most ML estimators expect numerical input and may reject missing values. Categorical columns may need encoding. Choose preprocessing based on the algorithm and the meaning of the data.

## 8. Train-test split

Use a library such as scikit-learn to split features and targets together:

```python
from sklearn.model_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(
    X, y,
    test_size=0.2,
    random_state=42
)
```

- `test_size=0.2`: reserve 20% for testing.
- `random_state=42`: make the split reproducible.
- `stratify=y`: often useful for classification to preserve class proportions, when appropriate.

For time-series problems, a random split may be inappropriate; use a time-aware split.

## 9. Build preprocessing without leakage

For real ML projects, use a scikit-learn Pipeline and ColumnTransformer to fit imputation, scaling and encoding on training data only. The same fitted transformations are then applied to test or future data.

This reduces the chance of inconsistent preprocessing and data leakage.

## 10. Final dataset validation checklist

Before training:
1. Are column names correct and consistent?
2. Are there duplicate or invalid rows?
3. Are missing values handled?
4. Are numeric and categorical dtypes appropriate?
5. Is the target separated from the features?
6. Are feature and target row counts equal?
7. Are all features available at prediction time?
8. Is the train/test split appropriate for the problem?
9. Are preprocessing steps fitted on training data only?
10. Can the saved dataset be read back correctly?

## 11. Common mistakes

- Exporting the index accidentally.
- Forgetting to separate target from features.
- Saving CSV and assuming all dtypes will be preserved.
- Splitting X and y independently.
- Applying preprocessing before the split and leaking information.
- Randomly splitting time-series observations.

## 12. Mini project: clean-to-ML workflow

Take a small CSV dataset and:
1. Load it with Pandas.
2. Inspect shape, dtypes, missing values and duplicates.
3. Clean inconsistent text.
4. Convert date and numeric columns.
5. Create two useful features.
6. Separate X and y.
7. Split into train and test sets.
8. Export a cleaned copy.
9. Read the exported file back and verify it.

**Checkpoint:** A model-ready dataset is not just a table with no errors. It is a well-understood dataset with valid features, a separate target and leakage-safe preprocessing.
