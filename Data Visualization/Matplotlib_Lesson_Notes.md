
# Matplotlib — Complete Learning Notes

Beginner-friendly notes with explanations, examples, styling properties, shorthand formats, and reference tables. These notes focus on plotting data with Matplotlib; image-loading and image-manipulation topics are intentionally not included.

## Contents

1. What Matplotlib is and how a graph works
2. Importing Matplotlib and preparing data
3. Understanding `range()`, `sample()`, and `np.linspace()`
4. The Pyplot and Object-Oriented approaches
5. Figure, Axes, axis, and `subplots()`
6. Manually positioning an Axes with `add_axes()`
7. Common plot types
8. Styling line plots
9. Styling shortcuts and format strings
10. Titles, labels, legends, grids, limits, and ticks
11. Multiple lines and multiple subplots
12. Layout, saving, and displaying figures
13. Method reference tables
14. Common beginner mistakes
15. Mini practice tasks
16. Quick revision sheet

---

## 1. What is Matplotlib?

**Matplotlib** is a Python library for creating graphs and visualizations from numerical or categorical data. It helps us see patterns, compare values, understand distributions, and communicate results.

Common plot types include:

- **Line plot:** shows a trend or change across ordered X values.
- **Scatter plot:** shows the relationship between paired X and Y values.
- **Bar chart:** compares values across categories.
- **Histogram:** shows how numerical values are distributed.
- **Box plot:** summarizes the spread of numerical data.

### Install and import

If Matplotlib is not installed, run this in a terminal:

```bash
python -m pip install matplotlib numpy
```

Import it in a Python program or notebook:

```python
import numpy as np
import matplotlib.pyplot as plt
```

- `matplotlib.pyplot` provides convenient plotting functions.
- `as plt` gives it the widely used short name `plt`.
- `numpy` helps create and work with numerical arrays.
- `as np` is the common short name for NumPy.

### Your first graph

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

plt.plot(x, y)
plt.show()
```

**What happens?**

1. `x` contains the horizontal coordinates.
2. `y` contains the corresponding vertical values.
3. `plt.plot(x, y)` draws a line through the points.
4. `plt.show()` displays the graph.

The first X value is paired with the first Y value, the second X value with the second Y value, and so on. For this kind of plot, X and Y must have compatible lengths.

---

## 2. Understanding data before plotting

A graph is only useful when we understand the data being plotted.

### 2.1 X values and Y values

```python
x = [1, 2, 3, 4]
y = [5, 8, 6, 12]
```

The paired coordinates are:

| Point | X | Y |
|---|---:|---:|
| 1 | 1 | 5 |
| 2 | 2 | 8 |
| 3 | 3 | 6 |
| 4 | 4 | 12 |

Matplotlib pairs values by position. It does not automatically decide which values are related; you supply that relationship.

### 2.2 Create evenly spaced values with `np.linspace()`

Syntax:

```python
np.linspace(start, stop, num)
```

It returns `num` evenly spaced numerical values from `start` to `stop`, including both endpoints by default.

```python
import numpy as np

x = np.linspace(0, 10, 5)
print(x)
```

Output:

```text
[ 0.   2.5  5.   7.5 10. ]
```

Explanation:
- `0` is the starting value.
- `10` is the ending value.
- `5` is the number of values to create.
- The gap between values is equal: 2.5.

Use `linspace()` when a smooth mathematical curve needs many X values.

Example:

```python
x = np.linspace(0, 5, 100)
y = x ** 2
```

This creates 100 X values from 0 to 5, then computes the square of every X value. The result gives enough points to draw a smooth-looking curve.

### 2.3 Understand `range()`

`range(start, stop)` represents integers from `start` up to, but not including, `stop`.

```python
numbers = range(1, 6)
print(list(numbers))
```

Output:

```text
[1, 2, 3, 4, 5]
```

The stop value is excluded. This is why `range(1, 1000)` can provide integers from 1 through 999.

### 2.4 Understand `sample()`

The `sample()` function from Python's `random` module selects a chosen number of **unique items** from a population. It selects without replacement, so an item cannot be selected twice in the same call.

Syntax:

```python
sample(population, k)
```

- `population`: the items to select from.
- `k`: the number of items to choose.

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

Your result can differ because the selection is random. The population contains integers 1 to 10, and `4` asks Python to choose four of them.

**Important:** `sample()` does not automatically create X and Y pairs. It simply returns a list of randomly selected values.

### 2.5 Choosing a data creation method

| Tool | Purpose | Example |
|---|---|---|
| `range()` | Represent a sequence of integers | `range(1, 6)` |
| `sample()` | Randomly select unique items | `sample(range(1, 100), 10)` |
| `np.linspace()` | Create evenly spaced numerical values | `np.linspace(0, 10, 100)` |
| A Python list | Enter known values manually | `[10, 15, 20]` |
| NumPy calculation | Calculate values from a formula | `y = x ** 2` |

---

## 3. Two ways to write Matplotlib code

Matplotlib can be used through the **Pyplot interface** or the **Object-Oriented (OO) interface**. Both can make the same kinds of graphs, but they organize code differently.

### 3.1 Pyplot style — the normal method

With the Pyplot style, you call functions directly on `plt`.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

plt.plot(x, y)
plt.title("Weekly Values")
plt.xlabel("Day")
plt.ylabel("Value")
plt.grid(True)
plt.show()
```

