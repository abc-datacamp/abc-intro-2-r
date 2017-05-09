---
title         : Plotting
description   : Introduces the ggplot2 package
free_preview  : true

--- type:NormalExercise lang:r xp:100 skills:1 key:1b4b89b117
## Introduction to ggplot
Although R has some basic plotting functionality which we have seen hints of, the ggplot2 package is
more comprehensive and consistent.

There are many ways to install a package. The main three are: from CRAN, using `install.packages(packagename)`; from Bioconductor, using `biocLite(packagename)`, and from GitHub, using 

```
install.packages("devtools")
devtools::install_github("username/packagename")
```

After installing a package, to load a library into an R session, use `library()`.

ggplot2 relies entirely on data frames for input. At a minimum, the two things that you need to give `ggplot()` are:<br/>
a. The dataset (which must be a data frame), and the variable(s) you want to plot<br/>
b. The type of plot you want to make.

Aesthetics are used to bind plotting parameters to your data. Thus

```
ggplot(ablation, aes(x = Time, y = Score)) + geom_point()
```

will take the data from the ablation data frame, plotting the Time column on the x-axis versus the Score column on the y-axis. The `geom_point()` layer indicates that we wish to plot a scatter plot.

```
ggplot(ablation, aes(x = Time, y = Score)) + geom_point(color = "red", size = 4)
```


*** =instructions

A data frame called `ablation` has been uploaded for you.
Use ggplot to plot the data, with the Time column along the x-axis and the Score column along the y-axis.
Modify the points, changing the color to red, and the size to 4.


*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)
library(ggplot2)
```

*** =sample_code
```{r}

# Create a scatter plot with the ablation data


# Change the color of the points to be red and of size 4


```

*** =solution
```{r}
# Create a scatter plot with the ablation data
ggplot(ablation, aes(x = Time, y = Score)) + geom_point()

# Change the color of the points to be red and of size 4
ggplot(ablation, aes(x = Time, y = Score)) + geom_point(color = "red", size = 4)

```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"), index = 1,
              not_called_msg = "Use `ggplot()` to plot the `ablation` dataset.",
              args_not_specified_msg = "Have you specified all the arguments to the `ggplot()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`ablation, aes(x = Time, y = Score)`) to the `ggplot()` function?")
test_function("geom_point", index = 1,
              not_called_msg = "Use `geom_point()` to plot a scatterplot. Use `+` to add the geom_point layer.")
test_function("ggplot", args = c("data", "mapping"), index = 2,
              not_called_msg = "Use `ggplot()` to plot the `ablation` dataset.",
              args_not_specified_msg = "Have you specified all the arguments to the `ggplot()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`ablation, aes(x = Time, y = Score)`) to the `ggplot()` function?")
test_function("geom_point", args = c("color", "size"), index = 2,
              not_called_msg = "Use `geom_point()` to plot a scatterplot. Use `+` to add the geom_point layer.",
              args_not_specified_msg = "Have you specified all the arguments to the `geom_point()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`color = 'red', size = 4`) to the `geom_point()` function?")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:299af8f62d
## Layers
Layers are added to the ggplot object with `+`, just as we saw before, using `+ geom_point()` to add the scatterplot layer.
The aesthetics that are used to bind plotting parameters to your data can be specific to each layer. Thus, 

```
g <- ggplot(ablation, aes(x = Time, y = Score))
```

creates a base ggplot object called `g`, binding the x and y axes.

```
g <- g + geom_point(aes(color = Experiment), size = 4)
```

adds a scatterplot layer to the `g` object, with its own binding of the color aesthetic. In addition to `x`, `y`, `color`, other aesthetics include: shape, size, linetype, fill, alpha, group.

