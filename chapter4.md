---
title         : Data wrangling
description   : Introduces split-apply-combine
free_preview  : true

--- type:NormalExercise lang:r xp:100 skills:1 key:1b4b89b117
## Casting data
In addition to making plots, R has tools to help you prepare tabular views of your data. This task can
be viewed as a two-part process: first, selecting (aka subsetting) the data points that you want to present,
and then arranging that data into the rows and columns that you need.

We have already seen how to use the `subset()` function to filter data.
Let’s subset the LDLR data from the E1909 experiment.

```
subset(ablation, Measurement == "LDLR-ABLATION" & Experiment == "E1909")
```

To reshape this list of data points into a dataframe where there is one row per time point and one column per cell type, we can use the `dcast()` function from the `reshape2` package (this package is installed with `ggplot2` but must be loaded to use the functions).

```
library(reshape2)
dcast(subset(ablation,
             Measurement == "LDLR-ABLATION" & Experiment == "E1909"),
       Time ~ CellType,
       value.var = "Score")
```

Note  that  all  of  the  experimentally  measured  values  in  this  table  come  from  the  original Score column; this is indicated by the `value.var` option in the above command.
The values in the Time column, and the column names, are referred to as identifying variables.
In other words, if you are looking up a specific experimentally measured value, you would need to specify
the identifying variables (Time and CellType) in order to find it.

*** =instructions

When using `dcast()`, the factors on the RHS of the tilde will be the rows, and the factors on the LHS will be the columns. 
You can specify more than one identifying variable on either side of the tilde.

Subset the E1909 experiment data from the `ablation` dataset, and assign it to a variable called `e1909`.
Reshape this data such that you have one row per unique combination of Measurement and Time, and one column per CellType.

Note that if you can also use more than one identifier in the column attribute, the column names are amalgamations of the originating identifiers.


*** =hint
Make sure you use a `==` to indicate the Experiment you want to subset.
Combine factors on either side of the tilde with `+`.


*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)

library(reshape2)
```

*** =sample_code
```{r}
# Assign a new variable called e1909 that contains only the data from the E1909 Experiment from the ablation dataset


# Reshape e1909 so that each row contains a unique combination of Measurement and Time, and there is one column per CellType



```

*** =solution
```{r}
# Assign a new variable called e1909 that contains only the data from the E1909 Experiment from the ablation dataset
e1909 <- subset(ablation, Experiment == "E1909")


# Reshape e1909 so that each row contains a unique combination of Measurement and Time, and there is one column per CellType
dcast(e1909, Measurement + Time ~ CellType, value.var = "Score")


```

*** =sct
```{r}
test_object("e1909",
             undefined_msg = "Make sure you assign the result from the subset command to `e1909`.",
             incorrect_msg = "Did you use the correct selection expression (`Experiment == 'E1909'`) to subset the `ablation` dataframe.")
test_function("subset", args = c("x"),
              not_called_msg = "Use `subset()` to extract subsets of data from a data frame.",
              args_not_specified_msg = "Have you specified the dataframe to be subsetted?",
              incorrect_msg = "Have you passed in the correct arguments (`ablation`, `Experiment == 'E1909'`) to the `subset()` function?")
test_function("dcast", args = c("data", "formula", "value.var"),
              not_called_msg = "Use `dcast()` to reshape the contents of `e1909`.",
              args_not_specified_msg = "Have you specified the dataframe to be reshaped?",
              incorrect_msg = "Have you passed in the correct arguments (`e1909, formula = Measurement + Time ~ CellType, value.var = 'Score'`) to the `dcast()` function?")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:e3140062cf
## Melting data
The format of the ablation dataset that we have been working with is long and skinny.
The hallmark of this canonical (melted) format is that there is only one (set of) independently observed value(s)  in each row.
All  of  the  other  columns  are  identifying  values (or metadata).
They  explain  what  exactly  was measured.
_When your data is in this format, it is straightfoward to subset, transform, and aggregate it by any combination of factors of the identifying variables._
That is why, for example, the `ggplot` package requires that your data is in melted format.

The `melt()` function is used to convert a data frame with several measurement columns into a data frame in this canonical format, which has one row for every observed (measured) value.
Let’s melt data frame about states, with eight observations per row.

```
state.stats <- data.frame(Name = rownames(state.x77), state.x77)
state.m <- melt(state.stats, id.vars = "Name")
```
You need to tell `melt()` which of your variables are identifying variables (`id.vars`), and which are measured variables (`measure.vars`).
If  you  only  supply  one  of `id.vars` or `measure.vars`, `melt()` will  assume  the  remainder  of  the
variables in the data set belong to the other. If you supply neither, `melt()` will assume factor and
character variables are id variables, and all others are measured.