Matplotlib uses the current figure and Axes. This style is convenient for short scripts and quick experiments.

### 3.2 Object-Oriented style

With the OO style, you create a Figure and Axes objects, then call the plotting methods on the Axes object.

```python
import matplotlib.pyplot as plt

x = [1, 2, 3, 4]
y = [10, 20, 15, 30]

fig, ax = plt.subplots()

ax.plot(x, y)
ax.set_title("Weekly Values")
ax.set_xlabel("Day")
ax.set_ylabel("Value")
ax.grid(True)
plt.show()
```

The graph belongs to `ax`. The overall figure belongs to `fig`.

### 3.3 Method comparison

| Task | Pyplot style | Object-Oriented style |
|---|---|---|
| Draw line | `plt.plot(x, y)` | `ax.plot(x, y)` |
| Draw scatter plot | `plt.scatter(x, y)` | `ax.scatter(x, y)` |
| Draw histogram | `plt.hist(data)` | `ax.hist(data)` |
| Set title | `plt.title("Title")` | `ax.set_title("Title")` |
| X label | `plt.xlabel("X")` | `ax.set_xlabel("X")` |
| Y label | `plt.ylabel("Y")` | `ax.set_ylabel("Y")` |
| Add legend | `plt.legend()` | `ax.legend()` |
| Add grid | `plt.grid(True)` | `ax.grid(True)` |
| Save the figure | `plt.savefig("plot.png")` | `fig.savefig("plot.png")` |
| Display | `plt.show()` | `plt.show()` |

**Which should you use?** Use `fig, ax = plt.subplots()` as your default for learning, Data Science, and projects. The OO style makes it clear which graph you are modifying, especially when there are several graphs. Learn the Pyplot style too, because it appears in many tutorials.

---

## 4. Figure, Axes, axis, and `subplots()`

### 4.1 What is a Figure?

A **Figure** is the entire canvas that contains one or more plotting areas, titles, labels, and other plot elements.

```python
fig = plt.figure(figsize=(8, 5))
```

The `figsize` value uses inches: 8 inches wide by 5 inches high. It does not mean pixels.

### 4.2 What is an Axes?

An **Axes** object represents one plotting area. It holds the data plotted there and its title, labels, ticks, legend, and grid.

```python
fig, ax = plt.subplots()
ax.plot([1, 2, 3], [10, 20, 30])
```

### 4.3 What is an axis?

An **axis** is one direction or scale, such as the horizontal X-axis or vertical Y-axis. An **Axes** object is the complete plotting area, which contains both axes. The names look similar but refer to different things.

### 4.4 Understanding `fig, ax = plt.subplots()`

```python
fig, ax = plt.subplots(figsize=(8, 5))
```

`plt.subplots()` returns a Figure and an Axes. Python unpacks those two returned objects into the variables `fig` and `ax`.

- `fig` is the full canvas.
- `ax` is the plotting area.
- `figsize=(8, 5)` controls the Figure's dimensions in inches.

### 4.5 Make multiple subplots

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot([1, 2, 3], [1, 4, 9])
axes[0].set_title("Squares")

axes[1].plot([1, 2, 3], [1, 8, 27])
axes[1].set_title("Cubes")

