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


# Generate a vector which is the colors vector twice. The colors vector has been preloaded for you.


# Repeat each element of the colors vector


# xx difference between each and times


# xx When using the length.out argument, you may not get a full cycle of repetition.


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

# Generate a vector which is the colors vector twice. The colors vector has been preloaded for you.
rep(colors, times = 2)

# Repeat each element of the colors vector
rep(colors, each = 2)

# xx difference between each and times
rep(colors, each = 2, times = 2)

# xx When using the length.out argument, you may not get a full cycle of repetition.
rep(colors, length.out = 10)

# Can you predict what the following code will do?
10 ^ (0:5)

```


*** =sct
```{r}

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




*** =instructions

R has a number of built-in datasets, such as state.name, state.area,

Use a logical vector to find the smallest states.

*** =sample_code
```{r}
# Find the first quartile value of state areas by running the summary() function on the state.area built-in vector.
which(state.area > cutoff)
state.name[which(state.area > cutoff)]

# Assign it to a variable called cutoff


# Generate a logical vector, showing whether each state is smaller than the cutoff


# List out the state names of those states smaller than the cutoff, using the logical vector as an indexing vector


# Use the %in% operator to test in "New York" is one of the smallest states.




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
state.name[state.area < 37320]

# Use the %in% operator to test in "New York" is one of the smallest states.
"New York" %in% state.name[state.area < cutoff]



```


*** =sct
```{r}
test_object("cutoff")
test_output_contains("state.area < cutoff",
                    incorrect_msg = "Did you assign the correct value to cutoff?")
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


# Ensure the levels are in the same order as the colors vector



```

*** =solution
```{r}
# Generate a vector of 500 colors, called pony.colors, from the colors vector
pony.colors <- sample(colors, size = 500, replace = TRUE)

# Convert this to a factor called pony.colors.f using the factor() function
pony.colors.f <- factor(pony.colors)

# Look at the structure of this factor using str()
str(pony.colors.f)

# Plot the pony.colors.f factor to see how often each factor appears
plot(pony.colors.f)

# Ensure the levels are in the same order as the colors vector
pony.colors.f2 <- factor(pony.colors, levels = colors)

```

*** =hint
no hints yet

*** =sct
```{r}
test_predefined_objects("colors")
test_error()
```






--- type:NormalExercise lang:r xp:50 skills:1 key:472005b77b
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