By default, the name of the measurement variables will be put into a column called "variable", and
their associated values will be put into a column called "value", but these can be changed by using the arguments
`variable.name` (or `varnames` for matrices) and `value.name`.


*** =instructions
The dataframe containing multiple observations about each US state has been given to you.
Melt this dataset so that each unique combination of state and measurement is on a row.
Subset out only the Population measurements and assign to a variable called `pop`.
Plot this data as a scatter plot, with state names along the x-axis and population sizes along the y-axis. 


*** =hint

Use `str()` to look at the structure of your data, both before and after melting.


*** =pre_exercise_code
```{r}
state.stats <- data.frame(Name=rownames(state.x77), state.x77)

library(ggplot2)
library(reshape2)
```

*** =sample_code
```{r}
# Create a data frame of multiple observations about US states
state.stats <- data.frame(Name=rownames(state.x77), state.x77)

# Melt this dataset and assign to a variable called state.m


# Subset this to include only the Population dataset, assign this to a variable called pop


# Plot this data as a scatter plot, with state names along the x-axis and population sizes along the y-axis



```

*** =solution
```{r}
# Create a data frame of multiple observations about US states
state.stats <- data.frame(Name=rownames(state.x77), state.x77)

# Melt this dataset and assign to a variable called state.m
state.m <- melt(state.stats, id.vars="Name")

# Subset this to include only the Population dataset, assign this to a variable called pop
pop <- subset(state.m, variable == "Population")

# Plot this data as a scatter plot, with state names along the x-axis and population sizes along the y-axis
ggplot(pop, aes(x = Name, y = value)) + geom_point()

```

*** =sct
```{r}
test_predefined_objects("state.stats")
test_object("state.m",
             undefined_msg = "Make sure you assign the result from the melt command to `state.m`.",
             incorrect_msg = "Did you use the correct selection expression (`id.vars='Name'`) to subset the `state.stats` dataframe.")
test_function("melt", args = c("data"),
              not_called_msg = "Use `melt()` to create one row for each combination of state and observation type.",
              args_not_specified_msg = "Have you specified both the dataframe to be subsetted, and the `id.vars`?",
              incorrect_msg = "Have you passed in the correct arguments (`state.stats, id.vars='Name'`) to the `melt()` function?")
test_object("pop",
             undefined_msg = "Make sure you assign the result from the subset command to `pop`.",
             incorrect_msg = "Did you use the correct selection expression (`variable == 'Population'`) to subset the `state.m` dataframe.")
test_function("subset", args = c("x"),
              not_called_msg = "Use `subset()` to extract subsets of data from a data frame.",
              args_not_specified_msg = "Have you specified the dataframe to be subsetted?",
              incorrect_msg = "Have you passed in the correct arguments (`state.m, variable == 'Population'`) to the `subset()` function?")
test_function("ggplot", args = c("data", "mapping"),
              not_called_msg = "Use `ggplot()` to reshape the contents of `e1909`.",
              args_not_specified_msg = "Have you specified the dataframe to be drawn?",
              incorrect_msg = "Have you passed in the correct arguments (`pop, aes(x = Name, y = value)`) to the `ggplot()` function?")
test_function("geom_point", 
              not_called_msg = "Use `geom_point()` to draw a scatterplot.")
test_error()
```

--- type:NormalExercise lang:r xp:100 skills:1 key:7381066a82
## Merging data
It is usually a good idea to keep all of your data from a particular study or project in a very small number of canonical "skinny" data frames. That way, when new experiments  are  performed,  you  can  add  new  rows  to  the dataset  with  the `rbind()` function. 

Sometimes, you will want to add new metadata columns.
For example, if you wanted to add technician data to each experiment, you can create a new data
frame with this information.

```
experiment.log <- data.frame(Experiment=c("E1909", "E1915", "E1921"), Tech=c("Jason", "Luce", "Jason"), stringsAsFactors=TRUE)
```

If you wanted to look at technician-specific bias, for example, you can merge the technician data with your main data using the `merge()` function.

```
merge(ablation, experiment.log)
```

The `merge()` function merges two data frames based on common column values. By default, it looks
for common column names, but these can be specified explicitly. By default, only rows which have
elements common to both data frames will be kept, but you can change this behavior (see `?merge`).

The merged data frame contains redundant information; i.e., if you know the Experiment, you know
the Tech (we say the data is "denormalized"). While the merged data frame may be convenient when
investigating  "tech  effects",  you  probably  don’t  want  to  store  this  data  frame  permanently.  This
becomes  more  important  at  scale,  when  the  cost  of  storing  the  redundant  information  becomes  a
limiting factor (usually in terms of the memory needed by R).

