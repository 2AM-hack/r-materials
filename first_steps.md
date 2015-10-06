# Getting started
Najko Jahn  
3. October 2015  

Attribution: Adapted from the  [Data Carpentry R intro material]( https://github.com/datacarpentry/r-ecology)

# Expected outcome

* R installation running
* participants are familiar with RStudio
* Installing packages
* Passing vectors to functions


# Installing R

R is available for Linux, Mac and Windows users. Many Linux distributions already have R installed.

1. Download R from the R Archive Network CRAN:

<https://cran.r-project.org/>

2 . Download RStudio:

<https://www.rstudio.com/products/rstudio/download/>

RStudio is a powerful Integrated Development Environment (IDE) for the R language. It helps you to write, store and share your coding activities. RStudio also provide syntax highlighting and code completion.

# RStudio overview

* Interactively run commands in the console
* Source code editor
* Workspace Environment
* File Browser
* Integrated help

**TASK 1 Create a working directory `alm_hack`**

# Packages

R comes with more than 20 essential packages. However, for many task, you will find it useful to check, if someone already has contributed her solution as a package to the R community. R packages are available through CRAN.

<https://cran.r-project.org/web/packages/available_packages_by_name.html>

Packages can be installed with `ìnstall.packages()`.

Example, installing `devtools`package from the RStudio mirror.


```r
install.packages("devtools",  repos="http://cran.rstudio.com/")
```

To load a package, type:


```r
library(devtools)
```

```
## Warning: package 'devtools' was built under R version 3.2.2
```

Please note, packages need to be loaded with every new session.

To get familiar with what a package offers, please read the vignettes and documentation.

Sometimes, packages are only available on GitHub. The `devtools` package makes it possible to install from GitHub. For instance, we want to use the [rOpenSci client](https://github.com/ropensci/rorcid) for the ORCID API.


```r
devtools::install_github("ropensci/rorcid")
library(rorcid)
```

**TASK 2: Choose one package from the rOpenSci initative: https://ropensci.org/packages/. Download the package from CRAN or, if it is not available on CRAN, from GitHub.**

# R language essentials

## R as a calculator


```r
(1 + 3) ^ 2
```

```
## [1] 16
```

```r
sqrt(64)
```

```
## [1] 8
```

```r
log(2)
```

```
## [1] 0.6931472
```

## Vectors

### Numeric


```r
my_data <- c(1, 3, 5, 9)
my_data
```

```
## [1] 1 3 5 9
```

```r
sum(my_data)
```

```
## [1] 18
```

```r
mean(my_data)
```

```
## [1] 4.5
```

Generate 100 uniform random numbers between 1 and 5.


```r
my_sample <- runif(100, 1, 5)
```

### Character


```r
my_friends <- c("John", "Martin", "Sue", "Linda")
your_friends <- c("John", "Rita", "Paul", "Sue")
```

Get the third element in `my_friends`


```r
my_friends[3]
```

```
## [1] "Sue"
```

Exclude the first element


```r
my_friends[-1]
```

```
## [1] "Martin" "Sue"    "Linda"
```

# Passing vectors to functions


How many elements are in a vector?


```r
length(your_friends)
```

```
## [1] 4
```

R offers a wide range of mathematical functions. For instance, if you want to calculate the intersection between `my_friends` and `your_friends` try `ìntersect`.


```r
intersect(my_friends, your_friends)
```

```
## [1] "John" "Sue"
```

To calculate the square root of each element in `my_data`


```r
sqrt(my_data)
```

```
## [1] 1.000000 1.732051 2.236068 3.000000
```

What type is the vector?


```r
class(your_friends)
```

```
## [1] "character"
```

```r
class(my_data)
```

```
## [1] "numeric"
```

Check, if vector is of type character


```r
is.character(my_friends)
```

```
## [1] TRUE
```

```r
is.character(my_data)
```

```
## [1] FALSE
```

We just saw 3 of the 6 **data types** that R uses: `"character"`
`"numeric"` and `"logical"` for `TRUE` and `FALSE` (the Boolean data type). The other 3 are:

* `"integer"` for integer numbers (e.g., `2L`, the `L` indicates to R that it's an integer)
* `"complex"` to represent complex numbers with real and imaginary parts (e.g.,
  `1+4i`) and that's all we're going to say about them
* `"raw"` that we won't discuss further

Vectors are one of the many **data structures** that R uses. Other important
ones are lists (`list`), matrices (`matrix`), data frames (`data.frame`) and
factors (`factor`).

In this course, we will only work with `data.frame`.
 
**Task 3: Create two vectors: One of type character and one of type numeric. Get the number of elements for each vector. **

**Task 4:  Assign 500 uniform random numbers on the interval `[-2, 9]` to a vector `a` and calculate the mean value**




