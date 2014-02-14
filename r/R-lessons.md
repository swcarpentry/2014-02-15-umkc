Adapted by Jonah Duckles from earlier work by [Jonah Duckles](https://github.com/jduckles/fossmodules/blob/master/R/Lecture1.mkd) and [Carlos Anderson](https://github.com/redcurry/r-tutorial/blob/master/tutorial.md)

### Why use R?
* Advantages
    * Can be run nearly anywhere (servers, clusters, etc)
    * lightweight on system resources
    * useful for testing
* Disadvantages 
    * No gui, or detached gui
    * Not an integrated development environment

### RStudio
[RStudio](http://www.rstudio.com/) is a development environment for R that is very easy to use.

![RStudio Desktop](./images/rstudio-windows.png)

### About RStudio
* Advantages
    * Easy to use
    * Integrated help, editor, etc
    * Debugging and data object viewing
* Disadvantages
    * Older and less updated packages can sometimes run unexpectedly

### A bit of history 
#### S language

* Developed by John Chambers at Bell Laboratories
* Motivation was "to turn ideas into software, quickly and faithfully"

#### S-Plus

* Commercial adaptation of S 

#### R Language

* GNU Licensed Open Source project
* Created by Ross Ihaka and Robert Gentleman in New Zealand 
* Named for the first letter in the primary author's names.


### When to use R 
* Plotting
* Statiscical analysis
* where everything can fit in memory.

### References 
* R in a nutshell
* R Cookbook 
* [Use R! Series at Springer](http://bit.ly/UseRBooks)

### Command Line 
R is an interactive language, much like the BASH shell.


    $ R
    
    R version 3.0.0 (2013-04-03) -- "Masked Marvel"
    Copyright (C) 2013 The R Foundation for Statistical Computing
    Platform: x86_64-apple-darwin10.8.0 (64-bit)

    R is free software and comes with ABSOLUTELY NO WARRANTY.
    You are welcome to redistribute it under certain conditions.
    Type 'license()' or 'licence()' for distribution details.

      Natural language support but running in an English locale

    R is a collaborative project with many contributors.
    Type 'contributors()' for more information and
    'citation()' on how to cite R or R packages in publications.

    Type 'demo()' for some demos, 'help()' for on-line help, or
    'help.start()' for an HTML browser interface to help.
    Type 'q()' to quit R.

    >


### R is Interactive

When you enter commands into the R prompt you'll get immediate feedback:

    > 1 + 2 + 7

    > 1 + 2 * 3

    > (1 + 2) * 3


### Everything is a vector

The results of our first example return as a vector of length one.

    [1] 7

### We can make longer vectors using `c()`

`c()` is used to *combine* numbers into longer vectors

    c(1,2,3,0,10,4,5)

or if what we want is a sequence we can use a shorthand `:` operator:

    1:50

### Getting help

Help is available whenever you need it in R
    
    ?c

### Variable assigment

Variables are named pieces of memory we can use to place data and recall it.  Variables have data types and the R language is a dynamically typed language.

Variable names can be any unique string of characters that starts with a letter and is not a reserved word.

    y <- 1
    typeof(y)

    y <- "1"
    typeof(y)
    
    y <- c(1,2)
    typeof(y)

    y <- c(1,"2") # Be careful, vectors of mixed type get coxed to some homogeneous type that you may not want.

    2 <- "2" # Won't work!
    n2 <- "2" # Variable names have to start with a letter

Reserved words in R are:
    
    if else repeat while function for in next break TRUE FALSE NULL Inf NaN NA NA_integer_ NA_real_ NA_complex_ NA_character_

### Operators
Many operations work directly on vectors, applying the operation on each
element of the vectors involved.

    y <- 10:1
    z <- x + y
    a <- 2 * x

Basic operations are `+`, `-`, `*`, `/`, and `^`. For example,

    y <- x^2    # Replaces old value of y

**Exercise.** Write R code to generate the first 100 odd numbers.

**Solution.** `2 * 1:100 - 1`


### Mismatched vector sizes

When operating with a smaller vector on a larger one, the smaller one will recycle, or repeat.

    c(1,2,3,4) + 1

    c(1,2,3,4) * c(10,20)


**Exercise**  Using the recycling behavior of short vectors, see if you can construct a two element vector which holds all of the odd numbers from `1:10` and zeros in the even number places.

**Solution** `c(1:10) * c(1,0)` What happens if you do c(1:11) * c(1,0)?


*** BREAK *** 


### Numbers

Numbers are interpreted literally

    > 2.5
    [1] 2.5

    > typeof(1)
    [1] "double"

### Matrix

Matrices in R are an extension of vectors to two dimensions, they are stored as lists with dimensions.

    m <- matrix(data=1:12, nrow=4, ncol=3)
    m

    m[1,1]
    m[4,2]
    m[4,3]

More info at `?matrix`

### Arrays

Extend vectors to n-dimensions

    a <- array(data=1:24, dim=c(4,3,2))

They're built up from arrays.

More info at `?array`

** Exercise ** Make a 4-dimensional array with 256 elements

** Solution ** array(1:256, dim=c(4,4,4,4))

### Boolean

`TRUE` and `FALSE` are special words in R

    > "a" == "b"
    1] FALSE
    > "a" == "a"
    [1] TRUE

    > TRUE == TRUE
    [1] TRUE

More at `help('TRUE')`


### Functions

Our computer is great at doing things over and over again.  We just have to learn how to tell the programming language to do what we want.

In mathematics we know about functions:
    
    f(x) = x^3

We feed in some x and it gives us back (returns), that x raised to the power 3.

In programming, functions are how we wrap up pieces of code that take some input, do a series of operations and return some output.

When we **define** a function, we make a recipe for what will happen, complete with ingredients and outcomes.

### Functions #2

In R we declare a function by calling a function called `function()`.

    cube <- function(x) { return(x^3) };

* cube is the function's *name*,
* x is the functions *parameter*,
* anything in the `{}` is the function's *body* or *expression*, it describes what the function does with its inputs. 


### Function parameters

We've seen that we can have functions that take parameters `x` and `n`.

    odds <- function(n) { return(2 * 1:n - 1) }

We can have multiple parameters

    product <- function(x,y) { return (x * y) } 

We can also set default parameters, allowing us to call the function in a way where the values set in the function definition are set as defaults if the value is not specified.

    odds <- function(n=100) { return(2 * 1:n - 1) }

    odds()
    
### Positional Parameters and Named Parameters

R functions can have either named parameters or positional parameters.  Named parameters can be specified in any order. 

    somefun <- function(x,y,name="Inigo Montoya") { return( c(x,y,name) ); }
    somefun(1,2)

    somefun(1,2,name="Six Fingered Man")

In this way we can define functions which have default behaviors, but can have their defaults overridden.  This is a very handy thing in scientific modeling exercises.

*Excercise* - Write a function called fv (future value) which computes compound interest on a value pv with a default annual rate of 4% compounded daily.  Write your function so the pv, rate and number of compounding periods are function parameters 
    
    interest <- function(x,rate=0.04,periods=365) { x * (1+(rate)/periods)^(periods) }

### Control structures 



### Histograms

We can quickly verify that these random numbers come from a normal distribution
by plotting a histogram:


    # Base plot histogram() function
    x <- rnorm(10000,mean=100, sd=25)
    hist(x)

**Exercise.** Plot a histogram of the normal distribution (10,000 numbers)
with a mean of 0 and a standard deviation of 1.

**Solution.** hist(rnorm(10000))

### Summary statistics


Given a vector of numbers, we can also get some summary statistics:

    summary(x)

Or specific quantiles, like the 2.5% and 97.5% quantiles:

    quantile(x, prob=c(0.025, 0.975))

Other useful functions you can use are `sum`, `mean`, `median`, `var`,
`min`, and `max`.

### Sampling


Sometimes you want to take a random sample from your data, either with
or without replacement. For example,

    sample(x, size=10, replace=TRUE)

takes a subsample. To randomize your data, don't specify a size:

    sample(x, replace=TRUE)

One may want to take thousands of such samples, calculate some statistic,
and examine the distribution of such statistic. This is known as bootstrapping.
To replicate an operation many times and get the result of each operation
as an element of a vector, use `replicate`:

    replicate(10, mean(sample(x, replace=TRUE)))

**Exercise.** Write a function that computes the 95% bootstrap
confidence interval of the mean for `x`.

**Solution.**
`ci <- function(x) { quantile(replicate(10000, mean(sample(x, replace=TRUE))), prob=c(0.025, 0.975)) }`


### Data frames

Used to represent tabular data:

    myframe <- data.frame(name=c("Jeff", "Mark", "John", "Fred"), 
        age=c(19,34,65,42), 
        height_in=c(72,70,74,69))
    myframe

* column names
* vectors of values for each colum name
* values have to be same length

More at `?data.frame`

**Exercise** Create your own data frame into your R session with the columns name, age and height_in

### Data frame

We've been working with vectors so far, but another important data structure
in R is the data frame. A data frame is like a table, with rows and columns,
and the columns are often named.

R comes with many built-in data sets, which often come as data frames.
See the built-in data sets:

    data()

Let's look at the data frame `trees`:

    trees

*Explain structure.*

We can access each column as a vector by specifying the header name after
the data frame variable name:

    trees$Girth

We can also access each row as a one-row data frame using bracket notation:

    trees[1,]    # First number is the row, empty columns means grab all

Instead of giving it a row index, we can also specify a conditional expression:

    trees[trees$Height > 75,]

**Exercise.** Write a function to calculate the mean Volume of x,
a data frame that conforms to `trees`, with a Girth less than `max_girth`.

**Solution.** `vol <- function(x, max_girth) { mean(x[x$Girth < max_girth,]$Volume) }`

We can also create a data frame on the fly:

    
### Reading Data Frames from files

Data frames can be read in from flat files using the read.* family of functions.

    m2012 <- read.csv('umkc-materials/medals/medals_2012.txt')
    summary(m2012)
    
    ?read.csv

    # Or created on the fly
    data <- data.frame(Turbidity=rnorm(10), Concentration=rnorm(10))

### Reading and writing data

Usually, your data will be in the form of a table in a file. It could be an
Excel file, which you'll need to export as a CSV file.

**Exercise.** Create a CSV file with headers `Age` (in years) and `Height`
(in inches) and fill it up with some made-up data. Call the file `height.csv`.

To read this file in R as a data frame:

    data <- read.csv('height.csv')

You may also write a data frame as a CSV file in your current directory:

    write.csv(data, 'data.csv')

### Data manipulation

You can add a new column to a data frame on the fly like this:

    data$Weight <- data$Height * 2

Or you can obtain a new data frame with the column added to it,
but the original data frame remains intact:

    income <- data$Age * 20000
    newdata <- cbind(data, income)

**Exercise.** Add an Age column to the trees dataset, where the Age
is some function of the Girth. Use our jitter function to randomize a bit.

**Solution.** `trees$Age = jitter(trees$Girth * 10)`

### Linear regression and ANOVA

R is a very powerful statistical language with hundreds of tools that allow you
to perform any statistical test ever conceived. I'm just going to show you
the very simple linear regression and basic ANOVA.

Let's look at the relationship between Girth and Height in `trees`.

    plot(trees$Girth, trees$Height)

The plot function plots a scatter plot where the first parameter (Girth)
is in the x-axis and the second (Height) is in the y-axis. The plot function
has many other parameters to customize how the plot is displayed.

Let's test if this relationship is significant. First, run a linear regression
function, which will return a model that we can then analyze:

    lmodel <- lm(trees$Height ~ trees$Girth)

If you print out the lmodel by itself, it shows the intercept and slope,
but it doesn't tell you whether it's significant. Run an anova on the model:

    anova(lmodel)

The `coef` function also shows you the intercept and slope.

To plot the best-fit line:

    intercept <- coef(lmodel)[1]
    slope <- coef(lmodel)[2]
    abline(intercept, slope)

**Exercise**. Create a data frame with two columns, each filled with random
numbers from a normal distribution. Run a linear model on the two columns
and make sure that the slope is not significantly different. Plot the data.

*If there looks like there will be time, teach `for` and `if`.*

Rscript
-------

Suppose you want to calculate the 95% bootstrap confidence interval of the mean
on several data files. One way to do it is to write an R script that you can
then call from the command line for each of your data files, perhaps as a loop.

    ci <- function(x) {
        quantile(replicate(10000, mean(sample(x, replace=T))),
            prob=c(0.025, 0.975))
    }

    args <- commandArgs(T)
    filename <- args[1]
    data <- read.csv(filename)
    ci(data$Height)    # Specify which column to operate on

Testing
-------

Even though I've left it until the end, testing is an important part of
software development. Just as you wouldn't trust an architect who builds
bridges but doesn't test ahead of time whether the design and the materials
used will hold up the bridge, you shouldn't trust a software engineer
who doesn't test his code. You have no way to know whether it works properly.

Testing is also useful to you. As your code evolves and you change parts
of your program to add more features, you want to make sure that those changes
haven't broken other parts of your code. Automatic testing is ideal for this.

The simplest way to test your code is to use it on various inputs
and make sure the results are what you expect. For example, let's say you wrote
the standard error function as

    se <- function(x) { sd(x) / length(x) }

Is there something wrong with this function? Let's say we didn't notice.
We can do a simple test:

    x <- 1:10
    sd(x) / sqrt(length(x))    # Expected value (eqn for the standard error)
    se(x)                      # Actual results

The values don't match, so there must be something wrong with our function.

There's a more automated way of running tests, which is handy when you have
lots of functions that you're testing. Write an R script with the above (se)
function.

Next, we'll write a function that will test the function se:

    test.se <- function() {
        x <- 1:10
        checkEquals(sd(x) / sqrt(length(x)), se(x))
    }

Now, go to an R command-line and run all tests in the file (only one here):

    install.package("RUnit")    # Needed if RUnit is not present
    library(RUnit)
    runTestFile('se.R')

Notice the summary in the end: it says there was one failure.

**Exercise.** Fix the error and run the test again.

We only have one test, but `runTestFile` would have automatically run all
functions that started with the word `test`.



### Quick ggplot2 example

ggplot2 is an R package by Hadley Wickham that follows the "Grammar of Graphics" approach to graphing.  "The Grammar of Graphics" is a proposed system for graphing where each element of the graph can be added to the graph based on the underlying data.

    # Open a dataset with medal counts from the 2012 olympics
    m2012 <- read.csv('~/umkc-materials/medals/medals_2012.txt')
    summary(m)
    p <- ggplot(m2012, aes(x=Gold,y=Bronze)) 
    p + geom_point()
    p + geom_point() + geom_smooth()
        
    # Revisiting our histogram function
    d <- data.frame(var=rnorm(10000, mean=100, sd=25))
    p <- ggplot(d, aes(x=var))
    p + geom_histogram()


### plyr Lesson

`plyr` is a tool for Split->Apply->Combine workflows.

* [plyr Lesson](https://github.com/swcarpentry/bc/blob/master/lessons/misc-r/plyr/plyr.Rmd)



### Reshape

    aqm <- melt(airquality, id=c("month", "day"), na.rm=TRUE)
    cast(aqm, day ~ month ~ variable)
    cast(aqm, month ~ variable, range)


### Other resources

* [Task Views](http://cran.r-project.org/web/views/)
* [lattice](http://cran.r-project.org/web/packages/lattice/index.html)
* [Tidy Data](http://vita.had.co.nz/papers/tidy-data.pdf)
* [Reshape](http://had.co.nz/reshape/)
* [Spatial Analysis](http://cran.r-project.org/web/views/Spatial.html)
* [Use R! Series at Springer](http://bit.ly/UseRBooks)
* [R Cookbook](http://shop.oreilly.com/product/9780596809164.do)
* [R in a Nutshell](http://shop.oreilly.com/product/0636920022008.do)