fig.tight_layout()
plt.show()
```

- `plt.subplots(1, 2)` means one row and two columns.
- `axes[0]` is the first Axes; indexes start at 0.
- `axes[1]` is the second Axes.
- `fig.tight_layout()` adjusts spacing to help prevent overlap.

For a 2-by-2 grid:

```python
fig, axes = plt.subplots(2, 2, figsize=(10, 7))
```

This creates four Axes in two rows and two columns. For a regular grid, Matplotlib handles the positioning for you.

---

## 5. Position an Axes manually with `add_axes()`

Use `fig.add_axes()` when you need to place an Axes at a precise location inside the Figure.

```python
fig = plt.figure(figsize=(10, 6))
ax = fig.add_axes([0.1, 0.1, 0.8, 0.8])

ax.plot([1, 2, 3], [10, 20, 30])
plt.show()
```

The list has this order:

```python
[left, bottom, width, height]
```

The numbers are fractions of the Figure's width and height, not pixels.

| Value in the example | Meaning |
|---|---|
| First `0.1` | Left edge starts at 10% of Figure width |
| Second `0.1` | Bottom edge starts at 10% of Figure height |
| Third `0.8` | Axes uses 80% of Figure width |
| Fourth `0.8` | Axes uses 80% of Figure height |

You can adjust an Axes created by `subplots()` too:

```python
ax.set_position([0.2, 0.2, 0.6, 0.6])
```

| `plt.subplots()` | `fig.add_axes()` |
|---|---|
| Automatically positions Axes | You provide the exact position |
| Convenient for one or many plots | Useful for custom or inset layouts |
| Recommended for routine practice | Use when you need precise placement |

**Daily practice tip:** Start with `plt.subplots()`. Learn `add_axes()` when you specifically need manual placement.

---

## 6. Common plot types

### 6.1 Line plot — `plot()`

A line plot connects ordered points. It is useful for trends over time or for showing a mathematical relationship.

```python
x = [1, 2, 3, 4, 5]
y = [10, 15, 12, 22, 28]

fig, ax = plt.subplots()
ax.plot(x, y)
ax.set_title("Values Over Time")
ax.set_xlabel("Time")
ax.set_ylabel("Value")
plt.show()
```

The first X value pairs with the first Y value. Lines connect the points in the order supplied.

### 6.2 Scatter plot — `scatter()`

A scatter plot draws individual points without connecting them by lines. It can help you inspect the relationship between two variables.

```python
x = [5, 12, 20, 33, 42]
y = [40, 15, 60, 25, 70]

fig, ax = plt.subplots()
ax.scatter(x, y)
ax.set_xlabel("X values")
ax.set_ylabel("Y values")
ax.set_title("Scatter Plot")
plt.show()
```

Each X value pairs with the Y value in the same position. X and Y should have the same number of values for this example.

### 6.3 Histogram — `hist()`

A histogram shows the distribution of numerical data. Matplotlib divides the numerical range into intervals called **bins** and counts how many values fall into each bin.

```python
from random import sample

data = sample(range(1, 1000), 100)

fig, ax = plt.subplots()
ax.hist(data, bins=10, edgecolor="black")
ax.set_title("Distribution of Random Values")
ax.set_xlabel("Value range")
ax.set_ylabel("Frequency")
plt.show()
```

- `data` is one numerical dataset.
- `bins=10` requests ten intervals.
- The vertical axis shows the count of data values in each interval.
- `edgecolor="black"` outlines each bar.

Use a histogram to answer questions such as “Are most values low, high, or near the middle?”

### 6.4 Bar chart — `bar()`

A bar chart compares values for distinct categories.

```python
subjects = ["Math", "Python", "Science", "English"]
marks = [88, 92, 78, 84]

fig, ax = plt.subplots()
ax.bar(subjects, marks, color="steelblue")
ax.set_title("Marks by Subject")
ax.set_xlabel("Subject")
ax.set_ylabel("Marks")
plt.show()
```

Categories are shown along the X-axis and their corresponding values determine bar heights.

### 6.5 Horizontal bar chart — `barh()`

A horizontal bar chart is helpful when category names are long.

```python
subjects = ["Mathematics", "Python Programming", "Engineering Chemistry"]
marks = [88, 92, 78]

fig, ax = plt.subplots()
ax.barh(subjects, marks)
ax.set_xlabel("Marks")
ax.set_title("Marks by Subject")
plt.show()
```

### 6.6 Box plot — `boxplot()`

A box plot summarizes the spread of numerical data. It helps show the median, the middle half of the data, the spread beyond the box, and potential outliers.

```python
marks = [55, 60, 62, 66, 68, 70, 72, 75, 95]

