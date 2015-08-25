---
layout: page
title: Programming with R
subtitle: Data types and structures
minutes: 45
output: 
  html_document: 
    keep_md: yes
---

> ## Learning Objectives {.objectives}
>
> * Expose learners to the different data types in R
> * Learn how to create vectors of different types
> * Be able to check the type of vector
> * Learn about missing data and other special values
> * Getting familiar with the different data structures (lists, matrices, data frames)

### Understanding Basic Data Types in R

To make the best of the R language, you'll need a strong understanding of the
basic data types and data structures and how to operate on those.

Very important to understand because these are the objects you will manipulate
on a day-to-day basis in R. Dealing with object conversions is one of the most
common sources of frustration for beginners.

**Everything** in R is an object.

R has 6 (although we will not discuss the raw class for this workshop) atomic
vector types.

* character
* numeric (real or decimal)
* integer
* logical
* complex

By *atomic*, we mean the vector only holds data of a single type.

* **character**: `"a"`, `"swc"`
* **numeric**: `2`, `15.5`
* **integer**: `2L` (the `L` tells R to store this as an integer)
* **logical**: `TRUE`, `FALSE`
* **complex**: `1+4i` (complex numbers with real and imaginary parts)

R provides many functions to examine features of vectors and other objects, for
example

* `class()` - what kind of object is it (high-level)?
* `typeof()` - what is the object's data type (low-level)?
* `length()` - how long is it? What about two dimensional objects?
* `attributes()` - does it have any metadata?


```r
# Example
x <- "bananas"
typeof(x)
```

```
## [1] "character"
```

```r
attributes(x)
```

```
## NULL
```

```r
y <- 1:10
y
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
typeof(y)
```

```
## [1] "integer"
```

```r
length(y)
```

```
## [1] 10
```

```r
z <- as.numeric(y)
z
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
typeof(z)
```

```
## [1] "double"
```

R has many __data structures__. These include

* atomic vector
* list
* matrix
* data frame
* factors

### Atomic Vectors

A vector is the most common and basic data structure in R and is pretty much the
workhorse of R. Technically, vectors can be one of two types:

* atomic vectors
* lists

although the term "vector" most commonly refers to the atomic types not to lists.

### The Different Vector Modes

A vector is a collection of elements that are most commonly of mode `character`,
`logical`, `integer` or `numeric`.

You can create an empty vector with `vector()`. (By default the mode is
`logical`. You can be more explicit as shown in the examples below.) It is more
common to use direct constructors such as `character()`, `numeric()`, etc.


```r
vector() # an empty 'logical' (the default) vector
```

```
## logical(0)
```

```r
vector("character", length = 5) # a vector of mode 'character' with 5 elements
```

```
## [1] "" "" "" "" ""
```

```r
character(5) # the same thing, but using the constructor directly
```

```
## [1] "" "" "" "" ""
```

```r
numeric(5)   # a numeric vector with 5 elements
```

```
## [1] 0 0 0 0 0
```

```r
logical(5)   # a logical vector with 5 elements
```

```
## [1] FALSE FALSE FALSE FALSE FALSE
```

You can also create vectors by directly specifying their content. R will then
guess the appropriate mode of storage for the vector. For instance:


```r
x <- c(1, 2, 3)
```

will create a vector `x` of mode `numeric`. These are the most common kind, and
are treated as double precision real numbers. If you wanted to explicitly create
integers, you need to add an `L` to each element (or *coerce* to the integer
type using `as.integer()`).


```r
x1 <- c(1L, 2L, 3L)
```

Using `TRUE` and `FALSE` will create a vector of mode `logical`:


```r
y <- c(TRUE, TRUE, FALSE, FALSE)
```

While using quoted text will create a vector of mode `character`:


```r
z <- c("Sarah", "Tracy", "Jon")
```

### Examining Vectors

The functions `typeof()`, `length()`, `class()` and `str()` provide useful
information about your vectors and R objects in general.


```r
typeof(z)
```

```
## [1] "character"
```

```r
length(z)
```

```
## [1] 3
```

```r
class(z)
```

```
## [1] "character"
```

```r
str(z)
```

```
##  chr [1:3] "Sarah" "Tracy" "Jon"
```

> ## Challenge - Finding commonalities {.challenge}
>
> Do you see a property that's common to all these vectors above?

### Adding Elements

The function `c()` (for combine) can also be used to add elements to a vector.


