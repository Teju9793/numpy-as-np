# 06 — Box Plots and Violin Plots

> **Goal:** Compare distributions using quartiles, median, whiskers, potential outliers and density shape.

## 1. Why use box plots?

A mean alone cannot describe a dataset. Two groups can have the same mean but very different spread. Box plots summarize the center and variability compactly.

## 2. Five-number summary

A box plot is based on:
1. Minimum (often represented by the lower whisker endpoint under the chosen rule).
2. First quartile (Q1, 25th percentile).
3. Median (Q2, 50th percentile).
4. Third quartile (Q3, 75th percentile).
5. Maximum (often represented by the upper whisker endpoint under the chosen rule).

The box spans Q1 to Q3. Its height is the **interquartile range**:

[
IQR=Q3-Q1
]

The line inside the box is the median.

## 3. Create a box plot

```python
import matplotlib.pyplot as plt

marks = [35, 40, 45, 50, 55, 60, 60, 65, 70, 75, 80, 100]
plt.boxplot(marks)
plt.ylabel("Marks")
plt.title("Exam Marks")
plt.show()
```

## 4. What do whiskers mean?

In the common Tukey box plot, whiskers extend to the most extreme observations within:

[
[Q1-1.5\times IQR,\ Q3+1.5\times IQR]
]

Points outside these limits are plotted individually as potential outliers. They are not automatically errors. Different plotting options can change whisker definitions.

## 5. Compare categories

```python
import seaborn as sns
import pandas as pd

df = pd.DataFrame({
    "Department": ["CSE"] * 5 + ["ECE"] * 5,
    "Marks": [70, 75, 80, 85, 90, 55, 65, 70, 75, 95]
})

sns.boxplot(data=df, x="Department", y="Marks")
plt.show()
```

This helps compare medians and spreads between departments.

## 6. Violin plot

A violin plot combines a distribution-density estimate with summary information. Its width indicates where values are more concentrated.

```python
sns.violinplot(data=df, x="Department", y="Marks", inner="quart")
plt.show()
```

A wide section means the estimated density is higher around those values. The shape depends on smoothing choices and sample size.

## 7. Box plot versus violin plot

| Box plot | Violin plot |
|---|---|
| Compact quartile summary | Shows estimated density shape |
| Easy to compare medians and IQR | Reveals multiple peaks or concentration |
| Does not show full distribution shape | Shape can be harder to interpret |
| Good for concise reports | Useful for deeper distribution exploration |

## 8. Outliers need investigation

A potential outlier could be:
- a data-entry error,
- a rare but valid observation,
- a different population,
- an event that deserves further analysis.

Do not automatically remove outliers. Check the source and the purpose of the analysis.

## 9. Common mistakes

- Calling every point outside whiskers an error.
- Confusing whiskers with the absolute minimum and maximum in every configuration.
- Comparing box plots without checking sample sizes.
- Treating violin width as raw count.
- Ignoring small sample sizes when interpreting density curves.

## 10. Practice

1. Create a box plot for marks.
2. Compare marks across three departments.
3. Identify median and IQR.
4. Create a violin plot and compare the distribution shape.
5. Investigate a potential outlier rather than deleting it automatically.

**Checkpoint:** Use box plots for a compact statistical summary and violin plots when the distribution's shape matters.
