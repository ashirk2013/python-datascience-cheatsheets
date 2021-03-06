# Introduction to Seaborn

## Introduction to Seaborn

### What is Seaborn

- Python data visualization library
- Easily create the most common types of plots
- Useful for the "explore" and "communicate results" phases of typical data flow

### Advantages of Seaborn

- Easy to use
- Works well with **pandas** data structures
- Built on top of **matplotlib**

### Getting started

```
import seaborn as sns
import matplotlib.pyplot as plt
```

- **S**amuel **N**orman **S**eaborn (sns)
  - "The West Wing" television show

### Example 1: Scatter plot

```
import seaborn as sns
import matplotlib.pyplot as plt
height = [62, 64, 78, ...]
weight = [120, 136, 148, ...]
sns.scatterplot(x=height, y=weight)
plt.show()
```

### Example 2: Create a count plot

```
import seaborn as sns
import matplotlib.pyplot as plt
gender = ["Female", "Female", "Male", ...]
sns.countplot(x=gender)
plt.show()
```

- This shows a bar plot with the counts of list entries for each category

## Using pandas with Seaborn

### Using DataFrames with countplot()

```
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns

df = pd.read_csv("masculinity.csv")
sns.countplot(x="how_masculine", data=df)
plt.show()
```

- The kwarg = x is the name of the column to display or count
- The kwarg = data points to the dataframe

### Tidy data

- DataFrames used with seaborn must be tidy
- This means the data is complete, valid and consistent
- Reach row is a complete observation
- Each column has data and of same data types

## Adding a third variable with hue

### Tips dataset

- Comes built-in with seaborn

```
import pandas as pd
import seaborn as sns
tips = sns.load_dataset("tips")
print(tips.head())
```

### A scatter plot with hue

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.scatterplot(x="total_bill",
                y="tip",
                data=tips,
                hue="smoker")

plt.show()
```

- The kwarg = hue is the column name to add to the chart using color
- This encodes the third variable using color
- Seaborn automatically adds a legend for the third variable

### Setting hue order

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.scatterplot(x="total_bill",
                y="tip",
                data=tips,
                hue="smoker",
                hue_order=["Yes", "No"])

plt.show()
```

- The kwarg = hue_order adjusts the color order and legend order

### Specifying hue colors

```
import matplotlib.pyplot as plt
import seaborn as sns

hue_colors - {"Yes": "black", "No": "red"}

sns.scatterplot(x="total_bill",
                y="tip",
                data=tips,
                hue="smoker",
                palette=hue_colors)

plt.show()
```

- Here color names are based on the color names available in matplotlib
- You can also use matplotlib colors specified by single character, i.e. "blue" = "b"
- Can also use html hex codes

### Using HTML hex color codes with hue

```
import matplotlib.pyplot as plt
import seaborn as sns

hue_colors - {"Yes": "#808080", "No": "#00FF00"}

sns.scatterplot(x="total_bill",
                y="tip",
                data=tips,
                hue="smoker",
                palette=hue_colors)

plt.show()
```

### Using hue with countplots

```
import matplotlib.pyplot as plt
import seaborn as sns

hue_colors - {"Yes": "#808080", "No": "#00FF00"}

sns.countplot(x="smoker",
              data=tips,
              hue="sex")

plt.show()
```

# Visualizing Two Quantitative Variables

## Introduction to relational plots and subplots

### Questions about quantitative variables

- We often want to understand the relationship between two quantitative variables
- Seaborn calls this kind of chart a "relational" chart
  - Height vs Weight
  - Number of school absences vs final grade
  - GDP vs percent literate

### Introducing relplot()

- Create "relational plots": scatter or line plots

Why use **relplot()** instead of **scatterplot()** ?

- **relplot()** lets you create subplots in a single figure

### scatterplot() vs relplot()

Using **scatterplot()**

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.scatterplot(x="total_bill", y="tip",
                data=tips)
plt.show()
```

Using **relplot()**

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter")
plt.show()
```

### Subplots in columns

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                col="smoker")
plt.show()
```

- Here the subplots will be based on the "smoker" column values, organized as columns

### Subplots in rows

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                row="smoker")
plt.show()
```

### Subplots in rows and columns

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                col="smoker", row="time")
plt.show()
```

### Wrapping columns

- Can use this if there are too many subplots on a row

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                col="smoker", col_wrap=2)
plt.show()
```