*** =instructions
The technician data has been created for you in a variable called experiment.log.
Merge this with the ablation dataset into a variable called `abl.exp`.
Plot the data as a scatterplot and color by technician.


*** =hint
Map Tech to color using an `aes()` function.



*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)

library(ggplot2)
library(reshape2)
```

*** =sample_code
```{r}
# Technician data about each experiment
experiment.log <- data.frame(Experiment=c("E1909", "E1915", "E1921"), Tech=c("Jason", "Luce", "Jason"), stringsAsFactors=TRUE)

# Merge this technician data with the ablation data frame, call it abl.exp


# Plot this data as a scatterplot and color by technician



```

*** =solution
```{r}
# Technician data about each experiment
experiment.log <- data.frame(Experiment=c("E1909", "E1915", "E1921"), Tech=c("Jason", "Luce", "Jason"), stringsAsFactors=TRUE)

# Merge this technician data with the ablation data frame, call it abl.exp
abl.exp <- merge(ablation, experiment.log)

# Plot this data as a scatterplot and color by technician
ggplot(abl.exp, aes(x = Time, y = Score)) + geom_point(aes(color = Tech))

```

*** =sct
```{r}
test_predefined_objects("experiment.log")
test_object("abl.exp",
             undefined_msg = "Make sure you assign the result from the merge command to `abl.exp`.",
             incorrect_msg = "Did you merge the correct data frames (`ablation, experiment.log`)?")
test_function("merge", args = c("x", "y"),
              not_called_msg = "Use `merge()` to merge two data frames.",
              args_not_specified_msg = "Have you specified both dataframes to be merged?",
              incorrect_msg = "Have you passed in the correct arguments (`ablation, experiment.log`) to the `merge()` function?")
test_function("ggplot", args = c("data", "mapping"),
              not_called_msg = "Use `ggplot()` to reshape the contents of `e1909`.",
              args_not_specified_msg = "Have you specified the dataframe to be drawn?",
              incorrect_msg = "Have you passed in the correct arguments (`abl.exp, aes(x = Time, y = Score)`) to the `ggplot()` function?")
test_function("geom_point", 
              not_called_msg = "Use `geom_point()` to draw a scatterplot.")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:78ced58e43
## Data aggregation
When we used `dcast()` earlier, we were rearranging the raw data.
In other words, every value in the cast data frame could be found in the original data frame.
The `dcast()` function can also be used to summarize your data (also known as "data aggregation"), by using a new parameter `fun.aggregate`.
For example, we may want to compute the mean Score for each combination of Measurement, Time, and CellType (i.e., averaging across experiments).

```
# Show all raw data in a table
dcast(ablation, Experiment + Time + Measurement ~ CellType, value.var="Score")
# Average across experiments
dcast(ablation,
      Time + Measurement ~ CellType,
      value.var="Score",
      fun.aggregate=mean)
```

You  can  pass  any  function  that  takes  a  vector  and  returns  a  single  value  as  an  aggregation  func-
tion; `dcast()` will  call  this  function  for  each  unique  combination  of  levels  of  the  factors  that  you
specify in the formula.
Here we compute the number of observations for each unique combination of Measurement, CellType and Experiment (the `length()` function is the default aggregation function).

```
dcast(ablation,
      Measurement + CellType ~ Experiment,
      value.var="Score",
      fun.aggregate=length)
```


*** =instructions
Summarize how many times each kind of Measurement was made for each of the two cells types. Get the maximum values of each of those Measurements. You'll notice that R issues an odd warning about non-missing arguments to `max()`when you do this. This is because `dcast()` will always call your aggregation function once with an empty vector (to figure out what to put in the result table if there are no cases for a particular combination of levels). To get rid of this error message, you can explicitly state what value should be used for missing cases (e.g., `fill=-Inf`).

*** =hint



*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)

library(ggplot2)
library(reshape2)
```

*** =sample_code
```{r}
# Summarize how many times each kind of Measurement was made for each of the two cells types


# Get the maximum values of each of those Measurements.

```

*** =solution
```{r}
# Summarize how many times each kind of Measurement was made for each of the two cells types
dcast(ablation, 
      CellType ~ Measurement,
      value.var="Score",
      fun.aggregate=length)

# Get the maximum values of each of those Measurements.
dcast(ablation, 
      CellType ~ Measurement,
      value.var="Score",
      fun.aggregate=max)

