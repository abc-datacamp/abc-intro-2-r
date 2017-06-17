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