- Here there are two subplots per row

### Ordering columns

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                col="smoker", col_wrap=2,
                col_order=["Yes", "No"])
plt.show()
```

- You can also use **row_order** to organize the row value order

## Customizing scatter plots

- Customizations looked at here
  - Subgroups with point size and style
  - Changing point transparency

### Subgroups with point size

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                size="size")
plt.show()
```

- Here **size** points to the size variable, representing the size of the group or party

### Point size and hue

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                size="size", hue="size")
plt.show()
```

### Subgroups with point style

```
import seaborn as sns
import matplotlib.pyplot as plt

sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                hue="smoker", style="smoker")
plt.show()
```

- Point style will vary by the value of the smoker variable

### Changing point transparency

```
import seaborn as sns
import matplotlib.pyplot as plt

# set alpha between 0 and 1
sns.relplot(x="total_bill", y="tip",
                data=tips, kind="scatter",
                alpha=0.4)
plt.show()
```

- Here, darker areas of the chart will indicate more observations

## Introduction to line plots

### What are line plots?

- Seaborn offers two types of relational plots: line and scatter
- Scatter plots:
  - Each plot point is an independent observation
- Line plots:

  - Each plot point represents the same "thing", typically tracked over time

- This chapter used air pollution data as a sample

### Scatter plot

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2_mean",
            data=air_df_mean, kind="scatter")

plt.show()
```

### Line plot

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2_mean",
            data=air_df_mean, kind="line")

plt.show()
```

### Subgroups by location

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2_mean",
            data=air_df_loc_mean,
            kind="line",
            style="location",
            hue="location")

plt.show()
```

- Produces multiple lines that vary by style and color, and has a legend

### Adding markers

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2_mean",
            data=air_df_loc_mean,
            kind="line",
            style="location",
            hue="location",
            markers=True)

plt.show()
```

- The kwarg = **markers** puts a mark for each data point
- The line marker style will vary by the style parameter (dot, square, x, etc)

## Turning off line style

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2_mean",
            data=air_df_loc_mean,
            kind="line",
            style="location",
            hue="location",
            markers=True,
            dashes=False)

plt.show()
```

- The kwarg = **dashes** as false, allows you to keep the markers but turn off the line style

### Multiple observations per x-value

#### Scatter plot

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2",
            data=air_df,
            kind="scatter")

plt.show()
```

- If the df has multiple observations / x-value, then each observation will be shown in the scatter plot

#### Line plot

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2",
            data=air_df,
            kind="line")

plt.show()
```

- By default seaborn will aggregate the measurement as the mean, and show it as a line
- Also shows a shaded region that represents the 95% confidence interval for the mean
  - Assumes the dataset is a random sample
  - 95% confident that the mean is within the interval
  - Indicates uncertainty in our estimate

### Replacing confidence interval with standard deviation

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2",
            data=air_df,
            kind="line",
            ci="sd")

plt.show()
```

- Shows the spread of the distribution of observations at each x value

### Turning off confidence interval

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.relplot(x="hour", y="NO_2",
            data=air_df,
            kind="line",
            ci=None)

plt.show()
```

# Visualizing a Categorical and a Quantitative Varaible

## Count plots and bar plots

### Categorical plots

- Examples: count plots, bar plots
- Involve a categorical value
- Comparisons between groups

### catplot()

- Used to create categorical plots
- Same advantages of **relplots()**
- Easily create subplots with row= and col=

### countplot() vs catplot()

#### countplot()

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.countplot(x="how_masculine", data=masculinity_data)
plt.show()
```

#### catplot()

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="how_masculine",
            data=masculinity_data,
            kind="count")
plt.show()
```

### Changing the order

```
import matplotlib.pyplot as plt
import seaborn as sns

category_order = ["No answer", "Not at all",
                  "Not very", "Somewhat", "Very"]

sns.catplot(x="how_masculine",
            data=masculinity_data,
            kind="count",
            order=category_order)
plt.show()
```

### Bar plots

- Display the mean of a quantitative variable per category

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="day",
            y="total_bill",
            data=tips,
            kind="bar")
plt.show()
```

- By default the Seaborn bar plot will show 95% confidence interval

### Confidence intervals

- Lines show 95% confidence intervals for the mean
- Shows uncertainty about out estimate
- Assumes our data is a random sample

### Turning off confidence intervals

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="day",
            y="total_bill",
            data=tips,
            kind="bar",
            ci=None)
plt.show()
```

