# Matplotlib Lesson Notes
## Beginner-Friendly Revision Notes

## 1. What is Matplotlib?

**Matplotlib** is a Python library used to create graphs and visualizations from data.

Common plot types include line plots, scatter plots, histograms, bar charts, and box plots.

Import it using:

```python
import matplotlib.pyplot as plt
```

The alias `plt` is a common short name for `matplotlib.pyplot`.

---

## 2. Creating Data for a Graph

### Using NumPy's `linspace()`

`np.linspace(start, stop, num)` creates `num` evenly spaced values between `start` and `stop`, including both endpoints.

```python
import numpy as np

x = np.linspace(0, 10, 5)
print(x)
```

Output:

```text
[ 0.   2.5  5.   7.5 10. ]
```

Here, `0` is the start, `10` is the end, and `5` is the number of values.

### Creating Y values from X values

```python
x = np.linspace(0, 5, 6)
y = x ** 2

print(x)
print(y)
```

`y = x ** 2` squares every value in `x`. For paired points in a line or scatter plot, X and Y should contain the same number of values.

### Using `range()`

`range(start, stop)` represents integers starting at `start` and ending just before `stop`.

```python
numbers = range(1, 6)
print(list(numbers))
```

Output:

```text
[1, 2, 3, 4, 5]
```

### Using `sample()`

`sample()` randomly selects a specified number of unique items from a population.

Syntax:

```python
sample(population, k)
```

Example:

```python
from random import sample

data = sample(range(1, 11), 4)
print(data)
```

One possible output:

```text
[8, 2, 10, 5]
```

Your output may differ because the selection is random.

- `range(1, 11)` provides the possible integers 1 through 10.
- `4` asks for four items.
- `sample()` selects items without repeating any item.
- The selected items are stored in `data` as a list.

**Remember:** `sample()` selects random data; it does not automatically create X and Y pairs.

---

## 3. Two Ways to Plot in Matplotlib

### A. Pyplot style (normal method)

In this style, use `plt` functions directly.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 30, 40]

plt.plot(x, y)
plt.title("Simple Line Plot")
plt.xlabel("X values")
plt.ylabel("Y values")
plt.grid(True)
plt.show()
```

Matplotlib works with the current figure and plotting area.

### B. Object-Oriented (OO) style

In this style, create a Figure and an Axes, then call methods on the Axes.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 30, 40]

fig, ax = plt.subplots()

ax.plot(x, y)
ax.set_title("Simple Line Plot")
ax.set_xlabel("X values")
ax.set_ylabel("Y values")
ax.grid(True)

plt.show()
```

### What are `fig` and `ax`?

- **Figure (`fig`)**: The complete figure or canvas.
- **Axes (`ax`)**: The area inside the figure where a graph is drawn. Axes means the whole plotting area, not just one axis line.

### Main differences

| Task | Pyplot style | Object-Oriented style |
|---|---|---|
| Draw a line | `plt.plot(x, y)` | `ax.plot(x, y)` |
| Set title | `plt.title("Title")` | `ax.set_title("Title")` |
| X-axis label | `plt.xlabel("X")` | `ax.set_xlabel("X")` |
| Y-axis label | `plt.ylabel("Y")` | `ax.set_ylabel("Y")` |
| Add grid | `plt.grid(True)` | `ax.grid(True)` |
| Show plot | `plt.show()` | `plt.show()` |
| Save figure | `plt.savefig("plot.png")` | `fig.savefig("plot.png")` |

**Recommendation:** Practise the Object-Oriented style using `fig, ax = plt.subplots()`. It is clear and convenient when working with multiple graphs and data science projects.

---

## 4. Understanding `plt.subplots()`

Example:

```python
fig, ax = plt.subplots(figsize=(8, 5))
```

This creates a Figure and one Axes.

- `fig` receives the Figure.
- `ax` receives the Axes.
- `figsize=(8, 5)` sets the overall figure size to 8 inches wide and 5 inches high.

Python assigns the two returned objects to `fig` and `ax`. This is called **unpacking**.

### Multiple subplots

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot([1, 2, 3], [1, 4, 9])
axes[0].set_title("Graph 1")

axes[1].plot([1, 2, 3], [1, 8, 27])
axes[1].set_title("Graph 2")

fig.tight_layout()
plt.show()
```

- `1, 2` means one row and two columns.
- `axes[0]` is the first plotting area.
- `axes[1]` is the second plotting area.
- `tight_layout()` helps prevent titles and labels from overlapping.

For a 2-by-2 grid:

```python
fig, axes = plt.subplots(2, 2, figsize=(10, 7))
```

This creates two rows and two columns of plotting areas.

---

## 5. Creating Axes Manually with `add_axes()`

Sometimes we want to choose the exact position and size of the plotting area.

```python
fig = plt.figure(figsize=(10, 6))
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8])

ax.plot([1, 2, 3], [10, 20, 30])
plt.show()
```

The values passed to `add_axes()` follow this order:

```python
[left, bottom, width, height]
```

These values are fractions of the Figure's dimensions, generally between 0 and 1.

| Value | Meaning |
|---|---|
| First `0.1` | Position 10% from the left |
| Second `0.1` | Position 10% from the bottom |
| `0.8` width | Use 80% of the Figure's width |
| `0.8` height | Use 80% of the Figure's height |

### `subplots()` vs `add_axes()`

| `plt.subplots()` | `fig.add_axes()` |
|---|---|
| Automatically arranges plotting areas | You specify the position and size |
| Convenient for one or many graphs | Useful for custom layouts or inset graphs |
| Best default choice for daily practice | Use when precise placement is needed |

You can also change an Axes' position later:

```python
ax.set_position([0.2, 0.2, 0.6, 0.6])
```

---

## 6. Common Plot Types

### A. Line plot

A line plot shows how values change or how two sets of values relate.

```python
x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

