# 01 — Data Visualization Fundamentals

> **Goal:** Understand why we visualize data, choose an appropriate chart and avoid misleading visual communication.

## 1. What is data visualization?

Data visualization is the presentation of information using charts, plots and graphs. Instead of reading hundreds of numbers, a viewer can quickly notice patterns, comparisons, trends, clusters and unusual values.

Examples:
- sales changing over time,
- marks across students,
- distribution of customer ages,
- relationship between advertising spend and revenue.

## 2. Why visualize data?

Visualization helps with:
1. **Exploration:** discover patterns before modeling.
2. **Comparison:** compare categories or groups.
3. **Distribution:** understand spread, skewness and outliers.
4. **Relationships:** see how variables move together.
5. **Communication:** explain findings to other people.

A chart is not decoration. It should answer a question.

## 3. Choose the chart based on the question

| Question | Suitable chart |
|---|---|
| How does a value change over time? | Line plot |
| Which category is larger? | Bar plot |
| How are numerical values distributed? | Histogram |
| Are two numerical variables related? | Scatter plot |
| How spread out are values? | Box plot / violin plot |
| How are two categories associated? | Heatmap / count plot |
| How do several numeric features relate? | Pair plot |

## 4. Understand variables

- **Numerical variable:** measured or counted, such as age, marks or price.
- **Categorical variable:** labels or groups, such as department or product type.
- **Time variable:** date/time sequence.
- **Ordinal variable:** category with a meaningful order, such as low, medium and high.

The data type influences the chart. A histogram is designed for numerical distributions; a bar chart is commonly used for category comparisons.

## 5. Matplotlib and Seaborn

**Matplotlib** is a foundational plotting library. It gives detailed control over figures, axes, labels, scales and layout.

**Seaborn** is built on Matplotlib and provides a higher-level interface, attractive statistical plots and convenient integration with DataFrames.

They are complementary:
- use Matplotlib for low-level control and custom layouts,
- use Seaborn for quick statistical visualizations,
- combine them when needed.

## 6. Install and import

```bash
pip install numpy pandas matplotlib seaborn
```

```python
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
```

In notebooks, plots often display automatically. In a normal Python script, call `plt.show()`.

## 7. The basic chart checklist

Every chart should make these clear:
- What is being measured?
- Which groups or time periods are shown?
- What are the units?
- What does each color or symbol represent?
- Is the scale appropriate?
- Is the chart title a useful summary?

## 8. Avoid misleading charts

- Do not crop a bar chart's y-axis in a way that exaggerates differences.
- Do not use 3-D effects when they make values harder to compare.
- Do not use too many colors without meaning.
- Do not overload one chart with too many categories.
- Do not imply causation from a visual correlation.
- Do not omit units or axis labels.

## 9. A simple exploration workflow

1. Inspect the dataset with Pandas.
2. Identify numerical and categorical columns.
3. State the question you want to answer.
4. Choose a chart type.
5. Add title, axis labels and units.
6. Check for misleading scales or clutter.
7. Explain the insight in one or two sentences.

## 10. Practice

For a student dataset containing department, marks, attendance and study hours, choose:
1. A chart to compare average marks by department.
2. A chart to show the distribution of marks.
3. A chart to inspect the relationship between study hours and marks.
4. A chart to compare attendance over a semester.

**Checkpoint:** Before writing plotting code, state the question and the variable types. The chart choice should follow from those.
