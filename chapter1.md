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
In the Console window, try other basic math operations, including subtraction (`-`), multiplication (`*`), division (`/`), as well as integer math (`%/%`)
and exponent math (`^`). When you include multiple operations, the order of operations is kept, but you can always force an order with parentheses.

In the Script window, you can run code that will be evaluated for correctness. Follow the instructions to multiply two numbers, divide two numbers, and perform exponent math. Try generating a vector of 10 random numbers. By default, the mean of the distribution the numbers are selected from will be 0, and the standard deviation will be 1. When you are satisfied with your code, click the Submit button.



*** =pre_exercise_code
```{r}
# The pre exercise code runs code to initialize the user's workspace.
# You can use it to load packages, initialize datasets and draw a plot in the viewer

set.seed(16180339)
```

*** =sample_code
```{r}
# Multiply 5 and 6 together


# Divide 7 by 8


# R can perform exponent math. Compute 2 to the power of 4.


# Generate a vector of 10 numbers


```

*** =solution
```{r}
# Multiply 5 and 6 together
5 * 6

# Divide 7 by 8
7 / 8

# R can perform exponent math. Compute 2 to the power of 4.
2 ^ 4

# Generate a vector of 10 numbers
rnorm(10)

```


*** =sct
```{r}
# SCT written with testwhat: https://github.com/datacamp/testwhat/wiki
ex() %>% check_operator("*") %>% check_result() %>% check_equal()
ex() %>% check_operator("/") %>% check_result() %>% check_equal()
ex() %>% check_operator("^") %>% check_result() %>% check_equal()
test_function("rnorm", args = "n",
              not_called_msg = "Use the `rnorm()` function to generate a vector of random numbers",
              args_not_specified_msg = "Have you specified the argument to the `rnorm()` function?",
              incorrect_msg = "Have you passed in the correct argument (`10`) to the `rnorm()` function? For this exercise, no other arguments are necessary.")
test_error()
success_msg("Great! Now you can do basic math in R!")
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
test_function("log", args = "x", index = 1,
              not_called_msg = "Use the `log()` function to calculate the natural log of a number",
              args_not_specified_msg = "Have you specified the argument to the `log()` function?",
              incorrect_msg = "Have you passed in the correct argument (`4`) to the `log()` function?")
test_function_result("log", index = 1, incorrect_msg = "Check your `log()` call. Are you passing in the correct argument (`4`)? Are you calculating the natural log?")  
test_function("log10", args = "x",
              not_called_msg = "Use the `log10()` function to calculate the base10 log of a number",
              args_not_specified_msg = "Have you specified the argument to the `log10()` function?",
              incorrect_msg = "Have you passed in the correct argument (`4`) to the `log10()` function?")
test_function("log", args = c("x", "base"), index = 2,
              not_called_msg = "Use the `log()` function with two arguments to calculate the log in any base of a number",
              args_not_specified_msg = "Have you specified both arguments to the `log()` function?",
              incorrect_msg = "Have you passed in the correct arguments (`4` and `10`) to the `log()` function?")
test_function("sqrt", args = "x",
              not_called_msg = "Use the `sqrt()` function to calculate the square root of a number",
              args_not_specified_msg = "Have you specified the argument to the `sqrt()` function?",
              incorrect_msg = "Have you passed in the correct argument (`9`)  to the `sqrt()` function?")
test_function("abs", args = "x",
              not_called_msg = "Use the `abs()` function to calculate the absolute value of a number",
              args_not_specified_msg = "Have you specified the argument to the `abs()` function?",
              incorrect_msg = "Have you passed in the correct argument (`3 - 4`) to the `abs()` function?")
test_function("exp", args = "x",
              not_called_msg = "Use the `exp()` function to calculate the exponential of a number",
              args_not_specified_msg = "Have you specified the argument to the `exp()` function?",
              incorrect_msg = "Have you passed in the correct argument (`2`) to the `exp()` function?")
test_error()
success_msg("Exactly! There are many more math functions in R for you to explore!")
```
--- type:NormalExercise lang:r xp:50 skills:1 key:2c8bc6120f
## Variables

It is useful to assign values to variables, so they can be referred to later. This is done using the assignment operator `<-`.


*** =instructions

Assign the given numeric values for `US.population` and `US.area` and calculate the `US.pop.density`. Note, case matters!

*** =sample_code
```{r}
# Set the variable US.population to 3.19e8


# Set the variable US.area to 3719000


# Calculate the US.pop.density by dividing US.population by US.area


# R will not automatically print out the value of an assigned variable. Type the name of the variable by itself to see it.


```

*** =solution
```{r}
# Set the variable US.population to 3.19e8
US.population <- 3.19e8

# Set the variable US.area to 3719000
US.area <- 3719000

# Calculate the US.pop.density by dividing US.population by US.area
US.pop.density <- US.population / US.area

# R will not automatically print out the value of an assigned variable. Type the name of the variable by itself to see it.
US.pop.density

```


*** =sct
```{r}
test_object("US.population")
test_object("US.area")
test_object("US.pop.density")
test_output_contains("US.pop.density",
                      incorrect_msg = "Did you print out `US.pop.density` on a line by itself?")
test_error()
```
