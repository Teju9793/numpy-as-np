# 13 — Feature Engineering with Pandas

> **Goal:** Create useful input features from raw columns while avoiding leakage and preserving the meaning of the data.

## 1. What is a feature?

A **feature** is an input variable used by an analysis or machine-learning model. For a student performance model, study hours and attendance may be features, while final marks may be the target.

**Feature engineering** means creating, transforming or selecting features so that they represent useful information for a task.

## 2. Create a feature from existing columns

```python
import pandas as pd

df = pd.DataFrame({
    "Math": [80, 60, 90],
    "Science": [70, 75, 85],
    "English": [90, 65, 95]
})

df["Total"] = df[["Math", "Science", "English"]].sum(axis=1)
df["Average"] = df["Total"] / 3
```

Each new column is calculated from the original subject marks.

## 3. Combine categorical information

```python
df = pd.DataFrame({
    "City": ["Tumkur", "Bengaluru"],
    "Department": ["CSE", "ECE"]
})

df["City_Department"] = df["City"] + "_" + df["Department"]
```

Combined categories can represent an interaction, but they can also create too many unique values. Consider whether the combination has a meaningful relationship to the target.

## 4. Extract date-based features

```python
df = pd.DataFrame({"Date": pd.to_datetime([
    "2026-01-10", "2026-02-15", "2026-03-20"
])})

df["Month"] = df["Date"].dt.month
df["Weekday"] = df["Date"].dt.dayofweek
df["Is_weekend"] = df["Date"].dt.dayofweek >= 5
```

Date features can reveal seasonal or weekly patterns. Use only information that would be available at prediction time.

## 5. Binning continuous values

Binning groups numeric values into intervals:

```python
ages = pd.Series([18, 22, 35, 48, 61])
bins = [0, 20, 40, 60, 100]
labels = ["0-20", "21-40", "41-60", "61+"]

age_group = pd.cut(ages, bins=bins, labels=labels, right=True)
print(age_group)
```

The exact boundary behavior depends on options such as `right` and `include_lowest`. Always check the interval definitions.

## 6. One-hot encoding categorical variables

Many ML algorithms require numerical inputs. One-hot encoding creates indicator columns for categories:

```python
df = pd.DataFrame({"Department": ["CSE", "ECE", "CSE", "ISE"]})
encoded = pd.get_dummies(df, columns=["Department"], dtype=int)
print(encoded)
```

Each category becomes a separate 0/1 column. For production ML pipelines, scikit-learn's encoders can handle categories consistently between training and test data.

## 7. Frequency encoding and ordinal values

For a category, frequency encoding replaces each label with its count or frequency. Ordinal encoding maps categories to ordered integers.

Do not assign arbitrary numbers to unordered categories and assume the model will understand them as labels. For example, mapping CSE=1, ECE=2 and ISE=3 creates an artificial order that may not exist.

## 8. Scaling numerical features

Common scaling ideas:
- **Standardization:** subtract mean and divide by standard deviation.
- **Min-max scaling:** map values into a chosen range, often 0 to 1.
- **Robust scaling:** use median and interquartile range to reduce sensitivity to outliers.

Pandas can calculate the formulas, but scikit-learn preprocessing tools are usually better for reusable ML pipelines.

## 9. Avoid data leakage

Never use information that would not be available at prediction time. Also, fit transformations such as scaling, imputation and category encoding on training data only, then apply them to validation/test data.

For example, computing the mean of a feature using the entire dataset before splitting leaks information from the test set.

## 10. Feature selection

More features do not always mean a better model. Remove features that:
- duplicate the same information,
- contain identifiers with no predictive meaning,
- leak the target,
- are mostly missing or unreliable,
- are unavailable at prediction time.

Use validation data and domain knowledge to assess usefulness.

## 11. Common mistakes

- Creating a feature that directly reveals the target.
- Encoding unordered categories as arbitrary integers.
- Fitting scaling or imputation on the entire dataset.
- Creating bins without checking their boundaries.
- Assuming a new feature automatically improves model performance.

## 12. Practice

Use a student dataset to create total marks, average marks, attendance bands, weekday/month features and one-hot department columns. Identify which transformations must be fitted only on training data.

**Checkpoint:** Every engineered feature should have a clear meaning, be available at prediction time and be created without leaking test information.
