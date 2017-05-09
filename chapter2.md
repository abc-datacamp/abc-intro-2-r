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

--- type:NormalExercise lang:r xp:50 skills:1 key:53cc697297
## Getting started with vectors

Many commands in R take vectors as input, e.g., `sum(x)`, `max(x)`, `summary(x)`.

There are many ways of creating vectors. The most common way is using the `c()` function, where `c` stands for `concatention`. We can create a vector of character strings, for example, using 
`colors <- c("red", "orange", "yellow", "green", "blue", "indigo", "violet")`. 
Note that character strings must be quoted.

The `c()` function can also combine vectors. 
`colors <- c("infrared", colors, "ultraviolet")`
By assigning the result back to the `colors` variable, we are updating its value.
The net effect is to both prepend and append new colors to the original `colors`
vector. Remember that "infrared" is a one-element vector!

Sequential numeric vectors can be created using the `:` operator. `1:4` generates a numeric vector of the numbers 1 through 4.

In addition to using the `:` notation to create vectors of sequential numbers, there are a handful of
useful functions for generating vectors with systematically created elements. Here we will look at `seq()` and `rep()`.

`seq(1, 10)` gives the same result as `1:10`, but seq() allows us to be more fine-grained: 
`seq(1, 4, 0.5)` shows all numbers from 1 to 4, incrementing by 0.5 each time.

Another commonly used function for making regular vectors is `rep()`. This repeats the values in the
argument vector as many times as specified. This can be used with character and logical vectors as
well as numeric.
`rep(colors, 2)` will return a new vector where the entire `colors` vector is repeated twice.

In many cases, R will implicitly 'recycle' vector elements as needed to get operations on vectors to
make sense. When vector operations align, results are as you would expect:

`x <- 0:9`

`y <- seq(from = 0, to = 90, by = 10)`

`x + y`

Here, the first element of x has the first element of y added to it, the second element of x has the
second element of y added to it, etc. What happens, though, when the vectors are not the same
length?
`(1:5) + y`
Here the elements of the first vector were recycled.
When one vector is shorter than the other, the elements of that entire vector get recycled, starting
from the first element and getting repeated as often as necessary. Note that if this mechanism does
not use a complete cycle, you'll get a warning.
`(1:4) + y`
Finally, note that using a single value (i.e., a scalar) is just a special case of recycling the same value
over and over.
`y * 2`


*** =instructions

Look at the help page for the `seq()` function (`?seq`).
The `seq()` function can take five different arguments, but not all of them make sense at the same
time. In particular, it would not make sense to give the from, to, by, and length arguments, since
you can figure out the length given from, to, and by. You can pass argments by name rather than
position; this is helpful for skipping arguments and it is often good form to used named arguments, even when not necessary, as it makes your intent clearer.

Use the `seq()` function to generate a vector of the numbers between 0 and 1, incrementing by 0.1 each time, using both the length.out and by parameters. Use the `seq()` function to generate numbers 1 through 99, using as few parameters as 

For the `rep()` function, explore the difference between `each` and `times`

Can you predict what this command does?
10 ^ (0:5)

*** =pre_exercise_code
```{r}
colors <- c("red", "orange", "yellow", "green", "blue", "indigo", "violet")
```


*** =sample_code
```{r}
# Generate a vector of the numbers between 0 and 1, incrementing by 0.1 each time, using the length.out parameter


# Generate a vector of the numbers between 0 and 1, incrementing by 0.1 each time, using the by parameter


# Generate a vector of numbers from 1 to 99


# Repeat the entire colors vector twice. The colors vector has been preloaded for you.


# Repeat each element of the colors vector twice


# Repeat the colors vector, setting both the times and each parameters to 2


# Repeat the colors vector, such that the result has 10 elements. When using the length.out argument, you may not get a full cycle of repetition.


# Can you predict what the following code will do?
10 ^ (0:5)

```

*** =solution
```{r}
# Generate a vector of the numbers between 0 and 1, incrementing by 0.1 each time, using the length.out parameter
seq(0, 1, length.out = 11)

# Generate a vector of the numbers between 0 and 1, incrementing by 0.1 each time, using the by parameter
seq(0, 1, by = 0.1)

# Generate a vector of numbers from 1 to 99
seq(to = 99)

# Repeat the colors vector twice. The colors vector has been preloaded for you.
rep(colors, times = 2)

# Repeat each element of the colors vector twice
rep(colors, each = 2)

# Repeat the colors vector, setting both the times and each parameters to 2
rep(colors, each = 2, times = 2)

# Repeat the colors vector, such that the result has 10 elements. When using the length.out argument, you may not get a full cycle of repetition.
rep(colors, length.out = 10)

# Can you predict what the following code will do?
10 ^ (0:5)

```

