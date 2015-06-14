---
layout: page
title: R for reproducible scientific analysis
subtitle: Introduction to R and RStudio
minutes: 30
---


> ## Learning Objectives {.objectives}
>
> * To get familiar with the RStudio interface
> * To get familiar with the buttons, shortcuts and options in Rstudio
> * To understand R arithmetical and relational operations
> * To understand variables and value assignment 


### Introduction to RStudio

This lesson focuses on the fundamentals of R and [RStudio](http://www.rstudio.com/). 
The latter one is a free, open source R integrated development environment. It provides 
a built in editor, works on all platforms (including servers) and provides many 
advantages, such as integration with version control and project management.

### Basic layout

When you first open RStudio, you will find three panels:

  * The interactive R Console (lower left)
  * The Environments (Workspace/History) (upper right)
  * The Files/Plots/Packages/Help (lower right)

Once you open files, such as R scripts, a scripting panel will also appear on the top left side.


## The interactive R console and introduction to R

A lot of your time in R will be spent on the R interactive console. This is where you
will run all of your code, and can be a useful environment to try out ideas. This console 
in RStudio is the same as the one you would get if you just typed in `R` in your 
command line environment.

The first thing you will see in the R interactive session is a bunch of information,
followed by a ">" and a blinking cursor. In many ways this is similar to the shell
environment: you type in commands, R tries to execute them, and
then returns a result.

### Using R as a calculator

The simplest thing you could do with R is do arithmetic:


~~~{.r}
1 + 100
~~~



~~~{.output}
[1] 101

~~~

And R will print out the answer, with a preceding "[1]". Don't worry about this
for now, we'll explain that later. For now think of it as indicating output.

Just like bash, if you type in an incomplete command, R will wait for you to
complete it:

~~~ {.r}
1 +
~~~

~~~ {.output}
+
~~~

Any time you hit return and the R session shows a "+" instead of a ">", it
means it's waiting for you to complete the command. If you want to cancel
a command you can simply hit "Esc" and RStudio will give you back the ">"
prompt.

> #### Tip: Cancelling commands {.callout}
>
> If you're using R from the command line instead of from within RStudio,
> you need to use `Ctrl+C` instead of `Esc` to cancel the command.
>
> Cancelling a command isn't just useful for killing incomplete commands:
> you can also use it to tell R to stop running code (for example if its
> taking much longer than you'd expect), or to delete the command you're
> currently writing.
>

When using R as a calculator, the order of operations is the same as you
would have learnt back in school.

From highest to lowest precedence:

 * Parentheses: `(`, `)`
 * Exponents: `^` or `**`
 * Divide: `/`
 * Multiply: `*`
 * Add: `+`
 * Subtract: `-`


~~~{.r}
3 + 5 * 2
~~~



~~~{.output}
[1] 13

~~~

Use parentheses to group to force the order of evaluation
if it differs from the default, or to set your own order.


~~~{.r}
(3 + 5) * 2
~~~



~~~{.output}
[1] 16

~~~

But this can get unwieldy when not needed:


~~~{.r}
(3 + (5 * (2 ^ 2))) # hard to read
3 + 5 * 2 ^ 2       # easier to read, once you know rules
3 + 5 * (2 ^ 2)     # if you forget some rules, this might help
~~~


The text I've typed after each line of code is called a comment. Anything that
follows on from the hash symbol `#` is ignored by R when it executes code.


> ## Tip {.callout}
>
> It is useful to document our code in this way so that others (and us 
> the next time we read it) have an easier time following what the code 
> is doing. Same applies to us next time we use the code.


Really small or large numbers get a scientific notation:


~~~{.r}
2/10000
~~~



~~~{.output}
[1] 2e-04

~~~

Which is shorthand for "multiplied by `10^XX`". So `2e-4`
is shorthand for `2 * 10^(-4)`.

You can write numbers in scientific notation too:


~~~{.r}
5e3  # Note the lack of minus here
~~~



~~~{.output}
[1] 5000

~~~

> #### Challenge 1 {.challenge}
>
> In the R console type:
>
> ~~~{.r}
> 1/0
> 0/0
> ~~~
>
> Can R handle division by 0?
> Does R throw an error? If not, what are the results of the above calculations?


#### Introduction to R built in functions

A function is a sequence of program instructions that perform a specific task, 
packaged as a unit. This unit can then be used in programs wherever that particular 
task should be performed.

R has many built in functions, a subset of which perform mathematical operations.
To call a function, we simply type the function name, followed by an open and closing
parenthesis. Anything we type inside those parentheses is called arguments and define 
the behaviour/output of the function.

To get a list of all R built in functions type:

~~~{.r}
builtins()  # lists R built in functions
~~~


~~~{.r}
sin(1)  # trigonometry functions
~~~



~~~{.output}
[1] 0.841471

~~~


~~~{.r}
log(1)  # natural logarithm
~~~



~~~{.output}
[1] 0

~~~


~~~{.r}
log10(10) # base-10 logarithm
~~~



~~~{.output}
[1] 1

~~~


~~~{.r}
exp(0.5) # e^(1/2)
~~~



~~~{.output}
[1] 1.648721

~~~


~~~{.r}
max(5, 0, Inf, 4, 6) # Return the maximum number
~~~



~~~{.output}
[1] Inf

~~~


Don't worry about trying to remember every function in R. You
can simply look them up on google, or if you can remember the
start of the function's name, use the tab completion in RStudio.

This is one advantage that RStudio has over R on its own, it
has autocompletion abilities that allow you to more easily
look up functions, their arguments, and the values that they
take.


#### Relational operations

We can also do comparison in R:


~~~{.r}
1 == 1  # equality (note two equals signs, read as "is equal to")
~~~



~~~{.output}
[1] TRUE

~~~


~~~{.r}
1 != 2  # inequality (read as "is not equal to")
~~~



~~~{.output}
[1] TRUE

~~~


~~~{.r}
1 <  2  # less than
~~~



~~~{.output}
[1] TRUE

~~~


~~~{.r}
1 <= 1  # less than or equal to
~~~



~~~{.output}
[1] TRUE

~~~


~~~{.r}
1 > 0  # greater than
~~~



~~~{.output}
[1] TRUE

~~~


~~~{.r}
1 >= -9 # greater than or equal to
~~~



~~~{.output}
[1] TRUE

~~~

> #### Tip: Comparing Numbers {.callout}
>
> A word of warning about comparing numbers: you should
> never use `==` to compare two numbers unless they are
> integers (a data type which can specifically represent
> only whole numbers).
>
> Computers may only represent decimal numbers with a
> certain degree of precision, so two numbers which look
> the same when printed out by R, may actually have
> different underlying representations and therefore be
> different by a small margin of error (called Machine
> numeric tolerance).
>
> Instead you should use the `all.equal` function.
>
> Further reading: [http://floating-point-gui.de/](http://floating-point-gui.de/)
>


#### Variables and value assignment

We can store values in variables using the assignment operator `<-`, like this:


~~~{.r}
x <- 1/40
~~~

Notice that assignment does not print a value. Instead, we stored it for later
in something called a **variable**. `x` now contains the **value** `0.025`:


~~~{.r}
x
~~~



~~~{.output}
[1] 0.025

~~~

More precisely, the stored value is a *decimal approximation* of
this fraction called a [floating point number](http://en.wikipedia.org/wiki/Floating_point).

Look for the `Environment` tab in one of the panes of RStudio, and you will see that `x` and its value
have appeared. Our variable `x` can be used in place of a number in any calculation that expects a number:


~~~{.r}
log(x)
~~~



~~~{.output}
[1] -3.688879

~~~

Notice also that variables can be reassigned:


~~~{.r}
x <- 100
~~~

`x` used to contain the value 0.025 and and now it has the value 100.

Assignment values can contain the variable being assigned to:


~~~{.r}
x <- x + 1 #notice how RStudio updates its description of x on the top right tab
~~~

The right hand side of the assignment can be any valid R expression.
The right hand side is *fully evaluated* before the assignment occurs.

Variable names can contain letters, numbers, underscores and periods. They
cannot start with a number nor contain spaces at all. Different people use
different conventions for long variable names, these include

  * periods.between.words
  * underscores\_between_words
  * camelCaseToSeparateWords

What you use is up to you, but **be consistent**.

It is also possible to use the `=` operator for assignment:


~~~{.r}
x = 1/40
~~~

But this is much less common among R users.  The most important thing is to
**be consistent** with the operator you use. There are occasionally places
where it is less confusing to use `<-` than `=`, and it is the most common
symbol used in the community. So the recommendation is to use `<-`.

#### Managing your environment

There are a few useful commands you can use to interact with the R session.

`ls` will list all of the variables and functions stored in the global environment
(your working R session):


~~~{.r}
ls()
~~~



~~~{.output}
[1] "x"       

~~~

> #### Tip: hidden objects {.callout}
>
> Just like in the shell, `ls` will hide any variables or functions starting
> with a "." by default. To list all objects, type `ls(all.names=TRUE)`
> instead
>

Note here that we didn't given any arguments to `ls`, but we still needed to give
the brackets to tell R to call the function.

If we type `ls` by itself, R will print out the source code for that function!


~~~{.r}
ls
~~~



~~~{.output}
function (name, pos = -1L, envir = as.environment(pos), all.names = FALSE, 
    pattern) 
{
    if (!missing(name)) {
        nameValue <- try(name, silent = TRUE)
        if (identical(class(nameValue), "try-error")) {
            name <- substitute(name)
            if (!is.character(name)) 
                name <- deparse(name)
            warning(gettextf("%s converted to character string", 
                sQuote(name)), domain = NA)
            pos <- name
        }
        else pos <- nameValue
    }
    all.names <- .Internal(ls(envir, all.names))
    if (!missing(pattern)) {
        if ((ll <- length(grep("[", pattern, fixed = TRUE))) && 
            ll != length(grep("]", pattern, fixed = TRUE))) {
            if (pattern == "[") {
                pattern <- "\\["
                warning("replaced regular expression pattern '[' by  '\\\\['")
            }
            else if (length(grep("[^\\\\]\\[<-", pattern))) {
                pattern <- sub("\\[<-", "\\\\\\[<-", pattern)
                warning("replaced '[<-' by '\\\\[<-' in regular expression pattern")
            }
        }
        grep(pattern, all.names, value = TRUE)
    }
    else all.names
}
<bytecode: 0x7fd893942358>
<environment: namespace:base>

~~~

You can use `rm` to delete objects you no longer need:


~~~{.r}
rm(x)
~~~

If you have lots of things in your environment and want to delete all of them,
you can pass the results of `ls` to the `rm` function:


~~~{.r}
rm(list = ls())
~~~

In this case we've combined the two. Just like the order of operations, anything
inside the innermost brackets is evaluated first, and so on.

In this case we've specified that the results of `ls` should be used for the
`list` argument in `rm`. When assigning values to arguments by name, you *must*
use the `=` operator!!

If instead we use `<-`, there will be unintended side effects, or you may just
get an error message:


~~~{.r}
rm(list <- ls())
~~~



~~~{.output}
Error in rm(list <- ls()): ... must contain names or character strings

~~~

> #### Tip: Warnings vs. Errors {.callout}
>
> Pay attention when R does something unexpected! Errors, like above,
> are thrown when R cannot proceed with a calculation. Warnings on the
> other hand usually mean that the function has run, but it probably
> hasn't worked as expected.
>
> In both cases, the message that R prints out usually give you clues
> on how to fix a problem.
>


#### Work flow within Rstudio
There are two main ways one can work within Rstudio.

1. Run single commands within the interactive R console.
  1.  This works well when testing small chunck of code.
  2.  Becomes quickly laboursome and unreproducible.
2. Type the commands in .R files in the script editor and use Rstudio's 
command/short cut to run a current line or selected lines on the interactive R console.
  1. This way all commands are saved for later reference/run.

> #### Tip: Pushing to the interactive R console {.callout}
> To run the current line click on the `Run` button just above the file pane. Or use the 
> `Ctrl-Enter` short cut, which can be see by hovering the mouse over the button.
>
> To run a block of code, select it and then `Run`. If you have modified a line
> of code within a block of code you have just run, there is no need to reselect the section 
> and press `Run`. Instead you can use the next button along, `Re-run the previous region`, 
> which will run the previous code block but with the modifications you have just made.
>

If R is ready to accept commands, the R console shows a `>` prompt. If it
receives a command (by typing, copy-pasting or sent from the script editor using
`Ctrl-Enter`), R will try to execute it, and when ready, show the results and
come back with a new `>`-prompt to wait for new commands.

If R is still waiting for you to enter more data because it isn't complete yet,
the console will show a `+` prompt. It means that you haven't finished entering
a complete command. This is because you have not 'closed' a parenthesis or
quotation. If you're in RStudio and this happens, click inside the console
window and press `Esc`; this should help you out of trouble.

> #### Tip: Switching between script and control consoles {.callout}
> At some point in your analysis you may want to check the content of a variable 
> without necessarily adding the command to your script. To avoid that you can type 
> these commands directly on the interactive console. RStudio provides the `Ctrl-1` 
> and `Ctrl-2` short cuts that allow you to jump between the script and theconsoles.
>

> #### Challenge 1 {.challenge}
>
> What are the values of each variable after each
> statement in the following program:
>
> 
> ~~~{.r}
> mass <- 47.5
> age <- 122
> mass <- mass * 2.3
> age <- age - 20
> ~~~
>

> #### Challenge 2 {.challenge}
>
> Run the code from the previous challenge, and write a command to
> compare mass to age. Is mass larger than age?
>

> #### Challenge 3 {.challenge}
>
> Clean up your working environment by deleting the mass and age
> variables.
>

