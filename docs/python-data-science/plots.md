# Plots

## Seaborn vs matplotlib

Seaborn is a visualization library based on maltplotlib. It provides a high-level interface for drawing attractive statistical graphics.

Matplotlib is a basic plotting library for Python.

## Histograms

```python
import seaborn as sns

sns.histplot(data=filtered, x="age", bins=20, hue="is.employed.fixed", multiple="dodge")
# hue is set based on employment status
# multiple="dodge" makes it so that employed/unemployed counts for a given age are separated into two bars beside each other
plt.title("Age Distribution by Employment Status")
plt.xlabel("Age")
plt.ylabel("Count")
plt.show()
```

## Global styles and themes

```python
# You can switch styles to mimic ggplot's theming variety.
# whitegrid is a style with a white background and gridlines
# darkgrid is a style with a dark background and gridlines
# ticks is a style with ticks on all sides of the plot
sns.set_theme(style="white", context="notebook")  # try: "white", "darkgrid"
# This following line sets the default figure DPI (dots per inch)
# 120 is a good default for most screens
plt.rcParams["figure.dpi"] = 120
```

## Formatting axis numbers (ticks)

```python

from matplotlib.ticker import FuncFormatter
dollar = FuncFormatter(lambda x, _: f"${x:,.0f}")
plt.gca().xaxis.set_major_formatter(dollar)
```

## Basic scatterplot

```python
sns.scatterplot(data=df, x="x_col", y="y_col")
plt.show()
```

## Adding color to a scatterplot

```python

sns.scatterplot(data=df, x="x", y="y", hue="category", palette="viridis", s=50)
```

## Controlling bins and binwidth w/ histograms

```python
sns.histplot(data=df, x="age", bins=30, edgecolor="white")
sns.histplot(data=df, x="age", binwidth=10, edgecolor="white")
```

## log-scaled axes

Better handlke skewed data with log transformation and log-spaced bins.

```python
plt.xscale("log")
bins = 10 ** np.arange(np.log10(df["income"].min()), np.log10(df["income"].max()), 0.1)
sns.histplot(data=df, x="income", bins=bins)
```

## Density plots (kernel density estimates)

```python
sns.kdeplot(data=df, x="income", bw_method="scott", fill=True)
```

## Bar charts

```python
sns.countplot(data=df, x="category")       # vertical
sns.countplot(data=df, y="category")       # horizontal
```

## Adjust font size for long labels

Good for when categories have many entries.

```python
ax = sns.countplot(data=df, y="category")
ax.set_yticklabels(ax.get_yticklabels(), fontsize=6)
```

## Split-apply-combine

Aggregate numeric data by categories.

```python
df.groupby("category", dropna=False)["value"].mean().reset_index()
```

## Barplot of aggregated values

```python
sns.barplot(data=summary_df, x="category", y="value", palette="viridis")
```

## Scatter plot with transparency / alpha

```python
sns.scatterplot(data=df, x="x", y="y", alpha=0.7, s=30)
```

## 2D histograms

```python
sns.histplot(data=df, x="x", y="y", bins=30, cbar=True)
```

## Hexbin plot

Hexagonal bins for dense scatter data.

```python
plt.hexbin(df["x"], df["y"], gridsize=30, cmap="viridis", mincnt=1)
plt.colorbar(label="count")
```

## Categorical vs continuous (jitter)

Avoid overplotting with random noise on categorical axis.

```python
sns.stripplot(data=df, x="continuous", y="category", jitter=0.2, size=3, alpha=0.6)
```

## Stacked / proportional bar charts

Show proportions of subcategories within each main category.

```python
sns.histplot(data=df, x="cat1", hue="cat2", multiple="fill", shrink=0.9)
```

## rotate axis labels

Improve readability of long categorical names.

```python
plt.xticks(rotation=15)
```