*** =hint
Read the help pages for `seq()` and `rep()`, e.g., `?seq`.
If you don't explicitly set a parameter, the default will be used.

Carefully consider how many vector elements there are between 0 and 1, when incrementing by 0.1!


*** =sct
```{r}
test_predefined_objects("colors")
test_function("seq", args = c("from", "length.out"), index = 1,
              not_called_msg = "Use the `seq()` function with `length.out` to generate a vector of numbers with a fixed number.",
              args_not_specified_msg = "Have you specified three arguments to the `seq()` function (to, from and length.out)?",
              incorrect_msg = "Have you passed in the correct arguments (`from` = `0`, `to` = `1`, `length.out` = `11`) to the `seq()` function? The `length.out` parameter should be 11!")
#test_function_result("seq", index = 1, incorrect_msg = "Check your `seq()` call. Are you passing in the correct arguments (`to` = `0`, `from` = `1`, `length.out` = `11`)?")  
test_function("seq", args = c("from", "by"), index = 2,
              not_called_msg = "Use the `seq()` function to generate a vector of numbers, where regular increments are defined by the `by` parameter.",
              args_not_specified_msg = "Have you specified three arguments to the `seq()` function (to, from and by)?",
              incorrect_msg = "Have you passed in the correct arguments (`0`, `1`, `0.1`) to the `seq()` function?")
test_function("seq", args = c("to"), index = 3,
              not_called_msg = "Use the `seq()` function to generate a regularly incremented vector of numbers.",
              args_not_specified_msg = "Have you specified the correct argument to the `seq()` function (by)?",
              incorrect_msg = "Have you passed in the correct arguments (`to` = `99`) to the `seq()` function?")
test_function("rep", args = c("x", "times"), index = 1,
              not_called_msg = "Use the `rep()` function with `times` to repeat an entire vector a fixed number of times.",
              args_not_specified_msg = "Did you specify the vector you want to repeat (`colors`)? Have you specified the correct number of times the `colors` vector should be repeated (2)?",
              incorrect_msg = "Have you passed in the correct argument (`times` = `2`) to the `rep()` function?")
test_function("rep", args = c("x", "each"), index = 2,
              not_called_msg = "Use the `rep()` function with `each` to repeat each element of a vector a fixed number of times.",
              args_not_specified_msg = "Did you specify the vector you want to repeat (`colors`)? Have you specified the correct number of times each element of the `colors` vector should be repeated (2)?",
              incorrect_msg = "Have you passed in the correct arguments (`each` = `2`) to the `rep()` function?")
test_function("rep", args = c("x", "each", "times"), index = 3,
              not_called_msg = "Use the `rep()` function with `each` and `times`.",
              args_not_specified_msg = "Did you specify the vector you want to repeat (`colors`)? Have you specified the correct arguments to the `rep()` function (each, times)?",
              incorrect_msg = "Have you passed in the correct arguments (`each` = `2`, `times` = `2`) to the `rep()` function?")
test_function("rep", args = c("x", "length.out"), index = 4,
              not_called_msg = "Use the `length.out` parameter to set the number of elements in the generated vector.",
              args_not_specified_msg = "Did you specify the vector you want to repeat (`colors`)? Have you specified the correct argument to the `rep()` function (length.out)?",
              incorrect_msg = "Have you passed in the correct arguments (`length.out` = `10`) to the `rep()` function?")
test_error()
```

--- type:NormalExercise lang:r xp:50 skills:1 key:24c5683a62
## Accessing vectors

Vector elements are accessed using indexing vectors, which can be numeric, character or logical vectors.

You can access an individual element of a vector by its position (or "index"), indicated using square brackets. In R, the first element has an index of 1. To get the 7th element of the  `colors` vector:
`colors[7]`.
You can also change the elements of a vector using the same notation as you use to access them:
`colors[7] <- "purple"`.

You can access multiple elements of a vector by specifying a vector of element indices inside the square brackets. All the methods that we learned about in the last section can be used to generate these indexing vectors. For example, 
`colors[c(1,7)]` gives the first and last element of the `colors` vector; `colors[1:2]` gives the first two elements.

We can select specific elements based on whether they pass some criterion, using the `which()` function. This takes a vector and returns a numeric vector of the indices of the elements which pass the test. 

Another means of accessing vector elements is using a logical indexing vector in the square brackets, where the elements that are returned are those where the logical element is `TRUE`. For example, `state.area[state.name == "Wyoming"]`. Here, the `==` is a test for equality. This is different from assignment.

We can test for membership in a vector using the `%in%` operator. For example, `"Rhode Island" %in% state.name[state.area < 56220]` will test if Rhode Island is in the smaller half of states.


*** =pre_exercise_code
```{r}
colors <- c("red", "orange", "yellow", "green", "blue", "indigo", "violet")
```


*** =instructions

R has a number of built-in datasets, such as state.name, state.area,