fig, ax = plt.subplots()
ax.boxplot(marks)
ax.set_ylabel("Marks")
ax.set_title("Spread of Marks")
plt.show()
```

A box plot is useful when you want a compact view of distribution rather than every individual value.

### Plot type comparison

| Plot | Main purpose | Typical data |
|---|---|---|
| Line plot | Trend or relationship | X and Y values |
| Scatter plot | Relationship between paired values | X and Y values |
| Histogram | Distribution and frequency | One numerical dataset |
| Bar chart | Compare categories | Category labels and values |
| Horizontal bar | Compare categories with horizontal bars | Labels and values |
| Box plot | Summarize distribution and spread | One or more numerical datasets |

---

## 7. Styling a line plot

Styling makes a graph easier to read. You can control color, line thickness, line pattern, markers, transparency, and the order in which objects are drawn.

### 7.1 Full example

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
    markersize=6,
    alpha=0.9,
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

### 7.2 Styling property reference

| Property | Example | Meaning |
|---|---|---|
| `color` | `color="red"` | Changes the line color |
| `linewidth` | `linewidth=3` | Changes line thickness |
| `linestyle` | `linestyle="--"` | Uses a dashed line |
| `marker` | `marker="o"` | Adds circular markers at the data points |
| `markersize` | `markersize=8` | Changes marker size |
| `markerfacecolor` | `markerfacecolor="yellow"` | Changes the marker's fill color |
| `markeredgecolor` | `markeredgecolor="black"` | Changes the marker's outline color |
| `markeredgewidth` | `markeredgewidth=1.5` | Changes marker outline thickness |
| `alpha` | `alpha=0.5` | Controls transparency: 0 is transparent, 1 is opaque |
| `label` | `label="Sales"` | Sets the name that can appear in a legend |
| `zorder` | `zorder=3` | Controls drawing order; larger values are drawn in front of lower ones |

### 7.3 Color options

You can give a color by name, a short code, a hex color, or an RGB/RGBA tuple.

```python
ax.plot(x, y, color="purple")
ax.plot(x, y, color="r")
ax.plot(x, y, color="#1f77b4")
```

Common color names include `"red"`, `"blue"`, `"green"`, `"black"`, `"orange"`, and `"purple"`.

A hex color such as `"#1f77b4"` specifies a color using hexadecimal RGB values. Choose colors that make different series easy to distinguish.

### 7.4 Line styles

| Value | Appearance |
|---|---|
| `"-"` | Solid line |
| `"--"` | Dashed line |
| `"-."` | Dash-dot line |
| `":"` | Dotted line |

Example:

```python
ax.plot(x, y, linestyle=":")
```

### 7.5 Marker styles

Markers show the locations of data points.

| Marker | Meaning |
|---|---|
| `"o"` | Circle |
| `"s"` | Square |
| `"^"` | Upward triangle |
| `"v"` | Downward triangle |
| `"*"` | Star |
| `"x"` | X mark |
| `"+"` | Plus sign |
| `"D"` | Diamond |
| `"."` | Small dot marker |
| `","` | Pixel-sized marker, useful for dense point sets |

Example:

```python
ax.plot(x, y, marker="s", markersize=7)
```

### 7.6 Transparency using `alpha`

`alpha` accepts a value from 0 to 1:

- `0` means fully transparent.
- `0.5` means half-transparent.
- `1` means fully opaque.

Example:

```python
ax.plot(x, y, color="blue", alpha=0.5)
```

Transparency can help when many points or lines overlap.

### 7.7 Shorthand format strings

Matplotlib allows a compact format string in `plot()` that combines a color, line style, and marker.

```python
ax.plot(x, y, "r--o")
```

This means:
- `r` = red
- `--` = dashed line
- `o` = circle marker

More examples:

| Format string | Meaning |
|---|---|
| `"b-o"` | Blue solid line with circle markers |
| `"r--s"` | Red dashed line with square markers |
| `"g-.^"` | Green dash-dot line with upward triangle markers |
| `"k:o"` | Black dotted line with circle markers |

You can write the same formatting with named parameters, which is often easier to read:

```python
ax.plot(x, y, color="red", linestyle="--", marker="o")
```

**Note:** A format string is a convenience, not a requirement. Named parameters are clearer when several styling options are used.

---

## 8. Titles, labels, legends, grids, limits, and ticks

### 8.1 Title and axis labels

Titles and labels tell the reader what the graph represents and what each axis measures.

```python
ax.set_title("Monthly Sales", fontsize=16, fontweight="bold")
ax.set_xlabel("Month", fontsize=12)
ax.set_ylabel("Sales (units)", fontsize=12)
```

- `fontsize` controls text size.
- `fontweight="bold"` makes the title bold.
- Include units in labels when useful, such as `"Temperature (°C)"`.

Pyplot equivalents are `plt.title()`, `plt.xlabel()`, and `plt.ylabel()`.

### 8.2 Legends

A legend explains which line or data series corresponds to each label.

```python
ax.plot(x, x ** 2, label="Square")
ax.plot(x, x ** 3, label="Cube")
ax.legend()
```

The `label` argument names each series. Calling `ax.legend()` displays the names.

Some useful legend settings:

```python
ax.legend(loc="upper left", fontsize=10, title="Functions")
```

- `loc` chooses the legend location.
- `fontsize` controls text size.
- `title` adds a title to the legend.

### 8.3 Grid lines

A grid helps the reader estimate values from the axes.

```python
ax.grid(True)
```

To make the grid less prominent:

```python
ax.grid(True, linestyle="--", alpha=0.4)
```

- `linestyle="--"` gives dashed grid lines.
- `alpha=0.4` makes them partially transparent.

### 8.4 Axis limits

Limits set the visible range on an axis.

```python
ax.set_xlim(0, 10)
ax.set_ylim(0, 100)
```

This displays X values from 0 to 10 and Y values from 0 to 100. Set limits only when they help explain the data; overly tight limits can make differences look misleading.

### 8.5 Ticks and tick labels

Ticks are the marked positions along an axis. Tick labels are the numbers or words displayed at those positions.

```python
ax.set_xticks([0, 2, 4, 6, 8, 10])
ax.set_yticks([0, 20, 40, 60, 80, 100])
```

You can set category labels when the positions are numerical:

```python
ax.set_xticks([1, 2, 3])
ax.set_xticklabels(["Jan", "Feb", "Mar"])
```

For category data, plotting category names directly (for example, `ax.bar(["Jan", "Feb", "Mar"], values)`) is often simpler.

Change tick label appearance:

```python
ax.tick_params(axis="x", labelrotation=45, labelsize=10)
```

- `axis="x"` applies to the X-axis ticks.
- `labelrotation=45` rotates the tick labels.
- `labelsize=10` sets their font size.

### 8.6 Style title and label colors

```python
ax.set_title("Performance", color="darkblue", fontsize=16)
ax.set_xlabel("Week", color="darkgreen")
ax.set_ylabel("Score", color="darkred")
```

Make styling choices that improve readability rather than adding decoration that competes with the data.

---

## 9. Plot multiple data series on one Axes

You can draw multiple lines on the same Axes by calling `ax.plot()` more than once.

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 5, 100)

fig, ax = plt.subplots(figsize=(8, 5))

ax.plot(x, x ** 2, color="blue", label="y = x²")
ax.plot(x, x ** 3, color="red", linestyle="--", label="y = x³")

ax.set_title("Comparing Two Functions")
ax.set_xlabel("X")
ax.set_ylabel("Y")
ax.grid(True, alpha=0.3)
ax.legend()

fig.tight_layout()
plt.show()
```