```r
z <- c(z, "Annette")
z
```

```
## [1] "Sarah"   "Tracy"   "Jon"     "Annette"
```

```r
z <- c("Greg", z)
z
```

```
## [1] "Greg"    "Sarah"   "Tracy"   "Jon"     "Annette"
```

### Vectors from a Sequence of Numbers

You can create vectors as a sequence of numbers.


```r
series <- 1:10
seq(10)
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10
```

```r
seq(from = 1, to = 10, by = 0.1)
```

```
##  [1]  1.0  1.1  1.2  1.3  1.4  1.5  1.6  1.7  1.8  1.9  2.0  2.1  2.2  2.3
## [15]  2.4  2.5  2.6  2.7  2.8  2.9  3.0  3.1  3.2  3.3  3.4  3.5  3.6  3.7
## [29]  3.8  3.9  4.0  4.1  4.2  4.3  4.4  4.5  4.6  4.7  4.8  4.9  5.0  5.1
## [43]  5.2  5.3  5.4  5.5  5.6  5.7  5.8  5.9  6.0  6.1  6.2  6.3  6.4  6.5
## [57]  6.6  6.7  6.8  6.9  7.0  7.1  7.2  7.3  7.4  7.5  7.6  7.7  7.8  7.9
## [71]  8.0  8.1  8.2  8.3  8.4  8.5  8.6  8.7  8.8  8.9  9.0  9.1  9.2  9.3
## [85]  9.4  9.5  9.6  9.7  9.8  9.9 10.0
```

### Missing Data

R supports missing data in vectors. They are represented as `NA` (Not Available)
and can be used for all the vector types covered in this lesson:


```r
x <- c(0.5, NA, 0.7)
x <- c(TRUE, FALSE, NA)
x <- c("a", NA, "c", "d", "e")
x <- c(1+5i, 2-3i, NA)
```

The function `is.na()` indicates the elements of the vectors that represent
missing data, and the function `anyNA()` returns `TRUE` if the vector contains
any missing values:


```r
x <- c("a", NA, "c", "d", NA)
y <- c("a", "b", "c", "d", "e")
is.na(x)
```

```
## [1] FALSE  TRUE FALSE FALSE  TRUE
```

```r
is.na(y)
```

```
## [1] FALSE FALSE FALSE FALSE FALSE
```

```r
anyNA(x)
```

```
## [1] TRUE
```

```r
anyNA(y)
```

```
## [1] FALSE
```

### Other Special Values

`Inf` is infinity. You can have either positive or negative infinity.


```r
1/0
```

```
## [1] Inf
```

`NaN` means Not a Number. It's an undefined value.


```r
0/0
```

```
## [1] NaN
```

### What Happens When You Mix Types Inside a Vector?

R will create a resulting vector with a mode that can most easily accommodate
all the elements it contains. This conversion between modes of storage is called
"coercion". When R converts the mode of storage based on its content, it is
referred to as "implicit coercion". For instance, can you guess what the
following do (without running them first)?


```r
xx <- c(1.7, "a")
xx <- c(TRUE, 2)
xx <- c("a", TRUE)
```

You can also control how vectors are coerced explicitly using the
`as.<class_name>()` functions:


```r
as.numeric("1")
```

```
## [1] 1
```

```r
as.character(1:2)
```

```
## [1] "1" "2"
```

### Objects Attributes

Objects can have __attributes__. Attributes are part of the object. These include:

* names
* dimnames
* dim
* class
* attributes (contain metadata)

You can also glean other attribute-like information such as length (works on
vectors and lists) or number of characters (for character strings).


```r
length(1:10)
```

```
## [1] 10
```

```r
nchar("Software Carpentry")
```

```
## [1] 18
```

### Matrix

In R matrices are an extension of the numeric or character vectors. They are not
a separate type of object but simply an atomic vector with dimensions; the
number of rows and columns.


```r
m <- matrix(nrow = 2, ncol = 2)
m
```

```
##      [,1] [,2]
## [1,]   NA   NA
## [2,]   NA   NA
```

```r
dim(m)
```

```
## [1] 2 2
```

Matrices in R are filled column-wise.


```r
m <- matrix(1:6, nrow = 2, ncol = 3)
```

Other ways to construct a matrix


```r
m      <- 1:10
dim(m) <- c(2, 5)
```

This takes a vector and transforms it into a matrix with 2 rows and 5 columns.