Any bindings defined in the base ggplot object are inherited by all layers (but can be overridden by any individual layer's aesthetic).

It is sometimes useful to save off the base ggplot object and add layers in separate commands. The
plot is only rendered when it is called with `print()`. This is useful for several reasons:<br/>
a. We don't need to create one big huge command to create a plot, we can create it piecemeal.<br/>
b. The plot will not get rendered until it has received all of its information, and therefore allows
ggplot2 to be more intelligent than R's built-in plotting commands when deciding how large a
plot should be, what the best scale is, etc.


*** =instructions

The ablation data frame has been loaded for you.

A p object has been given to you. Add a layer to the p object, binding color to Experiment and shape to Measurement. Add another layer to the p object, using a geom\_line layer, and binding color to Experiment, linetype to CellType and group to `interaction(Experiment, Measurement, CellType)`. Run this `interaction` command in the console to understand what it does (you'll have to include the data frame name: `interaction(ablation$Experiment, ablation$Measurement, ablation$CellType)`). This composite factor is passed to the group aesthetic of geom\_line() to inform ggplot which data values go together.


*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)
library(ggplot2)
```

*** =sample_code
```{r}
# A base ggplot object of the ablation dataset
p <- ggplot(ablation, aes(x = Time, y = Score))

# Add another layer to the p object, binding color to Experiment and shape to Measurement, making the size of the points = 4


# Add another layer to the p object, using a geom_line layer, and binding color to Experiment, linetype to CellType and group to interaction(Experiment, Measurement, CellType)


# Print the plot


```

*** =solution
```{r}
# A base ggplot object of the ablation dataset
p <- ggplot(ablation, aes(x = Time, y = Score))

# Add another layer to the p object, binding color to Experiment and shape to Measurement
p <- p + geom_point(aes(color = Experiment, shape = Measurement), size = 4)

# Add another layer to the p object, using a geom_line layer, and binding color to Experiment, linetype to CellType and group to interaction(Experiment, Measurement, CellType)
p <- p + geom_line(aes(group = interaction(Experiment, Measurement, CellType),
color = Experiment,
linetype = CellType))

# Print the plot
print(p)


```

*** =sct
```{r}
test_function("ggplot", args = c("data", "mapping"),
              not_called_msg = "Use `ggplot()` to plot the `ablation` dataset.",
              args_not_specified_msg = "Have you specified all the arguments to the `ggplot()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`ablation, aes(x = Time, y = Score)`) to the `ggplot()` function?")
test_function("geom_point", args = c("mapping", "size"),
              not_called_msg = "Use `geom_point()` to plot a scatterplot. Use `+` to add the geom_point layer.",
              args_not_specified_msg = "Have you specified all the arguments to the `geom_point()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`aes(color = Experiment, shape = Measurement), size = 4`) to the `geom_point()` function?")
test_function("geom_line", args = c("mapping"),
              not_called_msg = "Use `geom_line()` to add lines to the plot. Use `+` to add the geom_line layer.",
              args_not_specified_msg = "Have you specified all the arguments to the `geom_line()` function?",
              incorrect_msg = "Have you passed in the correct mapping aesthetics (`aes(group = interaction(Experiment, Measurement, CellType), color = Experiment, linetype = CellType`) to the `geom_line()` function?")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:831c68539b
## Legends and scales
Some layers don't plot data, but affect the plot in other ways. For example, there are layers that
control plot labeling and plot theme. The `labs()` function can also modify legend labels.

```
p <- p + labs(title = "Ablation", x = "Time (minutes)", y = "% Saturation")
p <- p + theme_bw()
```

ggplot gives you control over the scales of your plot. There is one scale for each binding. In the plot
we just made, there are five scales that we can manipulate: the x and y axes and the three legends.
Let's change our x-axis to include the 5 minute timepoint. This is achieved with yet another layer.

```
p + scale_x_continuous(breaks = c(0, 5, 10, 20, 30))
```

We can also manipulate legends with scale layers. Here we provide the labels for the Measurement scale (remember that we used an aesthetic to bind
shape to Measurement). Note that ggplot will always order the labels according to the levels of the
underlying factor, so the labels should be provided in that order. If you want to change the order in
which the legend elements are displayed, change the underlying factor.
We have also changed the title of the CellType legend (the linetype binding) to be two words and
used a different color palette (for the binding to Experiment).

```
p <- p + scale_shape_discrete(labels = c("LDLR", "TfR")) +
         scale_linetype_discrete(name = "Cell type") +
         scale_color_brewer(palette = "Set1")
```

Note the general form of the scale layer functions:
scale\_aestype\_colortype
where the aestype is the bound aesthetic, and the colortype is the type of color associated with that
binding. Common values for the colortype include:


               | Color type
 ------------- | ------------
 hue           | Equally-spaced colors from the color wheel
 manual        | Manually-specified values (e.g., colors, point shapes, line types)
 gradient      | Color gradients
 grey          | Shades of grey
 discrete      | Discrete values (e.g., colors, point shapes, line types, point sizes)
 continuous    | Continuous values (e.g., alpha, colors, point sizes)


*** =instructions
The ggplot object `p` has already been defined for you.
Change the name of the CellType legend (the linetype binding) to "Cell Type".
Read the documentation for `scale_color_manual()` and change the colors for E1909, E1915 and E1921 to be purple, orange and green, respectively.


*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)
library(ggplot2)
p <- ggplot(ablation, aes(x = Time, y = Score))
p <- p + geom_point(aes(color = Experiment, shape = Measurement), size = 4)
p <- p + geom_line(aes(group = interaction(Experiment, Measurement, CellType),
color = Experiment,
linetype = CellType))
```

*** =hint
Use ?scale_color_manual to learn how to set new color values.


*** =sample_code
```{r}
# Use a scale layer to change the name of the CellType legend (the linetype binding) to "Cell type".


