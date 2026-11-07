# 03 — Line Plots and Scatter Plots

> **Goal:** Use line plots to show trends and scatter plots to inspect relationships between two numerical variables.

## 1. Line plot — show change across an ordered axis

A line plot connects data points in sequence. It is useful when x-values have a meaningful order, especially time.

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr", "May"]
sales = [120, 150, 135, 180, 210]

fig, ax = plt.subplots()
ax.plot(months, sales, marker="o")
ax.set_title("Monthly Sales")
ax.set_xlabel("Month")
ax.set_ylabel("Sales (units)")
ax.grid(True)
plt.show()
```

The line helps the viewer see direction and changes over time.

## 2. Multiple lines

```python
months = [1, 2, 3, 4]
city_a = [20, 22, 21, 25]
city_b = [18, 19, 23, 24]

fig, ax = plt.subplots()
ax.plot(months, city_a, marker="o", label="City A")
ax.plot(months, city_b, marker="s", label="City B")
ax.set_xlabel("Month")
ax.set_ylabel("Temperature (°C)")
ax.legend()
plt.show()
```

Use distinct labels and a restrained set of visual styles. Too many lines can make the chart unreadable.

## 3. Scatter plot — show paired observations

A scatter plot places one point for each pair ((x,y)). It is useful for exploring whether two numerical variables are associated.

```python
study_hours = [1, 2, 3, 4, 5, 6]
marks = [35, 42, 55, 62, 78, 85]

fig, ax = plt.subplots()
ax.scatter(study_hours, marks)
ax.set_xlabel("Study Hours")
ax.set_ylabel("Marks")
ax.set_title("Study Hours vs Marks")
plt.show()
```

Each dot represents one student. The overall pattern may suggest a positive relationship, but it does not prove that study hours alone caused the marks.

## 4. Interpret scatter patterns

- **Positive association:** y tends to increase as x increases.
- **Negative association:** y tends to decrease as x increases.
- **No clear linear association:** no obvious upward or downward pattern.
- **Clusters:** groups of observations.
- **Outliers:** points far from the main pattern.
- **Nonlinear pattern:** a curve or other structured relationship.

Always consider context and possible third variables.

## 5. Add size or color to encode another variable

```python
fig, ax = plt.subplots()
scatter = ax.scatter(
    study_hours,
    marks,
    s=[40, 60, 80, 100, 120, 140],
    c=[1, 2, 1, 2, 1, 2],
    alpha=0.7
)
ax.set_xlabel("Study Hours")
ax.set_ylabel("Marks")
plt.show()
```

Marker size or color can represent another variable. If color represents a numerical value, add a colorbar and label it. If it represents categories, explain the category mapping.

## 6. Regression line as a visual guide

Seaborn can add a fitted trend line:

```python
import seaborn as sns
import pandas as pd

data = pd.DataFrame({
    "Hours": [1, 2, 3, 4, 5, 6],
    "Marks": [35, 42, 55, 62, 78, 85]
})
sns.regplot(data=data, x="Hours", y="Marks")
plt.show()
```

The line summarizes a linear trend. It is not proof of causation and may not be appropriate if the relationship is nonlinear or assumptions are violated.

## 7. Line plot versus scatter plot

| Line plot | Scatter plot |
|---|---|
| Connects observations | Shows separate points |
| Useful for ordered sequences | Useful for paired numerical values |
| Emphasizes trend or continuity | Emphasizes relationship, clusters and outliers |
| X-axis often time/order | X-axis is another variable |

Do not connect unrelated categories with a line because that implies an order or continuity that may not exist.

## 8. Common mistakes

- Using a line plot for unrelated categories.
- Connecting time points that are not in chronological order.
- Assuming a visible association proves causation.
- Hiding overlapping points in dense scatter plots; use transparency or sampling.
- Forgetting to label size/color encodings.

## 9. Practice

1. Plot monthly revenue as a line chart.
2. Plot study hours against exam marks as a scatter plot.
3. Add a second city's line to compare trends.
4. Identify positive, negative and nonlinear patterns using sample data.
5. Add a third variable through point color and explain its meaning.

**Checkpoint:** Ask whether the x-axis is an ordered sequence or a separate numerical variable before choosing line versus scatter.