```

*** =sct
```{r}
test_function("dcast", args = c("data", "formula", "value.var", "fun.aggregate"), index = 1,
              not_called_msg = "Use `dcast()` to summarize the ablation data frame.",
              args_not_specified_msg = "Have you specified all the arguments (data frame, formula, value.var, fun.aggregate)",
              incorrect_msg = "Have you passed in the correct arguments to the `dcast()` function?")
test_function("dcast", args = c("data", "formula", "value.var", "fun.aggregate"), index = 2,
              not_called_msg = "Use `dcast()` to summarize the ablation data frame.",
              args_not_specified_msg = "Have you specified all the arguments (data frame, formula, value.var, fun.aggregate)?",
              incorrect_msg = "Have you passed in the correct arguments to the `dcast()` function?")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:fe7e5696f2
## Summarizing data
A useful housekeeping function, that is part of another Hadley Wickham package (`plyr`) is `summarize()`.
The general form of `summarize()` is:

```
summarize(df, new.col.name = some.function)
```

where the first argument to is a data frame, and subsequent arguments are functions that will be called in the context of the data frame.
The result of is a new data frame where each column is the result of one of the functions you supplied (the name of the column will be the argument name you gave to the function).

To get the max and min Scores from the ablation data frame, we can use:

```
summarize(ablation, the.max=max(Score), the.min=min(Score))
```

The ability to do this will become useful in the next section.
*** =instructions

Create a new data frame called e1909.min.max containing the min and max Score for the E1909 Experiment.
Do the same for the E1915 Experiment.


*** =hint
Use `subset(ablation, Experiment == "E1909")` to extract data from the E1909 Experiment only.


*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)

library(ggplot2)
library(reshape2)
library(plyr)
```

*** =sample_code
```{r}
# Create a new data frame called e1909.min.max containing the min and max Score for the E1909 Experiment


# Create a new data frame called e1915.min.max containing the min and max Score for the E1915 Experiment

```

*** =solution
```{r}
# Create a new data frame called e1909.min.max containing the min and max Score for the E1909 Experiment
e1909.min.max <- summarize(subset(ablation, Experiment == "E1909"), the.min = min(Score), the.max = max(Score))

# Create a new data frame called e1915.min.max containing the min and max Score for the E1915 Experiment
e1915.min.max <- summarize(subset(ablation, Experiment == "E1915"), the.min = min(Score), the.max = max(Score))


```

*** =sct
```{r}
test_object("e1909.min.max",
             undefined_msg = "Make sure you assign the result from the summarize command to `e1909.min.max`.",
             incorrect_msg = "Did you subset the ablation data to only include data from Experiment E1909, and calculate the min and the max?")
test_object("e1915.min.max",
             undefined_msg = "Make sure you assign the result from the summarize command to `e1915.min.max`.",
             incorrect_msg = "Did you subset the ablation data to only include data from Experiment E1915, and calculate the min and the max?")
test_error()
```
--- type:NormalExercise lang:r xp:100 skills:1 key:0c4e4f3199
## Plyr: "Split, apply, combine"
What `dcast()` is actually doing is _splitting_ your data into groups (by sets of factors), _applying_  some  function  on  each  group  and  then  _combining_  the  results  into  a  set  with  one  entry  per group. However, as we saw, the aggregation function for `dcast()` must return a single value. What if you want to compute a range (max and min) for each combination of levels?

The `plyr` package allows us to do just that.
The plyr package contains a family of functions that implement the split, apply, combine approach in a flexible but consistent  manner.
The plyr functions can work with any data structure as input, and can output any data structure.
The general form of the plyr functions are `xyply()`, where _x_ and _y_ are one-letter
abbreviations of the different data structures (a: array, matrix or vector; l: list; d: data frame).

We can find the range of Scores for each combination of Measurement, CellType and Time, using the
`ddply()` function.

```
ddply(ablation,
      ~ Measurement + CellType + Time,
      summarize,
      the.max=max(Score), the.min=min(Score))
```

We use the `ddply()` function because our input is the ablation data frame, and we want the result to
be a data frame.
The second argument specifies the factors that we will split by.
The third argument gives the function to be applied to each group thus split.
The fourth and additional arguments are passed to this applied function.

*** =instructions


*** =hint



*** =pre_exercise_code
```{r}
ablation <- read.csv("http://s3.amazonaws.com/assets.datacamp.com/production/course_2921/datasets/ablation.csv", header = TRUE, stringsAsFactors = TRUE)

library(ggplot2)
library(reshape2)
library(plyr)
```

*** =sample_code
```{r}

```

*** =solution
```{r}

```

*** =sct
```{r}
test_error()
```