Use a logical vector to find the smallest states.

*** =sample_code
```{r}
# Find the first quartile value of state areas by running the summary() function on the state.area built-in vector.


# Assign it to a variable called cutoff


# Generate a logical vector, showing whether each state is smaller than the cutoff


# List out the state names of those states smaller than the cutoff, using the logical vector as an indexing vector


# Use the %in% operator to test if "New York" is one of the smallest states.




```

*** =solution
```{r}
# Find the first quartile value of state areas by running the summary() function on the state.area built-in vector.
summary(state.area)

# Assign it to a variable called cutoff
cutoff <- 37320

# Generate a logical vector, showing whether each state is smaller than the cutoff
state.area < cutoff

# List out the state names of those states smaller than the cutoff, using the logical vector as an indexing vector
state.name[state.area < cutoff]

# Use the %in% operator to test if "New York" is one of the smallest states.
"New York" %in% state.name[state.area < cutoff]



```

*** =hint
Run `summary(state.area)` to find the first quartile value.


*** =sct
```{r}
ex() %>% check_output_expr("summary(state.area)", 
             missing_msg = "Run `summary(state.area) to get the first quartile value of the states' area.")
test_object("cutoff",
                    undefined_msg = "Assign the first quartile value of the states' area to `cutoff`",
                    incorrect_msg = "Did you assign the correct value to cutoff? Check the output from summary(state.area).")
test_output_contains("state.area < cutoff",
                    incorrect_msg = "`state.area < cutoff` generates a vector where each element indicates whether that state is less than the cutoff or not.")
test_output_contains("state.name[state.area < cutoff]",
                    incorrect_msg = "Use the logical vector to index state.name. Put the logical vector inside `[]`")
ex() %>% check_operator("%in%") %>% check_result("Use `'New York' %in% state.name[state.area < cutoff]` to determine if New York is one of the smaller states.") %>% check_equal()
test_error()
```

--- type:NormalExercise lang:r xp:50 skills:1 key:9680228781
## Named vectors

Vector elements can be named using the `names()` function: 
`names(state.area) <- state.name`.
We have already seen this: the result of the `summary()` function is a named vector! 

We can access elements using a character indexing vector, where the index refers to the name(s) of the elements.
For exmple, we can access Wyoming directly:
`state.area["Wyoming"]`.

We can see all the small states and their areas in one shot:
`state.area[state.area < cutoff]`

Sadly, not all functions that fetch an element from a vector keep the associated name, e.g., `min(state.area)`, but you can find the index at which the minimum occurs, and use that.
`state.area[which.min(state.area)]`

To remove all names from vector elements, use the `unname()` function.


*** =instructions

Name each of the elements of the state.area vector with their state names (the state.name vector)

*** =pre_exercise_code
```{r}
cutoff <- 37320
```


*** =sample_code
```{r}
# Name each of the elements of the state.area vector


# Access the areas of New York and Alaska using a character indexing vector


# Print out all the states with an area less than the pre-loaded cutoff


```

*** =solution
```{r}
# Name each of the elements of the state.area vector
names(state.area) <- state.name

# Access the areas of New York and Alaska using a character indexing vector
state.area[c("New York", "Alaska")]

# Print out all the states with an area less than the pre-loaded cutoff
state.area[state.area < cutoff]

```


*** =sct
```{r}
test_predefined_objects("cutoff")
test_object("state.area",
                    undefined_msg = "Did you assign the state names to the state.area vector? Use the `names()` function.",
                    incorrect_msg = "Did you assign the state names to the state.area vector? Use the `names()` function.")
ex() %>% check_output_expr("state.area[c('New York', 'Alaska')]", 
             missing_msg = "Use the character vector `c('New York', 'Alaska')` to index state.area.")
test_output_contains("state.area[state.area < cutoff]",
                    incorrect_msg = "Try running `state.area[state.area < cutoff]`.")

test_error()
```

--- type:NormalExercise lang:r xp:50 skills:1 key:78f2f3aea7
## Miscellaneous vector functions

You can get the length of a vector using the `length()` function.

R supports sorting, using the `sort()` and `order()` functions, which return the sorted vector, or a vector of the positions of the sorted elements, respectively.

We can also randomly sample elements from a vector, using `sample()`.

Other miscellaneous useful commands on vectors include:
`rev(x)` reverses the vector <br/>
`sum(x)` sums all the elements in a numeric or logical vector <br/>
`cumsum(x)` returns a vector of cumulative sums (or a running total) <br/>
`diff(x)` returns a vector of differences between adjacent elements <br/> 
`max(x)` returns the largest element <br/>
`min(x)` returns the smallest element <br/>
`range(x)` returns a vector of the smallest and largest elements <br/>
`mean(x)` returns the arithmetic mean




*** =instructions

Get the length of the colors vector. Use the sort() and order() functions on the colors vector. 

Sort the state names by state size. Use sample() to randomly pick four state names. Use max() to find the size of the largest state. What is the name of the largest state?

*** =pre_exercise_code
```{r}
colors <- c("red", "orange", "yellow", "green", "blue", "indigo", "violet")
```

*** =sample_code
```{r}
# Get the length of the colors vector (preloaded for you).