### Changing the orientation

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="total_bill",
            y="day",
            data=tips,
            kind="bar")
plt.show()
```

- Flip the x and y values to change the orientation
- While this can work, it's pretty standard to see the categorical value on the x axis

## Box plots

### What is a box plot?

- Shows the distribution of quantitative data
- See median, spread, skewness, and outliers
- Facilitates comparisons between groups

### How to create a box plot

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="time",
            y="total_bill",
            data=tips,
            kind="box")
plt.show()
```

- Draws a box plot
- Colored box represents the 25% - 75% percentile, or IQR
- Line in the middle of the box represents the median
- Whisters give a sense of the spread of the data
- Dots represent the outliers

### Change the order of categories

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="time",
            y="total_bill",
            data=tips,
            kind="box",
            order=["Dinner", "Lunch"])
plt.show()
```

### Omitting the outliers using 'sym'

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="time",
            y="total_bill",
            data=tips,
            kind="box",
            sym="")
plt.show()
```

- Here the **sym** arg has an empty string

### Changing the whiskers using 'whis'

- By default the whiskers extend to 1.5 \* the interquartile range (IQR)
- Make them extend to 2.0 \* IQR: `whis=2.0`
- Show the 5th and 95th percentiles: `whis=[5, 95]`
- Show min and max values: `whis=[0, 100]`

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="time",
            y="total_bill",
            data=tips,
            kind="box",
            whis=[0, 100])
plt.show()
```

## Point plots

### What are point plots?

- Points show the mean of a quantitative variable
- Vertical lines show the 95% confidence interval of the mean

### Point plots vs line plots

Both show:

- Mean of quantitative variable
- 95% confidence interval of the mean

Differences:

- Line plot has a quantitative variable (usually time) on the x-axis
- Point plot has a categorical variable on the x-axis

### Point plots vs bar plots

Both show:

- Mean of quantitative variable
- 95% confidence interval of the mean

### Creating a point plot

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="age",
            y="masculinity_important",
            data=masculinity_data,
            hue="feel_masculine",
            kind="point")

plt.show()
```

### Disconnecting the points

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="age",
            y="masculinity_important",
            data=masculinity_data,
            hue="feel_masculine",
            kind="point",
            join=False)

plt.show()
```

### Displaying the median

```
import matplotlib.pyplot as plt
import seaborn as sns
from numpy import median

sns.catplot(x="age",
            y="masculinity_important",
            data=masculinity_data,
            hue="feel_masculine",
            kind="point",
            estimator=median)

plt.show()
```

### Customizing the confidence intervals

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="age",
            y="masculinity_important",
            data=masculinity_data,
            hue="feel_masculine",
            kind="point",
            capsize=0.2)

plt.show()
```

### Turning off confidence intervals

```
import matplotlib.pyplot as plt
import seaborn as sns

sns.catplot(x="age",
            y="masculinity_important",
            data=masculinity_data,
            hue="feel_masculine",
            kind="point",
            ci=None)

plt.show()
```

# Customizing Seaborn Plots

## Customizing plot style and color

### Why customize?

- Personal preference
- Improve readability
- Guide interpretation

### Changing the figure style

- Figure "style" includes background and axes
- Preset options: "white", "dark", "whitegrid", "darkgrid", "ticks"
- `sns.set_style()`
- Default style is "white"

### Changing the palette

- Figure "palette" changes the color of the main elements of the plot
- `sns.set_palette()`
- Use preset palettes or create a custom palette

### Diverging palettes

- Good to use for scales where the two ends are opposite with a nuetral mid-point
- "RdBu"
- "PRGn"
- "RdBu_r"
- "PRGn_r"

### Sequential palettes

- Great for emphasizing a variable on a continuous scale
- "Greys"
- "Blues"
- "PuRd"
- "GnBu"

### Custom palette

```
custom_palette = ["red", "orange", "yellow", "green", "blue", "indigo", "violet"]

sns.set_palette(custom_palette)
```

- Can also use color hex codes as well

### Changing the scale

- Figure "context" changes the scale of the plot elements and labels
- `sns.set_context()`
- Smallest to largest: "paper", "notebook", "talk", "poster"

## Adding title and labels: Part 1