Another way is to bind columns or rows using `cbind()` and `rbind()`.


```r
x <- 1:3
y <- 10:12
cbind(x, y)
```

```
##      x  y
## [1,] 1 10
## [2,] 2 11
## [3,] 3 12
```

```r
rbind(x, y)
```

```
##   [,1] [,2] [,3]
## x    1    2    3
## y   10   11   12
```

You can also use the `byrow` argument to specify how the matrix is filled. From R's own documentation:


```r
mdat <- matrix(c(1,2,3, 11,12,13), nrow = 2, ncol = 3, byrow = TRUE)
mdat
```

```
##      [,1] [,2] [,3]
## [1,]    1    2    3
## [2,]   11   12   13
```

### List

In R lists act as containers. Unlike atomic vectors, the contents of a list are
not restricted to a single mode and can encompass any mixture of data
types. Lists are sometimes called generic vectors, because the elements of a
list can by of any type of R object, even lists containing further lists. This
property makes them fundamentally different from atomic vectors.

A list is a special type of vector. Each element can be a different type.

Create lists using `list()` or coerce other objects using `as.list()`. An empty
list of the required length can be created using `vector()`


```r
x <- list(1, "a", TRUE, 1+4i)
x
```

```
## [[1]]
## [1] 1
## 
## [[2]]
## [1] "a"
## 
## [[3]]
## [1] TRUE
## 
## [[4]]
## [1] 1+4i
```

```r
x <- vector("list", length = 5) ## empty list
length(x)
```

```
## [1] 5
```

```r
x[[1]]
```

```
## NULL
```

```r
x <- 1:10
x <- as.list(x)
length(x)
```

```
## [1] 10
```

1. What is the class of `x[1]`?
2. What about `x[[1]]`?


```r
xlist <- list(a = "Karthik Ram", b = 1:10, data = head(iris))
xlist
```