# Sort the colors vector in reverse alphabetical order


# What do you get when you order the colors vector?


# Sort the state names by state size


# Use sample() to randomly pick four state names


# Use max() to find the size of the largest state


# What is the name of the largest state?

```

*** =solution
```{r}
# Get the length of the colors vector (preloaded for you).
length(colors)

# Sort the colors vector in reverse alphabetical order
sort(colors, decreasing = TRUE)

# What do you get when you order the colors vector?
order(colors)

# Sort the state names by state size
state.name[order(state.area)]

# Use sample() to randomly pick four state names
sample(state.name, 4)

# Use max() to find the size of the largest state
max(state.area)

# What is the name of the largest state?
state.name[state.area == max(state.area)]
```


*** =sct
```{r}
test_predefined_objects("colors")
test_function("length", args = "x",
              not_called_msg = "Use the `length()` function to count the number of elements in the `colors` vector",
              args_not_specified_msg = "Have you specified the argument to the `length()` function?",
              incorrect_msg = "Have you passed in the correct argument (`colors`) to the `length()` function?")
test_function("sort", args = c("x", "decreasing"),
              not_called_msg = "Use the `sort()` function to sort the elements of a vector",
              args_not_specified_msg = "Have you specified both arguments to the `sort()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`colors`, `decreasing = TRUE`) to the `sort()` function?")
test_function("order", args = c("..."),
              not_called_msg = "Use the `order()` function to get the ordered indices of a vector",
              args_not_specified_msg = "Have you specified the argument to the `order()` function?",
              incorrect_msg = "Have you passed in the correct argument (`colors`) to the `order()` function?")
ex() %>% check_output_expr("state.name[order(state.area)]", 
              missing_msg = "Use the ordered vector `order(state.area)` to index state.name.")
test_function("sample", args = c("x", "size"),
              not_called_msg = "Use the `sample()` function to randomly sample elements of a vector",
              args_not_specified_msg = "Have you specified both arguments to the `sample()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`state.name`, `4`) to the `sample()` function?")
test_function("max", args = c("..."),
              not_called_msg = "Use the `max()` function to return the largest element of a vector",
              args_not_specified_msg = "Have you specified the argument to the `max()` function?",
              incorrect_msg = "Have you passed in the correct argument (`state.area`) to the `max()` function?")
ex() %>% check_output_expr("state.name[state.area == max(state.area)]", 
              missing_msg = "Use the logical vector `state.area == max(state.area)` to index state.name.")
test_error()
```


--- type:NormalExercise lang:r xp:50 skills:1 key:a1e7552548
## Factors

Factors are similar to vectors, and can mostly be treated as such, but they have another tier of information. A factor keeps track of all the
distinct values in that vector, and notes the positions in the vector where each distinct value can be found.
Factors are R's preferred way of storing categorical data.
The set of distinct values are called levels. To see (and set) the levels of a factor, you can use the `levels()`
function, which will return the levels as a vector.

Note that setting the levels of a factor using `levels()` only changes the labels, not
the underlying integer representation.

The `str()` function allows you to view the structure of an object, and will give you a hint about how R stores factors (or any other object). 
The `class()` function returns the class of an object, without having to see all the details.</br>
`str(state.division)` </br>
`class(state.division)`

Note the list of integers corresponds to the level at each position. While factors may behave like
character vectors in many ways, they are much more efficient because they are internally represented
as integers, and computers are good at working with integers.

*** =instructions

Generate a vector of 500 colors, called pony.colors, from the colors vector (which has been pre-loaded for you), and convert it to a factor using the factor() function. The levels of a factor are by default sorted in alphabetical order, but the order can be set using the `levels` parameter in the `factor()` function. Create a second factor, pony.colors.f2, where the levels are in the same order as in the colors vector. This is especially important if your vector does not include examples of all the levels you want to include.

*** =pre_exercise_code
```{r}
colors <- c("red", "orange", "yellow", "green", "blue", "indigo", "violet")
```


*** =sample_code
```{r}
# Generate a vector of 500 colors, called pony.colors, from the colors vector


# Convert this to a factor called pony.colors.f using the factor() function


# Look at the structure of this factor using str()


# Plot the pony.colors.f factor to see how often each factor appears


# Assign a new factor, pony.colors.f2, where the levels are in the same order as the colors vector



```

*** =solution
```{r}
# Generate a vector of 500 colors, called pony.colors, randomly sampled from the colors vector
pony.colors <- sample(colors, size = 500, replace = TRUE)

