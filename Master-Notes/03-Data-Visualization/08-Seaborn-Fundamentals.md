# 08 — Seaborn Fundamentals

> **Goal:** Use Seaborn's high-level statistical plotting interface with Pandas DataFrames and understand how it differs from Matplotlib.

## 1. What is Seaborn?

Seaborn is a statistical data-visualization library built on top of Matplotlib. It provides convenient functions for common statistical charts and works naturally with Pandas DataFrames.

```python
import seaborn as sns
import matplotlib.pyplot as plt
import pandas as pd
```

## 2. Create a sample DataFrame

```python
df = pd.DataFrame({
    "Department": ["CSE", "ECE", "CSE", "ISE", "ECE", "CSE"],
    "Marks": [85, 72, 91, 65, 78, 88],
    "Hours": [4, 2, 5, 1, 3, 4]
})
```

## 3. Seaborn's data-oriented syntax

```python
sns.scatterplot(data=df, x="Hours", y="Marks", hue="Department")
plt.show()
```

- `data`: DataFrame or other supported data source.
- `x`, `y`: column names.
- `hue`: map color to a variable.
- `style`: map marker style.
- `size`: map marker size.

This is often easier than manually extracting arrays and creating separate series.

## 4. Common Seaborn plots

```python
sns.histplot(data=df, x="Marks", kde=True)
sns.boxplot(data=df, x="Department", y="Marks")
sns.violinplot(data=df, x="Department", y="Marks")
sns.countplot(data=df, x="Department")
sns.barplot(data=df, x="Department", y="Marks")
```

Each function answers a different question:
- histogram: numerical distribution,
- box/violin: distribution by category,
- countplot: category frequencies,
- barplot: estimate a numerical statistic by category (mean by default).

## 5. Barplot versus countplot

`countplot` counts observations in each category.

`barplot` estimates a numerical value for each category. By default, Seaborn's barplot uses an estimator such as the mean and may display an uncertainty interval.

If you already calculated one value per category, a Matplotlib bar plot or Seaborn barplot with an appropriate estimator/interval setting may be suitable. Know what the height represents.

## 6. Add a theme

```python
sns.set_theme(style="whitegrid", context="notebook")
```

Themes control visual defaults such as background, grid and scaling. You can still customize the Matplotlib Axes after creating a Seaborn plot.

## 7. Customize using Matplotlib

```python
ax = sns.scatterplot(data=df, x="Hours", y="Marks", hue="Department")
ax.set_title("Study Hours and Marks")
ax.set_xlabel("Study Hours per Day")
ax.set_ylabel("Exam Marks")
plt.show()
```

Seaborn often returns a Matplotlib Axes object, allowing further customization.

## 8. Figure-level versus axes-level functions

Some Seaborn functions create a figure-level object, such as `relplot` or `catplot`. Others, such as `scatterplot` and `boxplot`, draw onto an Axes.

Figure-level functions are convenient for faceting (multiple panels split by a category). Axes-level functions are convenient when you want to control a Matplotlib subplot layout yourself.

## 9. Common mistakes

- Confusing countplot with barplot.
- Passing the wrong column names in `x` and `y`.
- Assuming every Seaborn function returns the same object type.
- Forgetting that barplot usually estimates a statistic rather than simply plotting raw values.
- Adding too many hue categories and creating a cluttered legend.

## 10. Practice

Use a student DataFrame to create a histogram, count plot, bar plot, box plot and scatter plot. For each chart, write the question it answers and explain what each axis or visual encoding represents.

**Checkpoint:** Seaborn makes statistical plots convenient; Matplotlib gives you detailed control over the resulting figure.
