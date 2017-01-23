---
title         : Introduction
description   : Getting comfortable with the Console and Script windows, using R's calculator functionality
free_preview  : true
attachments   :
  slides_link : https://s3.amazonaws.com/assets.datacamp.com/course/teach/slides_example.pdf

--- type:NormalExercise lang:r xp:50 skills:1 key:a7e72915d4
## R as a calculator

To run a command and see what the effect will be, before submitting it, use the Console panel (lower right panel).
Typing commands here will allow them to be run immediately.


Try adding two numbers together. After the prompt in the Console panel, enter:
` 1 + 2 `.
When you hit return, you should see `[1] 3`.
The answer is, of course, 3, but what is the [1] before it? It turns out that all the numbers (or scalars) in R are vectors, and the [1] is a hint about how the vector is indexed. To see a long vector of random numbers, in the Console window, type: ` rnorm(100) `.


*** =instructions
In the script window, try other basic math operations, including subtraction, multiplication, division, as well as integer math
and exponent math. When you include multiple operations, the order of operations is kept, but you can always force an order with parentheses.

*** =sample_code
```{r}
# Subtract 4 from 3


# Multiply 5 and 6 together


# Divide 7 by 8


# Order of operations can be forced. Note the difference between 1 + 2 * 3 and (1 + 2) * 3


# The %/% operator does integer division (a division symbol inside two percent signs). The %% (two percent signs) gives you the remainder. Use the first operator to get the number of times 17 can be divided by 4.


# What is the remainder from 17 divided by 4?


# R can perform exponent math. Compute 2 ^ 4.



```

*** =solution
```{r}
# Subtract 4 from 3
3 - 4

# Multiply 5 and 6 together
5 * 6

# Divide 7 by 8
7 / 8

# Order of operations can be forced. Note the difference between 1 + 2 * 3 and (1 + 2) * 3
1 + 2 * 3
(1 + 2) * 3

# The %/% operator does integer division (a division symbol inside two percent signs). The %% (two percent signs) gives you the remainder. Use the first operator to get the number of times 17 can be divided by 4.
17 %/% 4

# What is the remainder from 17 divided by 4?
17 %% 4

# R can perform exponent math. Compute 2 ^ 4.
2 ^ 4
```


*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! You can now perform basic math in R!"

```
--- type:NormalExercise lang:r xp:50 skills:1 key:61c54de30b
## Math functions in R

R includes a number of mathematical functions. The arguments to an R function are enclosed in parentheses. If there are no arguments, the space within the parentheses is left blank. Functions can take multiple arguments, which are separated by commas.
For example, ` sqrt(4) ` calls a function called sqrt, which calculates the square root of the number given as an argument, within parentheses, here 4.

*** =instructions

Other examples of R math functions include: <br/>
 `log()` [natural log] <br/>
 `log10()` [base 10 log] <br/>
 `sqrt()` [square root] <br/>
 `abs()` [absolute value] <br/>
 `exp()` [exponential] <br/>
 

The `log()` function can also return the log in other bases, if its second argument is the base. For example, `log(4, 10)` returns the log of 4 in base 10.



*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

set.seed(16180339)
```

*** =sample_code
```{r}
# Compute the natural log of 4, using the log() function


# Compute the base 10 log of 4, using the log10() function


# Compute the base 10 log of 4, using the log() function


# Compute the square root of 9


# Compute the absolute value of 3 - 4


# Compute the exponential of 2

```

*** =solution
```{r}
# Compute the natural log of 4
log(4)

# Compute the base 10 log of 4
log10(4)

# Compute the base 10 log of 4, using the log() function
log(4, 10)

# Compute the square root of 9
sqrt(9)

# Compute the absolute value of 3 - 4
abs(3 - 4)

# Compute the exponential of 2
exp(2)

```


*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki

msg_bad <- "That is not correct!"
msg_success <- "Exactly! There are many more math functions in R for you to explore!"
```