### FacetGrid vs AxesSubplot objects

- Seaborn plots create two different types of objects: `FacetGrid` and `AxesSubplot`
- Can tell which type capturing the object in a variable and using the type() function

```
g = sns.scatterplot(x="height", y="weight", data=df)
type(g)
```

- The **scatterplot()** function returns: `matplotlib.axes._subplots.AxesSubplot`

### An empty FacetGrid

- A FacetGrid object can have multiple subplots
- Seaborn functions like `catplot()` and `relplot()` return FacetGrid objects

### FacetGrid vs. AxesSubplot objects

| Object Type | Plot Types                          | Characteristics            |
| ----------- | ----------------------------------- | -------------------------- |
| FacetGrid   | `relplot()`, `catplot()`            | Can create subplots        |
| AxesSubplot | `scatterplot()`, `countplot()`, etc | Only creates a single plot |

### Adding a title to FacetGrid

```
g = sns.catplot(x="Region",
                y="Birthrate",
                data=gdp_data,
                kind="box")
g.fig.suptitle("New Title")
plt.show()
```

### Adjusting height of title in FacetGrid

```
g = sns.catplot(x="Region",
                y="Birthrate",
                data=gdp_data,
                kind="box")

g.fig.suptitle("New Title",
              y=1.03)
plt.show()
```

## Adding titles and labels: Part 2

### Adding a title to AxesSubplot

#### FacetGrid

```
g = sns.catplot(x="Region",
                y="Birthrate",
                data=gdp_data,
                kind="box")

g.fig.suptitle("New Title",
              y=1.03)
plt.show()
```

### AxesSubplot

```
g = sns.boxplot(x="Region",
                y="Birthrate",
                data=gdp_data)

g.set_title("New Title",
              y=1.03)
plt.show()
```

### Titles for subplots

```
g = sns.catplot(x="Region",
                y="Birthrate",
                data=gdp_data,
                kind="box",
                col="Group")

g.fig.suptitle("New Title",
              y=1.03)

g.set_titles("This is {col_name}")

plt.show()
```

- The `g.fig.suptitle()` adds the title to the entire figure
- The `g.set_titles()` adds a title to each subolot
- You can specify the column name using the variable `col_name`

### Adding axis labels

```
g = sns.catplot(x="Region",
                y="Birthrate",
                data=gdp_data,
                kind="box")

g.set(xlabel="New X Label", ylabel="New Y Label")

plt.show()
```

### Rotating x-axis tick labels

```
g = sns.catplot(x="Region",
                y="Birthrate",
                data=gdp_data,
                kind="box")

plt.xticks(rotation=90)
plt.show()
```

- xticks are set by calling the `xticks()` method on matplotlib directly

## Putting it all together

### Getting started

To import Seaborn:

```
import seaborn as sns
```

To import matplotlib:

```
import matplotlib.pyplot as plt
```

To show a plot:

```
plt.show()
```

### Relational plots

- Show the relationship between two quantitative variables
- Examples: scatter plots, line plots

```
sns.relplot(x="x_variable_name",
            y="y_variable_name",
            data=pandas_df,
            kind="scatter")
```

### Categorical plots

- Show the distribution of a quantitative variable within categories defined by a categorical variable
- Examples: bar plots, count plots, box plots, point plots

```
sns.catplot(x="x_variable_name",
            y="y_variable_name",
            data=pandas_df,
            kind="bar")
```

### Adding a third variable (hue)

Setting `hue` will create subgroups that are displayed as different colors on a single plot.

### Adding a third variable (row/col)

Setting `row` and/or `col` in `relplot()` or `catplot()` will create subgroups that are displayed on separate subplots.

### Customization

- Change the background: `sns.set_style()`
- Change the main element colors: `sns.set_palette()`
- Change the scale: `sns.set_context()`

### Adding a title

| Object Type | Plot Types                          | Characteristics    |
| ----------- | ----------------------------------- | ------------------ |
| FacetGrid   | `relplot()`, `catplot()`            | `g.fig.suptitle()` |
| AxesSubplot | `scatterplot()`, `countplot()`, etc | `g.set_title()`    |

### Final touches

Add x- and y-axis labels:

```
g.set(xlabel="new x-axis label",
      ylabel="new y-axis label")
```

Rotate x-tick labels:

```
plt.xticks(rotation=90)
```