# Convert this to a factor called pony.colors.f using the factor() function
pony.colors.f <- factor(pony.colors)

# Look at the structure of this factor using str()
str(pony.colors.f)

# Plot the pony.colors.f factor to see how often each factor appears
plot(pony.colors.f)

# Assign a new factor, pony.colors.f2, where the levels are in the same order as the colors vector
pony.colors.f2 <- factor(pony.colors, levels = colors)

```


*** =sct
```{r}
test_predefined_objects("colors")
test_function("sample", args = c("x", "size", "replace"),
              not_called_msg = "Use the `sample()` function to randomly sample elements in the `colors` vector",
              args_not_specified_msg = "Have you specified all the arguments to the `sample()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`colors`, `size = 500`, `replace = TRUE`) to the `sample()` function?")
test_object("pony.colors",
              undefined_msg = "Assign 500 colors randomly sampled from the `colors` vector to `pony.colors`",
              incorrect_msg = "Use `sample(colors, size = 500, replace = TRUE)` to randomly sample 500 colors.")
test_object("pony.colors.f",
              undefined_msg = "Assign pony.colors.f using `factor()` to convert a vector to a factor.",
              incorrect_msg = "Did you use the `pony.colors` vector as an argument to `factor()`?")
test_function("str", args = c("object"),
              not_called_msg = "Use the `str()` function to display the internal structure of an object.",
              args_not_specified_msg = "Have you specified the argument to the `str()` function?",
              incorrect_msg = "Have you passed in the correct argument (`pony.colors.f`) to the `str()` function?")
test_function("plot", args = "x",
              not_called_msg = "Use the `plot()` function to display the frequency of each level of a factor.",
              args_not_specified_msg = "Have you specified the argument to the `plot()` function?",
              incorrect_msg = "Have you passed in the correct argument (`pony.colors.f`) to the `plot()` function?")
test_object("pony.colors.f2",
              undefined_msg = "Assign pony.colors.f2 using the `colors` vector to determine the levels.",
              incorrect_msg = "Did you use the `colors` vector to determine the levels of `pony.colors.f2`?")
test_function("factor", args = c("x", "levels"), index = 2,
              not_called_msg = "Use the `factor()` function to display the internal structure of an object.",
              args_not_specified_msg = "Have you specified both arguments to `factor()`?",
              incorrect_msg = "Have you passed in the correct arguments (`pony.colors`, `levels = colors`) to `factor()`?")
test_error()
```

--- type:NormalExercise lang:r xp:50 skills:1 key:646bd4bed5
## Matrices

The multi-dimensional structures in R, where all the elements are of the same data type, are called arrays.
Arrays have three dimensions: number of rows, number of columns and number of layers. Matrices are a
special type of array using only two of those dimensions (rows and columns) and can be thought of as
tables, which can only contain a single data type.

An example of a matrix is the USPersonalExpenditure dataset, one of the built-in datasets, which describes how
much Americans spent in five categories from 1940-1960.

Accessing (and assigning) elements of a matrix is analogous to accessing (and assigning) elements of
a vector, but where vectors have only one index position, matrices have two, one for rows and
one for columns. As with vectors, each specification is an indexing vector.

*** =instructions

Examine the USPersonalExpenditure dataset. Notice that the rows and columns of the matrix are named, using the categories and years as row
names and column names, respectively. Find how many rows and columns the dataset has using `dim()`. Access the rows and columns as separate vectors using the `rownames()` and `colnames()` functions. 

Use indexing vectors to access specific elements, or complete rows or columns. For example, `USPersonalExpenditure[1, 3]` 
returns the element in the first row, third column. Return the same element, but using character index vectors to indicate the rows and columns.

A blank vector in either the row or column specification implies we want all elements in that dimension. Get all Private Education expenditures. If your result is one-dimensional, it is by default returned as a vector. If you don't want this behavior, you can use the
`drop=FALSE` option.

Remember all of the elements in a matrix must be of the same data type. If you assign one element
of a different data type, R will convert (or coerce) elements as necessary.
`USPersonalExpenditure["Personal Care", "1955"] <- "Unknown"` will convert all elements in the matrix from numbers to characters. How should we have done this to avoid this
coercion?


*** =sample_code
```{r}
# Use dim() to find how many rows and columns the USPersonalExpenditure dataset has


# List the row and column names of USPersonalExpenditure



# Use character vectors to return the element at USPersonalExpenditure[1, 3]


# Get all Private Education and Personal Care expeditures for all years


# Return the Personal Care expenditures from all years, as a matrix


# Assign the element for Personal Care in 1955 as unknown, such that the elements of the matrix are not coerced to characters

```

*** =solution
```{r}
# Use dim() to find how many rows and columns the USPersonalExpenditure dataset has
dim(USPersonalExpenditure)