Both lines share the same axes. Use distinct colors or line styles and give each series a clear label so readers can tell them apart.

---

## 10. Organize plots with subplots

Subplots place multiple plotting areas inside one Figure. They are useful when you want to compare different variables or plot types together.

```python
import matplotlib.pyplot as plt

months = ["Jan", "Feb", "Mar", "Apr"]
sales = [20, 25, 18, 30]
expenses = [12, 15, 14, 20]

fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot(months, sales, marker="o", color="blue")
axes[0].set_title("Sales")
axes[0].set_ylabel("Units")

axes[1].bar(months, expenses, color="orange")
axes[1].set_title("Expenses")
axes[1].set_ylabel("Units")

fig.tight_layout()
plt.show()
```

How it works:
1. `plt.subplots(1, 2)` creates one row and two Axes.
2. `axes[0]` refers to the left Axes.
3. `axes[1]` refers to the right Axes.
4. You customize each Axes independently.
5. `fig.tight_layout()` helps separate the graphs and their labels.

Use `plt.subplots(2, 2)` to create a 2-by-2 set of Axes. In that case `axes` is a two-dimensional array, so refer to an Axes using `axes[row, column]`, such as `axes[0, 1]`.

---

## 11. Figure size, layout, displaying, and saving

### 11.1 Figure size