# Use scale_color_manual() to change the colors of the experiments to purple, orange and green

```

*** =solution
```{r}
# Use a scale layer to change the name of the CellType legend (the linetype binding) to "Cell type".
p + scale_linetype_discrete(name = "Cell type")

# Use scale_color_manual() to change the colors of the experiments to purple, orange and green
p + scale_color_manual(values = c("purple", "orange", "green"))
```

*** =sct
```{r}
test_function("scale_linetype_discrete", args = c("name"),
              not_called_msg = "Use `scale_linetype_discrete()` to change the attributes of the linetype aesthetic.",
              args_not_specified_msg = "Have you specified an argument to the `scale_linetype_discrete()` function?",
              incorrect_msg = "Have you passed in the correct argument and value (`name = 'Cell type'`) to the `scale_linetype_discrete()` function?")
test_function("scale_color_manual", args = c("values"),
              not_called_msg = "Use `scale_color_manual()` to change the colors of the aesthetic associated with Experiment.",
              args_not_specified_msg = "Have you specified an argument to the `scale_color_manual()` function?",
              incorrect_msg = "Have you passed in the correct argument and values (`values = c('purple', 'orange', 'green')`) to the `scale_color_manual()` function?")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:05b0d38908
## Faceting
This plot is probably showing too much data at once. One approach to resolve this would be to make
separate plots for the LDLR and TfR measurements. You can make multiple plots at once using
`facet_grid()`. 

```
p + facet_grid(Measurement ~ .)
```

will make a separate figure for each Measurement.
`facet_grid()` takes as its first argument a formula indicating the rows that will be shown on the LHS and the columns on the RHS.

In these plots, you can remove the color and shape legends entirely (an option that can be specified
in each of the respective legend layers):
`p + scale_colour_discrete(guide = "none") + scale_shape_discrete(guide = "none")`
or you may no longer want to bind the Measurement and Experiment variables to shape and color at all.
The `facet_wrap()` function can be used to wrap a 1D ribbon of plots into a 2D layout.

*** =instructions
The ggplot object `p` has already been defined for you.
Use `facet_grid()` to make separate figures for each Measurement, and each Experiment. Experiment with switching each of these factors on either side of the `~`.

*** =hint
`facet_wrap()` needs a factor on the RHS of the tilde.

*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)
library(ggplot2)
p <- ggplot(ablation, aes(x = Time, y = Score))
p <- p + geom_point(aes(color = Experiment, shape = Measurement), size = 4)
p <- p + geom_line(aes(group = interaction(Experiment, Measurement, CellType),
color = Experiment,
linetype = CellType))
```

*** =sample_code
```{r}
# Facet the ablation figure by Experiment (rows) and Measurement (columns)


# Facet the ablation figure by Measurement (rows) and Experiment (columns)


# Use facet_wrap() to wrap plots by Experiment

```

*** =solution
```{r}
# Facet the ablation figure by Experiment (rows) and Measurement (columns)
p + facet_grid(Experiment ~ Measurement)

# Facet the ablation figure by Measurement (rows) and Experiment (columns)
p + facet_grid(Measurement ~ Experiment)

# Use facet_wrap() to wrap plots by Experiment
p + facet_wrap( ~ Experiment)

```

*** =sct
```{r}
test_function("facet_grid", args = c("facets"), index = 1,
              not_called_msg = "Use `facet_grid()` to make separate plots for every combination of Experiment and Measurement.",
              args_not_specified_msg = "Have you specified the facets to be displayed?",
              incorrect_msg = "Have you passed in the correct facets (`Experiment ~ Measurement`) to the `facet_grid()` function?")
test_function("facet_grid", args = c("facets"), index = 2,
              not_called_msg = "Use `facet_grid()` to make separate plots for every combination of Measurement and Experiment.",
              args_not_specified_msg = "Have you specified the facets to be displayed?",
              incorrect_msg = "Have you passed in the correct facets (`Measurement ~ Experiment`) to the `facet_grid()` function?")
test_function("facet_wrap", args = c("facets"),
              not_called_msg = "Use `facet_wrap()` to make a separate plot for every Experiment.",
              args_not_specified_msg = "Have you specified the facets to be displayed?",
              incorrect_msg = "Have you passed in the correct facets (` ~ Experiment`) to the `facet_grid()` function?")
test_error()
```