# List the row and column names of USPersonalExpenditure
rownames(USPersonalExpenditure)
colnames(USPersonalExpenditure)

# Use character vectors to return the element at USPersonalExpenditure[1, 3]
USPersonalExpenditure["Food and Tobacco", "1950"]

# Get all Private Education and Personal Care expeditures for all years
USPersonalExpenditure[c("Private Education", "Personal Care"), ]

# Return the Personal Care expenditures from all years, as a matrix
USPersonalExpenditure["Personal Care",  , drop = FALSE]

# Assign the element for Personal Care in 1955 as unknown, such that the elements of the matrix are not coerced to characters
USPersonalExpenditure["Personal Care", "1955"] <- NA


```

*** =hint
Matrix elements are accessed by specifying two indexing vectors: the first indicating rows, the second columns. Leaving either of those vectors blank will select all of that dimension.

*** =sct
```{r}
test_function("dim", args = c("x"),
              not_called_msg = "Use the `dim()` function to get the number of rows and columns in the USPersonalExpenditure dataset",
              args_not_specified_msg = "Have you specified the correct argument (`USPersonalExpenditure`) to the `dim()` function?",
              incorrect_msg = "Have you passed in the correct argument (`USPersonalExpenditure`) to the `dim()` function?")
test_function("rownames", args = c("x"),
              not_called_msg = "Use the `rownames()` function to get the names of the rows for the USPersonalExpenditure dataset",
              args_not_specified_msg = "Have you specified the argument to the `rownames()` function?",
              incorrect_msg = "Have you passed in the correct argument (`USPersonalExpenditure`) to the `rownames()` function?")
test_function("colnames", args = c("x"),
              not_called_msg = "Use the `colnames()` function to get the names of the rows for the USPersonalExpenditure dataset",
              args_not_specified_msg = "Have you specified the argument to the `colnames()` function?",
              incorrect_msg = "Have you passed in the correct argument (`USPersonalExpenditure`) to the `colnames()` function?")
test_student_typed("USPersonalExpenditure['Food and Tobacco', '1950']",
              not_typed_msg = "`USPersonalExpenditure['Food and Tobacco', '1950']` uses 'Food and Tobacco' to indicate the row and '1950' to indicate the column.")
test_student_typed("USPersonalExpenditure[c('Private Education', 'Personal Care'), ]",
              not_typed_msg = "`USPersonalExpenditure[c('Private Education', 'Personal Care'), ]` selects the 'Private Education' and 'Personal Care' rows from the original matrix.")
test_output_contains("USPersonalExpenditure['Personal Care',  , drop = FALSE]",
              incorrect_msg = "`USPersonalExpenditure['Personal Care',  , drop = FALSE]` generates a 1-row matrix.")
test_output_contains("USPersonalExpenditure['Personal Care', '1955'] <- NA",
              incorrect_msg = "Assigning an element as NA does not coerce the rest of the matrix.")
test_error()
```


--- type:NormalExercise lang:r xp:50 skills:1 key:ee938e4524
## Creating matrices

There are a few ways to make a new matrix. The `matrix()` function takes as arguments a vector of all
the elements, and then some information about how many rows and columns there are. By default, the matrix
is filled in column order, but you can change this behaviour with the `by.rows=TRUE` option.

For example, `game1 <- matrix(c("X","","O","","X","O","","",""), ncol = 3)`
creates a tic-tac-toe game. 
In this matrix, the rows and columns are not named, and can only be accessed using numeric
indices.

Another very common way of assembling a matrix is by combining vectors or matrices. They can be
stacked by row or column, using the `rbind()` or `cbind()` functions, respectively.

*** =instructions

Look at the help pages for the `matrix()` function. Create a numeric 3x4 matrix called m, filled with 0. Name the rows and columns using the built-in letters and LETTERS vectors, which contain the lowercase and uppercase letters of the alphabet, respectively.

Use `cbind()` to create a second matrix from the built-in datasets `state.name` and `state.abb`.

*** =sample_code
```{r}
# Create a 3x4 numeric matrix called m, filled with 0


# Name the rows a through c and the columns A through D. Hint, use the built-in letters/LETTERS vectors for this.


# Assign 1s to the first column


# Create a second matrix called m2, using cbind() to combine state.name and state.abb

```

*** =solution
```{r}
# Create a 3x4 numeric matrix called m, filled with 0
m <- matrix(0, nrow = 3, ncol = 4)

# Name the rows a through c and the columns A through D. Hint, use the built-in letters/LETTERS vectors for this.
rownames(m) <- letters[1:3]
colnames(m) <- LETTERS[1:4]

# Assign 1s to the first column
m[ , 1] <- 1 # could also be accessed using m[ , "A"]