```python
fig, ax = plt.subplots(figsize=(10, 6))
```

`figsize=(10, 6)` means 10 inches wide and 6 inches high. A larger figure can provide more space for labels and multiple plots.

### 11.2 Improve layout

```python
fig.tight_layout()
```

This adjusts spacing around subplots so labels and titles are less likely to overlap.

You can also ask Matplotlib to use a constrained layout when creating the Figure:

```python
fig, axes = plt.subplots(2, 2, figsize=(10, 7), layout="constrained")
```

Use one layout strategy at a time unless you know why both are needed.

### 11.3 Display a plot

```python
plt.show()
```

In ordinary Python scripts, this opens/displays the figure using the available plotting backend. In Jupyter notebooks, plots may also be displayed automatically after a cell runs, but `plt.show()` is still useful in examples and scripts.

### 11.4 Save a plot to a file

Pyplot style:

```python
plt.savefig("my_plot.png", dpi=300, bbox_inches="tight")
```

OO style:

```python
fig.savefig("my_plot.png", dpi=300, bbox_inches="tight")
```

- `"my_plot.png"` is the output filename.
- `dpi=300` sets the output resolution.
- `bbox_inches="tight"` trims excess whitespace around the figure.

A reliable habit is to save before calling `plt.show()`:

```python
fig.savefig("my_plot.png", dpi=300, bbox_inches="tight")
plt.show()
```

---

## 12. Detailed styling reference

This section gathers frequently used styling options in one place.

| Property or method | Example | Purpose |
|---|---|---|
| `color` | `color="navy"` | Line or element color |
| `linewidth` | `linewidth=2.5` | Line thickness |
| `linestyle` | `linestyle=":"` | Line pattern |
| `marker` | `marker="o"` | Data point symbol |
| `markersize` | `markersize=7` | Size of markers |
| `markerfacecolor` | `markerfacecolor="white"` | Fill color for markers |
| `markeredgecolor` | `markeredgecolor="black"` | Marker outline color |
| `markeredgewidth` | `markeredgewidth=1` | Marker outline thickness |
| `alpha` | `alpha=0.7` | Transparency |
| `label` | `label="Model A"` | Label for the legend |
| `zorder` | `zorder=5` | Layer drawing order |
| `fontsize` | `fontsize=14` | Text size |
| `fontweight` | `fontweight="bold"` | Text weight |
| `rotation` / `labelrotation` | `labelrotation=45` | Rotate tick labels |
| `grid()` | `ax.grid(True)` | Show or hide grid |
| `legend()` | `ax.legend()` | Display labels for plotted series |
| `set_xlim()` | `ax.set_xlim(0, 10)` | Set visible X range |
| `set_ylim()` | `ax.set_ylim(0, 100)` | Set visible Y range |
| `tick_params()` | `ax.tick_params(labelsize=10)` | Customize tick marks and labels |
| `set_facecolor()` | `ax.set_facecolor("whitesmoke")` | Set Axes background color |
| `set_axisbelow()` | `ax.set_axisbelow(True)` | Place grid and ticks below plotted data |
| `set_title()` | `ax.set_title("Title")` | Set title |
| `set_xlabel()` | `ax.set_xlabel("X label")` | Set X-axis label |
| `set_ylabel()` | `ax.set_ylabel("Y label")` | Set Y-axis label |

### Full styling example

```python
import numpy as np
import matplotlib.pyplot as plt

x = np.linspace(0, 10, 20)
y = np.sin(x)

fig, ax = plt.subplots(figsize=(9, 5))

ax.plot(
    x, y,
    color="teal",
    linewidth=2.5,
    linestyle="-.",
    marker="o",
    markersize=5,
    markerfacecolor="white",
    markeredgecolor="teal",
    markeredgewidth=1.2,
    alpha=0.9,
    label="sin(x)"
)

ax.set_title("A Styled Line Plot", fontsize=16, fontweight="bold")
ax.set_xlabel("X values", fontsize=12)
ax.set_ylabel("sin(x)", fontsize=12)
ax.set_xlim(0, 10)
ax.grid(True, linestyle="--", alpha=0.35)
ax.legend(loc="best")
ax.set_axisbelow(True)

fig.tight_layout()
plt.show()
```

