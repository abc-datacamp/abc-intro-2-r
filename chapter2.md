---
title         : Data Structures
description   : Introduces the different types of data structures
free_preview  : true

--- type:MultipleChoiceExercise lang:r xp:50 skills:3 key:5cf9077e2a
## Overview

R has several different types of data structures and knowing what each is used for and when they are appropriate is fundamental to the efficient use of R. The ones that we are going to examine in detail here are: vectors, matrices, lists and data frames.

A quick summary of the four main data structures:

Vectors are ordered collections of elements, where each of the objects must be of the same data type or mode, but can be any mode.

A matrix is a rectangular array, having some number of columns and some number of rows. Matrices can only comprise one data type (if you want multiple data types in a single structure, use a data frame).

Lists are like vectors, but whereas elements in vectors must all be of the same type, a single list can include elements from any data type. One of the nice things about lists is that elements can be named. A common use of lists is to combine multiple values into a single variable that can then be passed to, or returned by, a function.

Data frames are similar to matrices, in that they can have multiple rows and multiple columns, but in a data frame, each of the columns can be of a different data type, although within a column, all elements must be of the same data type. You can think of a data frame as being like a list, but instead of each element in the list being just one value, each element corresponds to a complete vector.

Which data structures can mix data types?


*** =instructions
 - vectors and matrices
 - vectors and lists
 - matrices and data frames
 - lists and data frames

*** =sct
```{r}
msg1 = "No. All the data in both vectors and matrices must be of the same type. Try again."
msg2 = "No. All the data in a vector must be of the same type. Try again."
msg3 = "No. All the data in a matrix must be of the same type. Try again."
msg4 = "That is correct! A list or a data frame can include elements from different data types."
test_mc(correct = 4, 
        feedback_msgs = c(msg1, msg2, msg3, msg4))

```
--- type:NormalExercise lang:r xp:50 skills:1 key:a1e7552548
## Data frames

Data frames are two-dimensional data structures like matrices, but, unlike matrices, they can contain multiple different data types. You can think of a data frame as a list of vectors, where all the vector lengths are the same. Data frames are commonly used to represent tabular data.


*** =instructions

When we were learning about vectors, we used several parallel vectors, each with length 50 to represent information about US states. The collection of vectors really belongs together, and a data frame is the tool for doing this. The `data.frame()` function combines the four data sets into a single data frame. Note that the first three data sets are vectors (two character, one numeric), but the last data set is a list with two components.

Note the `stringsAsFactors = FALSE` argument. Some of the vectors that we are using are character vectors, but will be automatically converted to factors if this option is not set. Since we will want to work with our character data as vectors, not as factors, we want to set this argument to `FALSE`.

Data frames have a split personality. They behave both like a tagged list of vectors, and like a matrix! This gives you many options for accessing elements. Fortunately, you know them all already!



*** =sample_code
```{r}
# Combine different data about US states into a single data frame
state.db <- data.frame(state.name, state.abb, state.area, state.center, stringsAsFactors = FALSE)

# Access the state abbreviations column using list notation. Convince yourself that state.db$state.abb, state.db[[ "state.abb" ]] and state.db[[ 2 ]] all give the same result.


```

*** =solution
```{r}
# Combine different data about US states into a single data frame
state.db <- data.frame(state.name, state.abb, state.area, state.center, stringsAsFactors = FALSE)

# Access the state abbreviations column using list notation. Convince yourself that state.db$state.abb, state.db[[ "state.abb" ]] and state.db[[ 2 ]] all give the same result.
state.db$state.abb

```

*** =hint
You can access a column in a data frame using list notation. `state.db$state.abb`, `state.db[[ "state.abb" ]]` and `state.db[[ 2 ]]` all work!


*** =sct
```{r}
test_predefined_objects("state.db")
test_output_contains("state.db$state.abb",
                         incorrect_msg = "Check your syntax when printing out the state abbreviations column?")
test_error()
```