# Create a second matrix called m2, using cbind() to combine state.name and state.abb
m2 <- cbind(state.name, state.abb)


```

*** =hint
Did you assign the rows and columns correctly? Remember, by default, R does rows by columns (R x C).

*** =sct
```{r}
test_object("m",
            undefined_msg = "Assign a new matrix to `m`.",
            incorrect_msg = "Did you assign the correct values to `m`? Use `m[ , 1] <- 1` to fill the first row with 1s.")
test_object("m2",
            undefined_msg = "Assign a new matrix to `m2`.",
            incorrect_msg = "Did you assign the correct value to `m2`? Use `cbind()`.")

test_error()
```


--- type:NormalExercise lang:r xp:50 skills:1 key:7152a4e90b
## Lists

A list in R is analogous to a hash or associative array in most other programming languages. 
Lists can hold data structures of different types,
and of different sizes. Each component in a list can be (optionally, but commonly) separately named. In fact, one list
can be a member of another list, allowing for deeply nested and arbitrarily complex data structures to be
modeled.

Lists can be created using the list() function. When using the `list()` function, you can optionally
give names to the components (component names are called tags).
`pete <- list("Peter", "O'Toole", 1932, FALSE)`
`pete <- list(first.name = "Peter", last.name = "O'Toole", yob = 1932, oscar.winner = FALSE)`
Note that we have different data types in the same list (character, numeric and logical). Note also
the difference between the first and second attempt to model a great actor. In the first case, you need
to know what the position of each component is; in the second, each component is named (tagged)
with the tag we provided at creation.

There are several ways to refer to the components of a list; the differences can be subtle, but important.
The most straightforward way to refer to a single component is using the `[[` notation. You can always
provide an integer to access the component by position, or you can provide a character string if the
component is tagged.

For tagged components where the tag is a literal character string, you can use the `$` notation. This
is less flexible, but looks clearer. Use this when you can.
If you want to access multiple components, you can use the `[` notation, which takes the usual indexing
vector. Note that this will always return a list (this has to be so, because the components returned
could be of different datatypes).

*** =instructions

The results of many high-level analyses in R are packaged as lists.
The `lm()` function fits data to a linear model (i.e., performs a linear regression), and packages up
all of the results into a kind of list object.

Use the `lm()` function to generate a linear model for the relationship between Private Education expenditure over the years. This code has been provided for you.

Explore the my.model object.

Can you extract the slope and intercept of the best-fit line?
Can you extract the value of R-squared reported by the `summary()` function? Hint: save the
result of this function, and look into its structure.


*** =pre_exercise_code
```{r}
edu.spend <- unname(USPersonalExpenditure["Private Education", ])
edu.yr <- seq(from = 0, to = 20, by = 5)
my.model <- lm(edu.spend ~ edu.yr)

```


*** =sample_code
```{r}
# Make a linear model of Private Education expenditure over 25 years
edu.spend <- unname(USPersonalExpenditure["Private Education", ])
edu.yr <- seq(from = 0, to = 20, by = 5)
my.model <- lm(edu.spend ~ edu.yr)

# Extract the slope (labelled edu.yr in the coefficients component) of the best-fit line into a variable called slope.


# Extract the intercept (also from the coefficients component) into a variable called intercept


# Run summary() on the my.model object and save it to a variable called model.summary


# Extract the value of R-squared from the model.summary object 


```

*** =solution
```{r}
# Make a linear model of Private Education expenditure over 25 years
edu.spend <- unname(USPersonalExpenditure["Private Education", ])
edu.yr <- seq(from = 0, to = 20, by = 5)
my.model <- lm(edu.spend ~ edu.yr)

# Extract the slope (labelled edu.yr in the coefficients component) of the best-fit line into a variable called slope.
slope <- my.model$coefficients["edu.yr"]

# Extract the intercept (also from the coefficients component) into a variable called intercept
slope <- my.model$coefficients["(Intercept)"]

# Run summary() on the my.model object and save it to a variable called model.summary
model.summary <- summary(my.model)

# Extract the value of R-squared from the model.summary object 
model.summary$r.squared


```

*** =hint
Use an indexing vector to extract the correct element from the coefficients component

*** =sct
```{r}
test_error()
```





--- type:NormalExercise lang:r xp:50 skills:1 key:472005b77b
## Data frames

Data frames are two-dimensional data structures like matrices, but, unlike matrices, they can contain multiple different data types. You can think of a data frame as a list of vectors, where all the vector lengths are the same. Data frames are commonly used to represent tabular data.

Data frames behave both like a tagged list of vectors, and like a matrix, giving many options for accessing elements. Fortunately, you know them all already! When accessing a single column, the list notation is preferred. When accessing multiple columns or a subset of rows, the matrix notation is used (rows and columns are given as indexing vectors).


*** =instructions

When we were learning about vectors, we used several parallel vectors, each with length 50 to represent information about US states. The collection of vectors really belongs together, and a data frame is the tool for doing this. The `data.frame()` function combines the four data sets into a single data frame (code provided for you). Note that the first three data sets are vectors (two character, one numeric), but the last data set is a list with two components.

Note the `stringsAsFactors = FALSE` argument. Some of the vectors that we are using are character vectors, but will be automatically converted to factors if this option is not set. Since we will want to work with our character data as vectors, not as factors, we want to set this argument to `FALSE`.

As with matrices, the rows can be given names, using `rownames()`. Column names are accessed with the `names()` or `colnames()` functions.

New columns are added the same way you would add one to a list.

Many tools in R work naturally with data frames. Read the help pages for the`plot()` function. The code for visualizing the size distribution of
state within each division is provided for you. Read the first argument as "area as a function of division". 


*** =pre_exercise_code
```{r}
state.db <- data.frame(state.name, state.abb, state.area, state.center, stringsAsFactors = FALSE)
```


*** =sample_code
```{r}
# Combine different data about US states into a single data frame
state.db <- data.frame(state.name, state.abb, state.area, state.center, stringsAsFactors = FALSE)

# Access the state abbreviations column using list notation. Convince yourself that state.db$state.abb, state.db[[ "state.abb" ]] and state.db[[ 2 ]] all give the same result.

# Name the rows of state.db using state abbreviations from state.abb


# Update the column names: "name", "abb", "area", "long", "lat"


# Add state.division to the data frame as a column called division


# Use plot() to visualize the size distribution of state within each division
plot(area ~ division, data = state.db)

# Use plot() to visualize latitude as a function of longtitude



```

*** =solution
```{r}
# Combine different data about US states into a single data frame
state.db <- data.frame(state.name, state.abb, state.area, state.center, stringsAsFactors = FALSE)

# Access the state abbreviations column using list notation. Convince yourself that state.db$state.abb, state.db[[ "state.abb" ]] and state.db[[ 2 ]] all give the same result.
state.db$state.abb

# Name the rows of state.db using state abbreviations from state.abb
rownames(state.db) <- state.abb

# Update the column names: "name", "abb", "area", "long", "lat"
names(state.db) <- c("name", "abb", "area", "long", "lat")

# Add state.division to the data frame as a column called division
state.db$division <- state.division

# Use plot() to visualize the size distribution of state within each division
plot(area ~ division, data = state.db)

# Use plot() to visualize latitude as a function of longtitude
plot(lat ~ long, data = state.db)


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


--- type:NormalExercise lang:r xp:50 skills:1 key:f84392e3cd
## Subsetting data frames

As before, logical vectors can be used as indices.

Another way to select data from a data frame is using the `subset()` function. You can choose rows
based on a logical expression and can choose columns with the select option. With this function,
we only have to type the dataset name once.

The logical condition is optional, and you can specify columns to omit instead of columns to include.
`subset(state.db, select = c(name, abb))`
`subset(state.db, select = -c(long, lat))`


*** =instructions
The state.db dataset from the last exercise has been pre-loaded for you. 

Use row and column indexing vectors to extract the longitude and latitude of the centers of New York, New Jersey and Rhode Island.

Use both a logical indexing vector, and `subset()`, to extract the names of all states where the area of the state is less than the median.

Use `subset()` to extract all the states that are part of the New England, Middle Atlantic, South Atlantic and Pacific divisions (hint: use the `%in%` operator).



*** =pre_exercise_code
```{r}
state.db <- data.frame(state.name, state.abb, state.area, state.center, stringsAsFactors = FALSE)
rownames(state.db) <- state.abb
names(state.db) <- c("name", "abb", "area", "long", "lat")
state.db$division <- state.division
```


*** =sample_code
```{r}
# Extract the longitude and latitude of the centers of New York, New Jersey and Rhode Island  


# Extract the names of all states where the area of the state is less than the median, using a logical indexing vector


# Do the same thing, using the subset() function


# Use subset() to extract all the states that are part of the New England, Middle Atlantic, South Atlantic and Pacific divisions



```

*** =solution
```{r}
# Extract the longitude and latitude of the centers of New York, New Jersey and Rhode Island  
state.db[c("NY", "NJ", "CT", "RI"), c("long", "lat")]

# Extract the names of all states where the area of the state is less than the median, using a logical indexing vector
state.db[state.db$area < median(state.db$area), "name"]

# Do the same thing, using the subset() function
subset(state.db, area < median(area), select = name)

# Use subset() to extract all the states that are part of the New England, Middle Atlantic, South Atlantic and Pacific divisions
subset(state.db, division %in% c("New England", "Middle Atlantic", "South Atlantic", "Pacific") )


```

*** =hint
no hints yet

*** =sct
```{r}
test_error()
```