```
## $a
## [1] "Karthik Ram"
## 
## $b
##  [1]  1  2  3  4  5  6  7  8  9 10
## 
## $data
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

1. What is the length of this object? What about its structure?

Lists can be extremely useful inside functions. You can “staple” together lots
of different kinds of results into a single object that a function can return.

A list does not print to the console like a vector. Instead, each element of the
list starts on a new line.

Elements are indexed by double brackets. Single brackets will still return
a(nother) list.


### Data Frame

A data frame is a very important data type in R. It's pretty much the *de facto*
data structure for most tabular data and what we use for statistics.

A data frame is a special type of list where every element of the list has same length.

Data frames can have additional attributes such as `rownames()`, which can be
useful for annotating data, like `subject_id` or `sample_id`. But most of the
time they are not used.

Some additional information on data frames:

* Usually created by `read.csv()` and `read.table()`.
* Can convert to matrix with `data.matrix()` (preferred) or `as.matrix()`
* Coercion will be forced and not always what you expect.
* Can also create with `data.frame()` function.
* Find the number of rows and columns with `nrow(dat)` and `ncol(dat)`, respectively.
* Rownames are usually 1, 2, ..., n.

### Creating Data Frames by Hand

To create data frames by hand:


```r
dat <- data.frame(id = letters[1:10], x = 1:10, y = 11:20)
dat
```

```
##    id  x  y
## 1   a  1 11
## 2   b  2 12
## 3   c  3 13
## 4   d  4 14
## 5   e  5 15
## 6   f  6 16
## 7   g  7 17
## 8   h  8 18
## 9   i  9 19
## 10  j 10 20
```

> ## Useful data frame functions {.callout}
>
> * `head()` - shown first 6 rows
> * `tail()` - show last 6 rows
> * `dim()` - returns the dimensions
> * `nrow()` - number of rows
> * `ncol()` - number of columns
> * `str()` - structure of each column
> * `names()` - shows the `names` attribute for a data frame, which gives the
>column names.

See that it is actually a special list:


```r
is.list()
```

```
## Error in is.list(): 0 arguments passed to 'is.list' which requires 1
```

```r
class(iris)
```

```
## [1] "data.frame"
```

| Dimensions | Homogenous | Heterogeneous |
| ------- | ---- | ---- |
| 1-D | atomic vector | list |
| 2-D | matrix | data frame |

Factors are used to represent categorical data. Factors can be ordered or
unordered and are an important class for statistical analysis and for plotting.

Factors are stored as integers, and have labels associated with these unique
integers. While factors look (and often behave) like character vectors, they are
actually integers under the hood, and you need to be careful when treating them
like strings.

Once created, factors can only contain a pre-defined set values, known as
*levels*. By default, R always sorts *levels* in alphabetical order. For
instance, if you have a factor with 2 levels:

> ## Tip {.callout}
>
> The `factor()` command is used to create and modify factors in R


```r
sex <- factor(c("male", "female", "female", "male"))
```

R will assign `1` to the level `"female"` and `2` to the level `"male"` (because
`f` comes before `m`, even though the first element in this vector is
`"male"`). You can check this by using the function `levels()`, and check the
number of levels using `nlevels()`:


```r
levels(sex)
```

```
## [1] "female" "male"
```

```r
nlevels(sex)
```

```
## [1] 2
```

Sometimes, the order of the factors does not matter, other times you might want
to specify the order because it is meaningful (e.g., "low", "medium", "high") or
it is required by particular type of analysis. Additionally, specifying the
order of the levels allows us to compare levels:


```r
food <- factor(c("low", "high", "medium", "high", "low", "medium", "high"))
levels(food)
```

```
## [1] "high"   "low"    "medium"
```

```r
food <- factor(food, levels=c("low", "medium", "high"))
levels(food)
```

```
## [1] "low"    "medium" "high"
```

```r
min(food) ## doesn't work
```

```
## Error in Summary.factor(structure(c(1L, 3L, 2L, 3L, 1L, 2L, 3L), .Label = c("low", : 'min' not meaningful for factors
```

```r
food <- factor(food, levels=c("low", "medium", "high"), ordered=TRUE)
levels(food)
```

```
## [1] "low"    "medium" "high"
```

```r
min(food) ## works!
```

```
## [1] low
## Levels: low < medium < high
```

In R's memory, these factors are represented by numbers (1, 2, 3). They are
better than using simple integer labels because factors are self describing:
`"low"`, `"medium"`, and `"high"`" is more descriptive than `1`, `2`, `3`. Which
is low?  You wouldn't be able to tell with just integer data. Factors have this
information built in. It is particularly helpful when there are many levels
(like the subjects in our example data set).

> ## Challenge - Representing data in R {.challenge}
>
> You have a vector representing levels of exercise undertaken by 5 subjects
>
> **"l","n","n","i","l"** ; n=none, l=light, i=intense
>
> What is the best way to represent this in R?
>
> a) exercise<-c("l","n","n","i","l")
>
> b) exercise<-factor(c("l","n","n","i","l"), ordered=TRUE)
>
> c) exercise<-factor(c("l","n","n","i","l"), levels=c("n","l","i"), ordered=FALSE)
>
> d) exercise<-factor(c("l","n","n","i","l"), levels=c("n","l","i"), ordered=TRUE)

###  Converting Factors

Converting from a factor to a number can cause problems:


```r
f<-factor(c(3.4, 1.2, 5))
as.numeric(f)
```

```
## [1] 2 1 3
```

This does not behave as expected (and there is no warning).

The recommended way is to use the integer vector to index the factor levels:


```r
levels(f)[f]
```

```
## [1] "3.4" "1.2" "5"
```

This returns a character vector, the `as.numeric()` function is still required to convert the values to the proper type (numeric).


```r
f<-levels(f)[f]
f<-as.numeric(f)
```

### Using Factors

Lets load our example data to see the use of factors:


```r
dat<-read.csv(file='data/sample.csv', stringsAsFactors=TRUE)
```

> ## Tip {.callout}
>
> `stringsAsFactors=TRUE` is the default behaviour for R. We could leave this argument out. It is included here for clarity.


```r
str(dat)
```

```
## 'data.frame':	100 obs. of  9 variables:
##  $ ID           : Factor w/ 100 levels "Sub001","Sub002",..: 1 2 3 4 5 6 7 8 9 10 ...
##  $ Gender       : Factor w/ 4 levels "f","F","m","M": 3 3 3 1 3 4 1 3 3 1 ...
##  $ Group        : Factor w/ 3 levels "Control","Treatment1",..: 1 3 3 2 2 3 1 3 3 1 ...
##  $ BloodPressure: int  132 139 130 105 125 112 173 108 131 129 ...
##  $ Age          : num  16 17.2 19.5 15.7 19.9 14.3 17.7 19.8 19.4 18.8 ...
##  $ Aneurisms_q1 : int  114 148 196 199 188 260 135 216 117 188 ...
##  $ Aneurisms_q2 : int  140 209 251 140 120 266 98 238 215 144 ...
##  $ Aneurisms_q3 : int  202 248 122 233 222 320 154 279 181 192 ...
##  $ Aneurisms_q4 : int  237 248 177 220 228 294 245 251 272 185 ...
```

Notice the first 3 columns have been converted to factors. These values were text in the data file so R automatically interpreted them as catagorical variables.


```r
summary(dat)
```

```
##        ID     Gender        Group    BloodPressure        Age       
##  Sub001 : 1   f:35   Control   :30   Min.   : 62.0   Min.   :12.10  
##  Sub002 : 1   F: 4   Treatment1:35   1st Qu.:107.5   1st Qu.:14.78  
##  Sub003 : 1   m:46   Treatment2:35   Median :117.5   Median :16.65  
##  Sub004 : 1   M:15                   Mean   :118.6   Mean   :16.42  
##  Sub005 : 1                          3rd Qu.:133.0   3rd Qu.:18.30  
##  Sub006 : 1                          Max.   :173.0   Max.   :20.00  
##  (Other):94                                                         
##   Aneurisms_q1    Aneurisms_q2    Aneurisms_q3    Aneurisms_q4  
##  Min.   : 65.0   Min.   : 80.0   Min.   :105.0   Min.   :116.0  
##  1st Qu.:118.0   1st Qu.:131.5   1st Qu.:182.5   1st Qu.:186.8  
##  Median :158.0   Median :162.5   Median :217.0   Median :219.0  
##  Mean   :158.8   Mean   :168.0   Mean   :219.8   Mean   :217.9  
##  3rd Qu.:188.0   3rd Qu.:196.8   3rd Qu.:248.2   3rd Qu.:244.2  
##  Max.   :260.0   Max.   :283.0   Max.   :323.0   Max.   :315.0  
## 
```

Notice the `summary()` function handles factors differently to numbers (and strings), the occurence counts for each value is often more useful information.

> ## Tip {.callout}
> 
> The `summary()` function is a great way of spotting errors in your data, look at the *dat$Gender* column. It's also a great way for spotting missing data.

> ## Challenge - Reordering factors {.challenge}
> 
> The function `table()` tabulates observations and can be used to create bar plots quickly. For instance:
>
> 
> ```r
> table(dat$Group)
> ```
> 
> ```
> ## 
> ##    Control Treatment1 Treatment2 
> ##         30         35         35
> ```
> 
> ```r
> barplot(table(dat$Group))
> ```
> 
> ![plot of chunk reordering-factors](figure/reordering-factors-1.png) 
> Use the `factor()` command to modify the column dat$Group so that the *control* group is plotted last

### Removing Levels from a Factor

Some of the Gender values in our dataset have been coded incorrectly.
Let's remove factors.


```r
barplot(table(dat$Gender))
```

![plot of chunk gender-counts](figure/gender-counts-1.png) 

Values should have been recorded as lowercase 'm' & 'f'. We should correct this.


```r
dat$Gender[dat$Gender=='M']<-'m'
```

> ## Challenge - Updating factors {.challenge}
>
> 
> ```r
> plot(x=dat$Gender,y=dat$BloodPressure)
> ```
> 
> ![plot of chunk updating-factors](figure/updating-factors-1.png) 
>
> Why does this plot show 4 levels?
>
> *Hint* how many levels does dat$Gender have?


We need to tell R that "M" is no longer a valid value for this column.
We use the `droplevels()` function to remove extra levels.


```r
dat$Gender<-droplevels(dat$Gender)
plot(x=dat$Gender,y=dat$BloodPressure)
```

![plot of chunk dropping-levels](figure/dropping-levels-1.png) 

> ## Tip {.callout}
>
> Adjusting the `levels()` of a factor provides a useful shortcut for reassigning values in this case.
>
> 
> ```r
> levels(dat$Gender)[2] <- 'f'
> plot(x = dat$Gender, y = dat$BloodPressure)
> ```
> 
> ![plot of chunk adjusting-levels](figure/adjusting-levels-1.png) 

> ## Key Points {.callout}
>
> * Factors are used to represent catagorical data
> * Factors can be *ordered* or *unordered*
> * Some R functions have special methods for handling factors