This example demonstrates styling a line, its markers, text, grid, and legend. The exact color is optional; the goal is a graph that is clear and easy to read.

---

## 13. Method reference tables

### 13.1 Main plotting methods

| Method | What it draws | Typical call |
|---|---|---|
| `ax.plot()` | Line plot | `ax.plot(x, y)` |
| `ax.scatter()` | Scatter plot | `ax.scatter(x, y)` |
| `ax.hist()` | Histogram | `ax.hist(data, bins=10)` |
| `ax.bar()` | Vertical bar chart | `ax.bar(categories, values)` |
| `ax.barh()` | Horizontal bar chart | `ax.barh(categories, values)` |
| `ax.boxplot()` | Box plot | `ax.boxplot(data)` |

### 13.2 Figure and Axes methods

| Method | Purpose |
|---|---|
| `plt.subplots()` | Create a Figure and one or more Axes |
| `plt.figure()` | Create a Figure |
| `fig.add_axes()` | Create an Axes at a specified position |
| `ax.set_title()` | Set Axes title |
| `ax.set_xlabel()` | Set X-axis label |
| `ax.set_ylabel()` | Set Y-axis label |
| `ax.set_xlim()` | Set X-axis limits |
| `ax.set_ylim()` | Set Y-axis limits |
| `ax.set_xticks()` | Choose X tick positions |
| `ax.set_yticks()` | Choose Y tick positions |
| `ax.tick_params()` | Adjust tick appearance |
| `ax.set_position()` | Adjust Axes placement |
| `ax.grid()` | Control grid lines |
| `ax.legend()` | Display legend |
| `fig.tight_layout()` | Improve subplot spacing |
| `fig.savefig()` | Save the Figure |
| `plt.show()` | Display plots |

---

## 14. Useful shortcuts and shorthand

### 14.1 Plot-format shorthand

A short string can combine a color, line style, and marker.

| Shorthand | Explanation |
|---|---|
| `"r-o"` | Red line with circle markers |
| `"b--s"` | Blue dashed line with square markers |
| `"g-."` | Green dash-dot line |
| `"k:"` | Black dotted line |
| `"m^"` | Magenta upward-triangle markers; no line style is specified |

These are shortcuts only. You can always use named parameters such as `color="red"` and `marker="o"` for readability.

### 14.2 Frequently used code patterns

| Goal | Code |
|---|---|
| Create one graph | `fig, ax = plt.subplots()` |
| Make a wider Figure | `fig, ax = plt.subplots(figsize=(10, 5))` |
| Create a 1-row, 2-column layout | `fig, axes = plt.subplots(1, 2)` |
| Plot and label a line | `ax.plot(x, y, label="Series A")` |
| Show legend | `ax.legend()` |
| Add a light grid | `ax.grid(True, alpha=0.3)` |
| Improve spacing | `fig.tight_layout()` |
| Save a high-resolution plot | `fig.savefig("plot.png", dpi=300, bbox_inches="tight")` |
| Show the plot | `plt.show()` |

### 14.3 Common Jupyter Notebook keyboard shortcuts

These are common shortcuts in the classic Jupyter Notebook interface. Shortcuts may differ in other editors or interfaces.

| Shortcut | Action |
|---|---|
| `Shift + Enter` | Run the current cell and move to the next cell |
| `Ctrl + Enter` | Run the current cell and remain on it |
| `Esc` then `A` | Insert a cell above, in command mode |
| `Esc` then `B` | Insert a cell below, in command mode |
| `Esc` then `D` twice | Delete the selected cell, in command mode |
| `Ctrl + S` | Save the notebook |

---

## 15. Common beginner mistakes

### Mistake 1: X and Y lengths do not match

Incorrect:

```python
x = [1, 2, 3, 4]
y = [10, 20, 30]
ax.plot(x, y)
```

There are four X values but only three Y values. For ordinary paired plotting, provide matching lengths.

### Mistake 2: Forgetting to call the legend

```python
ax.plot(x, y, label="Measurements")
ax.legend()
```

Setting `label` names the series, but `ax.legend()` is needed to display the legend.

### Mistake 3: Mixing up `fig` and `ax`

