---
layout: page
title: R for reproducible scientific analysis
subtitle: Seeking help
minutes: 15
---




> ## Learning objectives {.objectives}
>
> * To know where to look for help.
> * To become familiar with R help files for functions and special 
operators.
> * To be able to use CRAN task views to identify packages to solve a problem.
> * To be able to seek help from your peers
>

### Reading Help files

R and add-on packages provide help files for functions. To load the help page for a specific function:


~~~{.r}
?function_name
help(function_name)
~~~

These functions will display the requested help page at the bottom left panel in RStudio (or as plain text in R).

Each help page is broken down into sections:

 - Description: an extended description of what the function does.
 - Usage: the arguments of the function and their default values.
 - Arguments: an explanation of the data each argument expects.
 - Details: any important details to be aware of.
 - Value: the data the function returns and in which type.
 - See Also: any related functions you might find useful.
 - Examples: some examples on how to use the function.

Different functions might have different sections, but these are the main ones you should be aware of.

> #### Tip: Reading help files {.callout}
>
> One of the most daunting aspects of R is the large number of functions
> available. It is impossible to remember the
> correct usage for every function you use. Luckily, the help files
> mean you don't have to!
>

### Special Operators

To seek help on special operators, use quotes:


~~~{.r}
?"+"
~~~

### Getting help on packages

Many packages come with "vignettes": tutorials and extended example documentation.
Without any arguments, `vignette()` will list all vignettes for all installed packages;
`vignette(package="package-name")` will list all available vignettes for
`package-name`, and `vignette("vignette-name")` will open the specified vignette.

If a package doesn't have any vignettes, you can usually find help by typing
`help("package-name")`.

### When you kind of remember the function

If you're not sure what package a function is in, or how it's specifically spelled you can do a fuzzy search:


~~~{.r}
??function_name
~~~

### When you have no idea where to begin

If you don't know what function or package you need to use
[CRAN Task Views](http://cran.at.r-project.org/web/views)
is a specially maintained list of packages grouped into
fields. This can be a good starting point.

### When your code doesn't work: seeking help from your peers

If you're having trouble using a function, 9 times out of 10,
the answers you are seeking have already been answered on
[Stack Overflow](http://stackoverflow.com/). You can search using
the `[r]` tag.

If you can't find the answer, there are a few useful functions to
help you ask a question from your peers:


~~~{.r}
?dput
~~~

Will dump the data you're working with into a format so that it can
be copied and pasted by anyone else into their R session.


~~~{.r}
sessionInfo()
~~~



~~~{.output}
R version 3.2.0 (2015-04-16)
Platform: x86_64-apple-darwin13.4.0 (64-bit)
Running under: OS X 10.9.5 (Mavericks)

locale:
[1] en_GB.UTF-8/en_GB.UTF-8/en_GB.UTF-8/C/en_GB.UTF-8/en_GB.UTF-8

attached base packages:
[1] stats4    parallel  stats     graphics  grDevices utils     datasets 
[8] methods   base     

other attached packages:
[1] knitr_1.10.12

loaded via a namespace (and not attached):
 [1] XML_3.98-1.2         digest_0.6.8         bitops_1.0-6        
 [7] rmarkdown_0.7        tools_3.2.0          Biobase_2.28.0      
[10] RCurl_1.95-4.6       yaml_2.1.13          htmltools_0.2.6     

~~~

Will print out your current version of R, as well as any packages you
have loaded. This can be useful for others to help reproduce and debug
your issue.

> #### Challenge 1 {.challenge}
> 
> Look at the help for the `paste` function. You'll need to use this later. 
> What is the difference between the `sep` and `collapse` arguments?
> 

### Other ports of call

* [Quick R](http://www.statmethods.net/)
* [RStudio cheat sheets](http://www.rstudio.com/resources/cheatsheets/)
* [Cookbook for R](http://www.cookbook-r.com/)

## Challenge solutions

> #### Solution to challenge 1 {.challenge}
> 
> Look at the help for the `paste` function. You'll need to use this later. 
> 
> 
> ~~~{.r}
> help("paste")
> ?paste
> ~~~
>
