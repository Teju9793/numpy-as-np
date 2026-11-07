# 07 — Figure, Axes and Subplots in Matplotlib

> **Goal:** Understand Matplotlib's object model and build layouts containing multiple plots.

## 1. Figure versus Axes versus Axis

These names sound similar but mean different things:
- **Figure:** the entire canvas.
- **Axes:** one plotting area that can contain data, labels, title and legend.
- **Axis:** the x-axis or y-axis scale, ticks and tick labels.

A single Figure can contain many Axes.

## 2. Create one Figure and one Axes

```python
import matplotlib.pyplot as plt

fig, ax = plt.subplots()
ax.plot([1, 2, 3], [10, 20, 15])
ax.set_title("Simple Plot")
plt.show()
```

`plt.subplots()` returns a Figure and an Axes object. The Axes is where most plot customization happens.

## 3. Create a 1-by-2 subplot layout

```python
fig, axes = plt.subplots(1, 2, figsize=(10, 4))

axes[0].plot([1, 2, 3], [2, 4, 3])
axes[0].set_title("Line Plot")

axes[1].bar(["A", "B", "C"], [5, 3, 7])
axes[1].set_title("Bar Plot")

fig.tight_layout()
plt.show()
```

The first argument is number of rows; the second is number of columns. With a 1-by-2 layout, `axes` is a one-dimensional array of two Axes objects.

## 4. Create a 2-by-2 layout

```python
fig, axes = plt.subplots(2, 2, figsize=(9, 7))

axes[0, 0].plot([1, 2, 3], [2, 4, 3])
axes[0, 1].scatter([1, 2, 3], [3, 2, 5])
axes[1, 0].bar(["A", "B"], [4, 7])
axes[1, 1].hist([1, 2, 2, 3, 3, 3, 4])

fig.tight_layout()
plt.show()
```

For a 2-D layout, use `axes[row, column]`.

## 5. Share axes

```python
fig, axes = plt.subplots(1, 2, sharey=True)
```

Sharing an axis can make comparisons fairer because the plots use the same scale. Use it when the same units and range are meaningful across panels.

## 6. Figure-level and Axes-level titles

```python
fig, axes = plt.subplots(1, 2)
fig.suptitle("Student Performance")
axes[0].set_title("Math")
axes[1].set_title("Science")
```

The Figure title describes the whole layout; each Axes title describes its own chart.

## 7. Layout spacing

- `fig.tight_layout()`: automatically adjusts spacing to reduce overlap.
- `constrained_layout=True` in `plt.subplots`: another layout engine that can manage spacing.

```python
fig, axes = plt.subplots(2, 2, constrained_layout=True)
```

Do not combine layout engines unnecessarily. Check the result after adding long labels or legends.

## 8. Save the full figure

```python
fig.savefig("dashboard.png", dpi=300, bbox_inches="tight")
```

Call save on the Figure object to export the entire multi-plot layout.

## 9. Common mistakes

- Confusing the Axes object with the x/y Axis.
- Indexing a 1-D axes array as if it were 2-D.
- Forgetting to set a title or labels for each subplot.
- Overlapping titles and tick labels.
- Saving only one plot instead of the complete Figure.

## 10. Practice

Create a 2-by-2 dashboard for a student dataset: histogram of marks, bar chart of department counts, scatter plot of study hours versus marks, and box plot by department. Add a figure-level title and ensure labels do not overlap.

**Checkpoint:** Understand that a Figure is the canvas and each Axes is an individual plotting area.
