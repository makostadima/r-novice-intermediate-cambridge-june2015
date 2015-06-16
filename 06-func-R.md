---
layout: page
title: R for reproducible scientific analysis
subtitle: Creating functions
minutes: 45
---



> ## Learning objectives {.objectives}
>
> * Define a function that takes arguments.
> * Return a value from a function.
> * Set default values for function arguments.
> * Explain why we should divide programs into small, single-purpose functions.
>

If we only had one data set to analyse, it would probably be faster to load the file into a spreadsheet and use that to plot simple statistics. However, the gapminder data is updated periodically, and we may want to pull in that new information later and re-run our analysis again. We may also obtain similar data from a different source in the future.

In this lesson, we'll learn how to write a function so that we can repeat
several operations with a single command.


### Defining a function

Let's start by defining a function `fahr_to_kelvin` that converts temperatures from Fahrenheit to Kelvin:


~~~{.r}
fahr_to_kelvin <- function(temp) {
  kelvin <- ((temp - 32) * (5 / 9)) + 273.15
  return(kelvin)
}
~~~

We define `fahr_to_kelvin` by assigning it to the output of `function`.
The list of argument names are containted within parentheses.
Next, the [body](reference.html#function-body) of the function--the statements that are executed when it runs--is contained within curly braces (`{}`).
The statements in the body are indented by two spaces.
This makes the code easier to read but does not affect how the code operates.

When we call the function, the values we pass to it are assigned to those variables so that we can use them inside the function.
Inside the function, we use a [return statement](reference.html#return-statement) to send a result back to whoever asked for it.

> ## Tip {.callout}
>
> One feature unique to R is that the return statement is not required.
> R automatically returns whichever variable is on the last line of the body
> of the function. Since we are just learning, we will explicitly define the
> return statement.

Let's try running our function.
Calling our own function is no different from calling any other function:


~~~{.r}
# freezing point of water
fahr_to_kelvin(32)
~~~



~~~{.output}
[1] 273.15

~~~



~~~{.r}
# boiling point of water
fahr_to_kelvin(212)
~~~



~~~{.output}
[1] 373.15

~~~

We've successfully called the function that we defined, and we have access to the value that we returned.

### Composing Functions

Now that we've seen how to turn Fahrenheit into Kelvin, it's easy to turn Kelvin into Celsius:


~~~{.r}
kelvin_to_celsius <- function(temp) {
  celsius <- temp - 273.15
  return(celsius)
}

#absolute zero in Celsius
kelvin_to_celsius(0)
~~~



~~~{.output}
[1] -273.15

~~~

What about converting Fahrenheit to Celsius?
We could write out the formula, but we don't need to.
Instead, we can [compose](reference.html#function-composition) the two functions we have already created:


~~~{.r}
fahr_to_celsius <- function(temp) {
  temp_k <- fahr_to_kelvin(temp)
  result <- kelvin_to_celsius(temp_k)
  return(result)
}

# freezing point of water in Celsius
fahr_to_celsius(32.0)
~~~



~~~{.output}
[1] 0

~~~

This is our first taste of how larger programs are built: we define basic operations, then combine them in ever-large chunks to get the effect we want.
Real-life functions will usually be larger than the ones shown here--typically half a dozen to a few dozen lines--but they shouldn't ever be much longer than that, or the next person who reads it won't be able to understand what's going on.

> ## Challenge - Create a function {.challenge}
>
>  + In the first lesson, we learned to **c**oncatenate elements into a vector using the `c` function, e.g. `x <- c("A", "B", "C")` creates a vector `x` with three elements.
>  Furthermore, we can extend that vector again using `c`, e.g. `y <- c(x, "D")` creates a vector `y` with four elements.
>  Write a function called `fence` that takes two vectors as arguments, called
>`original` and `wrapper`, and returns a new vector that has the wrapper vector
>at the beginning and end of the original:
>
> 
> ~~~{.r}
> best_practice <- c("Write", "programs", "for", "people", "not", "computers")
> asterisk <- "***"  # R interprets a variable with a single value as a vector
>                    # with one element.
> fence(best_practice, asterisk)
> ~~~
> 
> 
> 
> ~~~{.output}
> [1] "***"       "Write"     "programs"  "for"       "people"    "not"      
> [7] "computers" "***"      
> 
> ~~~
>  + If the variable `v` refers to a vector, then `v[1]` is the vector's first element and `v[length(v)]` is its last (the function `length` returns the number of elements in a vector).
>    Write a function called `outside` that returns a vector made up of just the first and last elements of its input:
> 
> ~~~{.r}
> dry_principle <- c("Don't", "repeat", "yourself", "or", "others")
> outside(dry_principle)
> ~~~
> 
> 
> 
> ~~~{.output}
> [1] "Don't"  "others"
> 
> ~~~

Going back to our data, we're going to define a function, called `calcGDP`, that calculates the Gross Domestic Product of a nation from the data available in our dataset by multiplying the total population with the gross national income per capita.

Let's create a new folder within our project called `functions/`. Then open a new R script file and save it under the `functions/` directory with the name `calcGDP-function.R`.

Then within the R script type:


~~~{.r}
# Takes a dataset and multiplies the population column
# with the GDP per capita column.
calcGDP <- function(dat) {
  gdp <- dat$pop * dat$gdpPercap
  return(gdp)
}
~~~

Source the file and then apply the function `calcGDP` to the first few rows of our `gapminder` data frame.


~~~{.r}
calcGDP(head(gapminder))
~~~


What we get is a vector:


~~~{.output}
[1]  6567086330  7585448670  8758855797  9648014150  9678553274 11697659231

~~~



### Defining Defaults

Let's expand the `calcGDP` function, by adding some more arguments, so that we can extract the Gross Domestic Product for a specific year and a specific country. Another feature of the new function is to return the Gross Domestic Product as an added column to the input data frame. Edit the function as follows:

~~~{.r}
# Takes a dataset and multiplies the population column
# with the GDP per capita column.
calcGDP <- function(dat, year=NULL, country=NULL) {
  dat <- dat[dat$year == year, ]
  dat <- dat[dat$country == country,]

  gdp <- dat$pop * dat$gdpPercap

  new <- cbind(dat, gdp=gdp)
  return(new)
}
~~~


Here we've added two arguments, `year` and `country`, which we use to slice our `dat` data.frame and then compute the Gross Domestic Product on a subset of the data. 

To add a column to the data.frame, we used the function `cbind`, which is a two-dimensional equivalents of the `c` function, and assigned the name `gdp` to the new column.

So let's take a look at the output when we call `calcGDP` for Australia in 2007:


~~~{.r}
source("functions/calcGDP-function.R")
calcGDP(gapminder, year=2007, country="Australia")
~~~



~~~{.output}
     country year      pop continent lifeExp gdpPercap          gdp
72 Australia 2007 20434176   Oceania  81.235  34435.37 703658358894
~~~

We've set *default arguments* for both `year` and `country` variables to `NULL` using the `=` operator in the function definition. This means that those arguments will take on those values unless the user specifies otherwise.

This is handy because by default we can run the function `calcGDP` on the whole data frame, but also have the option to run in a subset of the data frame by passing an argument to either or both optional arguments.

So let us check that our function is still working for the first few rows of our `gapminder` data frame as before.


~~~{.r}
calcGDP(head(gapminder))
~~~



~~~{.output}
[1] country   year      pop       continent lifeExp   gdpPercap gdp      
<0 rows> (or 0-length row.names)

~~~

It doesn't return any output. Why?

The `year` and `country` arguments of our function `calcGDP` are by default set to `NULL`. But within the function body we slice the `dat` data frame based on these values. So when these are set to NULL the slicing returns:

~~~{.r}
year <- NULL
gapminder[gapminder$year == year, ]
~~~


~~~{.output}
[1] country   year      pop       continent lifeExp   gdpPercap gdp      
<0 rows> (or 0-length row.names)

~~~



### Conditionals

In order to update our function to decide between slicing the dataframe or not, we need to write code that automatically decides between multiple options. The tool R gives us for doing this is called a conditional statement, and looks like this: 

~~~{.r}
num <- 37
if (num > 100) {
  print("greater")
} else {
  print("not greater")
}
~~~


~~~{.output}
[1] "not greater"
 
~~~

In our case we want to check whether the arguments `year` and `country` are not NULL. To do so we will use a built in function called `is.null` and the special operator `!`.

~~~{.r}
year <- NULL
if (!is.null(year)) {
  print("year is defined")
} else {
  print("year is NULL")
}
~~~


~~~{.output}
[1] "year is NULL"
 
~~~


> #### Challenge - Adding conditional statements {.challenge}
>
> Modify the `calcGDP` function to check whether each additional argument is 
> set to `null`. Whenever they're not `null` overwrite the dataset stored in 
> `dat` with a subset given by the non-`null` argument.
>



~~~{.r}
# Takes a dataset and multiplies the population column
# with the GDP per capita column.
calcGDP <- function(dat, year=NULL, country=NULL) {
	if(!is.null(year)){
		dat <- dat[dat$year == year, ]
	}
	if(!is.null(country))
	{
	  dat <- dat[dat$country == country,]
	}

  gdp <- dat$pop * dat$gdpPercap

  new <- cbind(dat, gdp=gdp)
  return(new)
}
~~~

Now when calling the `calcGDP` function specifying only the country:


~~~{.r}
calcGDP(gapminder, country="Australia")
~~~

~~~{.output}
     country year      pop continent lifeExp gdpPercap          gdp
61 Australia 1952  8691212   Oceania  69.120  10039.60  87256254102
62 Australia 1957  9712569   Oceania  70.330  10949.65 106349227169
63 Australia 1962 10794968   Oceania  70.930  12217.23 131884573002
64 Australia 1967 11872264   Oceania  71.100  14526.12 172457986742
65 Australia 1972 13177000   Oceania  71.930  16788.63 221223770658
66 Australia 1977 14074100   Oceania  73.490  18334.20 258037329175
67 Australia 1982 15184200   Oceania  74.740  19477.01 295742804309
68 Australia 1987 16257249   Oceania  76.320  21888.89 355853119294
69 Australia 1992 17481977   Oceania  77.560  23424.77 409511234952
70 Australia 1997 18565243   Oceania  78.830  26997.94 501223252921
71 Australia 2002 19546792   Oceania  80.370  30687.75 599847158654
72 Australia 2007 20434176   Oceania  81.235  34435.37 703658358894
 
~~~


We did this so that our function is more flexible for later. We
can ask it to calculate the GDP for:

 * The whole dataset;
 * A single year;
 * A single country;
 * A single combination of year and country.

By using another speecial operator, `%in%` instead of `==` for the conditional splicing of the dataframe, we can also give multiple years or countries to those arguments. So the function becomes general enough:

~~~{.r}
# Takes a dataset and multiplies the population column
# with the GDP per capita column.
calcGDP <- function(dat, year=NULL, country=NULL) {
	if(!is.null(year)){
		dat <- dat[dat$year %in% year, ]
	}
	if(!is.null(country))
	{
	  dat <- dat[dat$country %in% country,]
	}

  gdp <- dat$pop * dat$gdpPercap

  new <- cbind(dat, gdp=gdp)
  return(new)
}
~~~

Now when calling the `calcGDP` function specifying two countries and a year:


~~~{.r}
calcGDP(gapminder, year=2007, country=c("Argentina", "Australia"))
~~~


~~~{.output}
     country year      pop continent lifeExp gdpPercap          gdp
60 Argentina 2007 40301927  Americas  75.320  12779.38 515033625357
72 Australia 2007 20434176   Oceania  81.235  34435.37 703658358894

~~~


> #### Tip: Pass by value {.callout}
>
> Functions in R almost always make copies of the data to operate on
> inside of a function body. When we modify `dat` inside the function
> we are modifying the copy of the gapminder dataset stored in `dat`,
> not the original variable we gave as the first argument.
>
> This is called "pass-by-value" and it makes writing code much safer:
> you can always be sure that whatever changes you make within the
> body of the function, stay inside the body of the function.
>

> #### Tip: Function scope {.callout}
>
> Another important concept is scoping: any variables (or functions!) you
> create or modify inside the body of a function only exist for the lifetime
> of the function's execution. When we call `calcGDP`, the variables `dat`,
> `gdp` and `new` only exist inside the body of the function. Even if we
> have variables of the same name in our interactive R session, they are
> not modified in any way when executing a function.
>


~~~{.r}
  gdp <- dat$pop * dat$gdpPercap
  new <- cbind(dat, gdp=gdp)
  return(new)
~~~

Finally, we calculated the GDP on our new subset, and created a new
data frame with that column added. This means when we call the function
later we can see the context for the returned GDP values,
which is much better than in our first attempt where we just got a vector of numbers.


> ## Tip {.callout}
>
> R has some unique aspects that can be exploited when performing
> more complicated operations. We will not be writing anything that requires
> knowledge of these more advanced concepts. In the future when you are
> comfortable writing functions in R, you can learn more by reading the
> [R Language Manual][man] or this [chapter][] from
> [Advanced R Programming][adv-r] by Hadley Wickham. For context, R uses the
> terminology "environments" instead of frames.

[man]: http://cran.r-project.org/doc/manuals/r-release/R-lang.html#Environment-objects
[chapter]: http://adv-r.had.co.nz/Environments.html
[adv-r]: http://adv-r.had.co.nz/


> #### Tip: Testing and documenting {.callout}
>
> It's important to both test functions and document them:
> Documentation helps you, and others, understand what the
> purpose of your function is, and how to use it, and its
> important to make sure that your function actually does
> what you think.
>
> When you first start out, your workflow will probably look a lot
> like this:
>
>  1. Write a function
>  2. Comment parts of the function to document its behaviour
>  3. Load in the source file
>  4. Experiment with it in the console to make sure it behaves
>     as you expect
>  5. Make any necessary bug fixes
>  6. Rinse and repeat.
>
> Formal documentation for functions, written in separate `.Rd`
> files, gets turned into the documentation you see in help
> files. The [roxygen2][] package allows R coders to write documentation alongside
> the function code and then process it into the appropriate `.Rd` files.
> You will want to switch to this more formal method of writing documentation
> when you start writing more complicated R projects.
>
> Formal automated tests can be written using the [testthat][] package.

[roxygen2]: http://cran.r-project.org/web/packages/roxygen2/vignettes/rd.html
[testthat]: http://r-pkgs.had.co.nz/tests.html

<!---

## Challenge solutions

> #### Solution to challenge 1 {.challenge}
>
> Write a function called `kelvin_to_celsius` that takes a temperature in Kelvin
> and returns that temperature in Celsius
>
> 
> ~~~{.r}
> kelvin_to_celsius <- function(temp) {
>  celsius <- temp - 273.15
>  return(celsius)
> }
> ~~~


> #### Solution to challenge 2 {.challenge}
>
> Define the function to convert directly from Fahrenheit to Celsius,
> by reusing these two functions above
>
>
> 
> ~~~{.r}
> fahr_to_celsius <- function(temp) {
>   temp_k <- fahr_to_kelvin(temp)
>   result <- kelvin_to_celsius(temp_k)
>   return(result)
> }
> ~~~
>

> #### Solution to challenge 3 {.challenge}
> 
>
>  Write a function called `fence` that takes two vectors as arguments, called
> `text` and `wrapper`, and prints out the text wrapped with the `wrapper`:
>
> 
> ~~~{.r}
> fence <- function(text, wrapper){
>   text <- c(wrapper, text, wrapper)
>   result <- paste(text, collapse = " ")
>   return(result)
> }
> best_practice <- c("Write", "programs", "for", "people", "not", "computers")
> fence(text=best_practice, wrapper="***")
> ~~~
> 
> 
> 
> ~~~{.output}
> [1] "*** Write programs for people not computers ***"
> 
> ~~~
> 

-->