- Use `ax.plot()` to draw a series on an Axes.
- Use `ax.set_title()` to configure that Axes' title.
- Use `fig.savefig()` to save the complete Figure.

### Mistake 4: Confusing `figsize` with pixels

```python
fig, ax = plt.subplots(figsize=(10, 5))
```

This means 10 by 5 inches, not 10 by 5 pixels. The saved pixel dimensions also depend on the output resolution (DPI).

### Mistake 5: Using a histogram when you need category comparisons

- Use a **histogram** to examine the distribution of numerical values.
- Use a **bar chart** to compare known categories such as subjects, products, or departments.

### Mistake 6: Expecting random data to stay the same every run

`sample()` can produce different selections each time. This is normal. For repeatable random experiments, use a seeded random-number generator, such as NumPy's `np.random.default_rng(seed)`.

### Mistake 7: Calling the wrong title or label method in OO code

For OO code, use:

```python
ax.set_title("My Title")
ax.set_xlabel("X")
ax.set_ylabel("Y")
```

For Pyplot code, use:

```python
plt.title("My Title")
plt.xlabel("X")
plt.ylabel("Y")
```

Both styles work, but use the methods belonging to the approach you're writing.

---

## 16. Mini practice tasks

Try these without looking up a full solution. Use the OO approach unless a task asks for something else.

### Task 1 — Basic line plot

Data:

```python
x = [1, 2, 3, 4, 5]
y = [4, 7, 5, 9, 12]
```

Create a line plot with a title, X and Y labels, and a grid.

### Task 2 — Style a line

Use:

```python
x = [1, 2, 3, 4, 5]
y = [3, 6, 4, 8, 10]
```

Make the line red, dashed, width 2.5, with square markers. Add a legend.

### Task 3 — Create a curve

Use `np.linspace(0, 5, 100)` for X. Calculate `y = x ** 2` and draw a smooth line. Set an informative title and labels.

### Task 4 — Histogram

Use:

```python
from random import sample
data = sample(range(1, 501), 80)
```

Create a histogram with 10 bins. Label the axes so they explain value range and frequency.

### Task 5 — Bar chart

Use:

```python
subjects = ["Math", "Python", "Science", "English"]
marks = [88, 95, 76, 84]
```

Compare marks across subjects. Add a title and axis labels.

### Task 6 — Two subplots

Create a 1-by-2 subplot layout. Plot `y = x ** 2` on the first Axes and `y = x ** 3` on the second. Give both plots their own titles.

### Task 7 — Manual Axes positioning

Create a Figure with `figsize=(8, 5)`. Use `fig.add_axes([0.15, 0.15, 0.7, 0.7])` to add an Axes and plot a simple line.

### Task 8 — Save a plot

Take any previous plot, improve the layout, and save it as `practice_plot.png` with `dpi=300`.

---

## 17. Final quick revision sheet

| Concept | Remember |
|---|---|
| `plt` | The Pyplot interface |
| `fig` | The whole Figure/canvas |
| `ax` | One plotting area (Axes) |
| `plt.subplots()` | Creates a Figure and Axes |
| `fig.add_axes()` | Adds an Axes at a custom position |
| `figsize` | Figure dimensions in inches |
| `np.linspace()` | Creates evenly spaced numerical values |
| `range()` | Represents integers up to but excluding the stop |
| `sample()` | Randomly selects unique items |
| `plot()` | Draws a line plot |
| `scatter()` | Draws separate data points |
| `hist()` | Shows a numerical distribution |
| `bar()` | Compares categories |
| `boxplot()` | Summarizes distribution and spread |
| `color` | Controls color |
| `linewidth` | Controls line thickness |
| `linestyle` | Controls solid, dashed, dash-dot, or dotted style |
| `marker` | Adds a symbol at each point |
| `markersize` | Controls marker size |
| `alpha` | Controls transparency |
| `label` + `legend()` | Names and displays plotted series |
| `set_xlim()` / `set_ylim()` | Set the visible axis ranges |
| `tight_layout()` | Helps prevent overlap between plot elements |
| `savefig()` | Saves the plot to a file |
| `show()` | Displays the plot |

**Recommended workflow:** Create data → create `fig, ax` → plot the data → add titles and labels → style the plot → add grid/legend if useful → adjust layout → save if needed → display the plot.

The goal is not to use every styling option. The goal is to make the data easy to understand.