fig, ax = plt.subplots()
ax.plot(x, y)
plt.show()
```

### B. Scatter plot

A scatter plot shows individual points using paired X and Y values.

```python
from random import sample

x = sample(range(1, 100), 10)
y = sample(range(1, 100), 10)

fig, ax = plt.subplots()
ax.scatter(x, y)
plt.show()
```

The first X value pairs with the first Y value, the second X value pairs with the second Y value, and so on. The X and Y collections should have equal lengths.

### C. Histogram

A histogram shows how numerical data is distributed. It groups values into intervals called **bins** and counts the values in each interval.

```python
from random import sample

data = sample(range(1, 1000), 100)

fig, ax = plt.subplots()
ax.hist(data, bins=10)
plt.show()
```

A histogram uses one dataset. Matplotlib chooses intervals and counts how many data values fall into each interval.

### D. Bar chart

A bar chart compares values across categories.

```python
categories = ["A", "B", "C"]
values = [10, 25, 15]

fig, ax = plt.subplots()
ax.bar(categories, values)
plt.show()
```

### E. Box plot

A box plot summarizes the distribution of numerical data. It can help show the median, spread, and potential outliers.

```python
data = [10, 12, 13, 15, 18, 20, 35]

fig, ax = plt.subplots()
ax.boxplot(data)
plt.show()
```

### Plot type summary

| Plot | Main purpose | Typical input |
|---|---|---|
| Line plot | Show a trend or relationship | X and Y |
| Scatter plot | Show relationships between paired values | X and Y |
| Histogram | Show the distribution of values | One numerical dataset |
| Bar chart | Compare categories | Categories and values |
| Box plot | Summarize spread and potential outliers | One or more numerical datasets |

---

## 7. Customizing a Plot

You can customize the line, markers, labels, and grid.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 5, 11)
y = x ** 3

fig, ax = plt.subplots(figsize=(8, 5))

ax.plot(
    x, y,
    color="blue",
    linewidth=2,
    linestyle="--",
    marker="o",
    markersize=5,
    label="y = x³"
)

ax.set_title("Cubic Function")
ax.set_xlabel("X values")
ax.set_ylabel("Y values")
ax.grid(True, alpha=0.3)
ax.legend()

fig.tight_layout()
plt.show()
```

| Property | Example | Meaning |
|---|---|---|
| `color` | `color="red"` | Line color |
| `linewidth` | `linewidth=3` | Line thickness |
| `linestyle` | `linestyle="--"` | Dashed line |
| `marker` | `marker="o"` | Circular markers at data points |
| `markersize` | `markersize=8` | Marker size |
| `alpha` | `alpha=0.5` | Transparency; 0 is transparent and 1 is opaque |
| `label` | `label="Sales"` | Name used in the legend |
| `ax.legend()` | `ax.legend()` | Display the legend |
| `ax.grid(True)` | `ax.grid(True)` | Display grid lines |

---

## 8. Saving a Plot

Save a figure using `savefig()`.

### Pyplot style

```python
plt.savefig("my_plot.png", dpi=300)
```

### Object-Oriented style

```python
fig.savefig("my_plot.png", dpi=300)
```

- `"my_plot.png"` is the filename.
- `dpi=300` specifies the image resolution.
- Saving before `plt.show()` is a reliable habit across environments.

---

## 9. Quick Revision

| Term | Simple meaning |
|---|---|
| `plt` | Pyplot interface |
| `fig` | Complete Figure or canvas |
| `ax` | Plotting area |
| `plt.subplots()` | Creates a Figure and one or more Axes |
| `fig.add_axes()` | Adds an Axes at a specified position |
| `figsize` | Overall Figure size in inches |
| `np.linspace()` | Creates evenly spaced numerical values |
| `range()` | Represents a sequence of integers |
| `sample()` | Randomly selects unique items |
| `plot()` | Draws a line plot |
| `scatter()` | Draws individual points |
| `hist()` | Draws a histogram |
| `bar()` | Draws a bar chart |
| `boxplot()` | Draws a box plot |
| `tight_layout()` | Helps improve spacing |
| `savefig()` | Saves a figure to a file |
| `show()` | Displays the plot |

---

## 10. Recommended Practice Order

1. Create X values using `np.linspace()`.
2. Calculate Y values using a formula such as `y = x ** 2`.
3. Draw a line plot with `fig, ax = plt.subplots()`.
4. Add a title, axis labels, grid, and legend.
5. Practise styling with colors, line styles, and markers.
6. Create two or four subplots.
7. Practise scatter plots, histograms, bar charts, and box plots.
8. Learn `fig.add_axes()` for custom positioning.
9. Save a graph using `fig.savefig()`.

**Final takeaway:** Use `fig, ax = plt.subplots()` as your standard starting point. Remember that the Figure is the whole canvas, the Axes is the plotting area, and the plot type determines what kind of data you need.
