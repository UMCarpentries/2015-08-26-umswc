---
layout: page
title: Programming with R
subtitle: Loading Data
minutes: 30
output: 
  html_document: 
    keep_md: yes
---

> ## Learning Objectives {.objectives}
> * Read tabular data from a file into a program.
> * Assign values to variables.
> * Select individual values and subsections from data.
> * Perform operations on a data frame of data.


The data sets are stored in [comma-separated values](reference.html#comma-separated-values-(csv)) (CSV) format. 
The first few rows of our first file look like this:


```
## ID,Gender,Group,BloodPressure,Age,Aneurisms_q1,Aneurisms_q2,Aneurisms_q3,Aneurisms_q4
## Sub001,m,Control,132,16,114,140,202,237
## Sub002,m,Treatment2,139,17.2,148,209,248,248
## Sub003,m,Treatment2,130,19.5,196,251,122,177
## Sub004,f,Treatment1,105,15.7,199,140,233,220
```

We want to:

* Load data into memory,
* Look at different data types and how to manipulate data
* Plot some results

To do all that, we'll have to learn a little bit about programming.

### Loading Data

Now that we have our data files, we need to start RStudio. Since we've pre-made a project, the easiest way to do this is to double click on the `SWC_R_exercise.r` file inside our project. RStudio should automatically put us into the correct directory, and show us the files available under the `Files` tab. However, we can also check in the Console:



```r
getwd()
```

```
## [1] "/Users/Amanda/2015-08-26-umswc/Lessons/r_inflam"
```

Just like in the Unix Shell, we type the command and then press `Enter` (or `return`).
getwd() shows us the working directory. If we hadn't set up a project beforehand, we could also specifically set a working directory:


```r
setwd("C:/Users/Amanda/Desktop/SWC_R_exercise")
```

But since we're already in that directory, this command has no effect. Now we can load the data into R using `read.csv`:



```r
read.csv(file = "sample.csv", header = FALSE)
```

```
##         V1     V2         V3            V4   V5           V6           V7
## 1       ID Gender      Group BloodPressure  Age Aneurisms_q1 Aneurisms_q2
## 2   Sub001      m    Control           132   16          114          140
## 3   Sub002      m Treatment2           139 17.2          148          209
## 4   Sub003      m Treatment2           130 19.5          196          251
## 5   Sub004      f Treatment1           105 15.7          199          140
## 6   Sub005      m Treatment1           125 19.9          188          120
## 7   Sub006      M Treatment2           112 14.3          260          266
## 8   Sub007      f    Control           173 17.7          135           98
## 9   Sub008      m Treatment2           108 19.8          216          238
## 10  Sub009      m Treatment2           131 19.4          117          215
## 11  Sub010      f    Control           129 18.8          188          144
## 12  Sub011      m Treatment1           126 14.8          134          155
## 13  Sub012      f Treatment2            96 15.3          152          177
## 14  Sub013      f    Control            77 16.5          112          220
## 15  Sub014      m    Control           158 12.6          109          150
## 16  Sub015      m    Control            81 14.3          146          140
## 17  Sub016      m    Control           137 15.9           97          172
## 18  Sub017      f Treatment1           147 18.4          165          157
## 19  Sub018      m Treatment2           130 18.3          158          265
## 20  Sub019      m Treatment1           105 15.4          178          109
## 21  Sub020      F Treatment1            92 14.3          107          188
## 22  Sub021      f    Control           111 12.7          174          160
## 23  Sub022      m Treatment1           122 15.4           97          110
## 24  Sub023      f Treatment2            97 17.2          187          239
## 25  Sub024      f Treatment2           118 17.3          188          191
## 26  Sub025      m Treatment1            82 16.7          114          199
## 27  Sub026      M Treatment1           123 19.6          115          160
## 28  Sub027      M Treatment2           126   15          128          249
## 29  Sub028      f Treatment1            94 16.1          112          230
## 30  Sub029      m    Control           135 17.6          136          109
## 31  Sub030      f    Control           108 18.6          103          148
## 32  Sub031      f Treatment1           133 18.3          132          151
## 33  Sub032      m Treatment1           108 16.7          118          154
## 34  Sub033      m Treatment2           122 12.5          166          176
## 35  Sub034      m Treatment1           134 14.3          152          105
## 36  Sub035      m Treatment1           145 19.7          191          148
## 37  Sub036      f    Control           133 17.6          152          178
## 38  Sub037      f Treatment2            90   17          161          270
## 39  Sub038      m Treatment2           118 12.2          239          184
## 40  Sub039      M Treatment1           113 15.1          132          137
## 41  Sub040      m Treatment2           115 17.7          168          255
## 42  Sub041      f Treatment1           142   19          140          184
## 43  Sub042      m Treatment1           114 14.7          166           85
## 44  Sub043      m    Control           139 15.2          141          160
## 45  Sub044      m Treatment1            90 15.3          161          168
## 46  Sub045      f    Control           126 12.9          103          111
## 47  Sub046      f Treatment2           109 18.4          231          240
## 48  Sub047      M    Control           125 18.1          192          141
## 49  Sub048      M    Control            99 15.6          178          180
## 50  Sub049      m    Control           122 19.5          167          123
## 51  Sub050      m Treatment1           111 13.5          135          150
## 52  Sub051      m Treatment2           109 13.5          150          166
## 53  Sub052      f Treatment1           134 13.7          192           80
## 54  Sub053      f Treatment1           113 18.7          153          153
## 55  Sub054      f Treatment2           105 12.2          205          264
## 56  Sub055      m Treatment2           125 16.9          117          194
## 57  Sub056      f Treatment2           123 19.5          199          119
## 58  Sub057      m    Control           155 12.1          182          129
## 59  Sub058      m Treatment2           117   17          180          196
## 60  Sub059      m Treatment1           116 19.2          111          111
## 61  Sub060      f    Control           133 14.7          101           98
## 62  Sub061      f    Control            94   20          166          167
## 63  Sub062      f Treatment2           106 14.1          158          171
## 64  Sub063      f Treatment1           144 14.7          189          178
## 65  Sub064      M Treatment1           149 16.6          189          101
## 66  Sub065      f Treatment2           108   15          239          189
## 67  Sub066      m Treatment1           116   15          185          224
## 68  Sub067      f Treatment2           136 13.8          224          112
## 69  Sub068      f    Control            98 14.8          104          139
## 70  Sub069      M Treatment2           148 19.1          222          199
## 71  Sub070      m    Control            74 18.9          107           98
## 72  Sub071      m Treatment2           147 17.7          153          255
## 73  Sub072      m    Control           116 17.4          118          165
## 74  Sub073      F Treatment1           133 15.5          102          184
## 75  Sub074      m    Control            97 13.1          188          125
## 76  Sub075      m Treatment2           132 12.2          180          283
## 77  Sub076      f Treatment2           153   17          178          214
## 78  Sub077      M Treatment1           151 17.7          168          184
## 79  Sub078      M Treatment1           121 19.5          118          170
## 80  Sub079      M Treatment1           116 19.5          169          114
## 81  Sub080      f    Control           104 12.8          156          138
## 82  Sub081      m Treatment2           111 17.6          232          211
## 83  Sub082      M Treatment1            62 17.7          188          108
## 84  Sub083      M Treatment2           124 14.2          169          168
## 85  Sub084      m Treatment2           124 19.2          241          233
## 86  Sub085      m Treatment2           109   16           65          207
## 87  Sub086      f    Control           117 15.2          225          185
## 88  Sub087      f    Control            90 17.6          104          116
## 89  Sub088      f Treatment1           158 17.6          179          158
## 90  Sub089      m Treatment1           113 15.1          103          140
## 91  Sub090      m    Control           150 17.8          112          130
## 92  Sub091      f Treatment2           115 16.2          226          170
## 93  Sub092      m Treatment2            83 16.6          228          221
## 94  Sub093      F    Control           116 19.1          209          142
## 95  Sub094      f Treatment1           141 17.2          153          104
## 96  Sub095      m    Control           108 13.6          111          118
## 97  Sub096      m    Control           102 14.6          148          132
## 98  Sub097      F Treatment2            90 19.6          141          196
## 99  Sub098      m Treatment1           133   17          193          112
## 100 Sub099      M Treatment2            83 16.2          130          226
## 101 Sub100      M Treatment1           122 18.4          126          157
##               V8           V9
## 1   Aneurisms_q3 Aneurisms_q4
## 2            202          237
## 3            248          248
## 4            122          177
## 5            233          220
## 6            222          228
## 7            320          294
## 8            154          245
## 9            279          251
## 10           181          272
## 11           192          185
## 12           247          223
## 13           323          245
## 14           225          195
## 15           177          189
## 16           239          223
## 17           203          207
## 18           200          193
## 19           243          187
## 20           206          182
## 21           167          218
## 22           203          183
## 23           194          133
## 24           281          214
## 25           256          265
## 26           242          195
## 27           158          228
## 28           294          315
## 29           281          126
## 30           105          155
## 31           219          228
## 32           234          162
## 33           260          160
## 34           253          233
## 35           197          299
## 36           166          185
## 37           158          170
## 38           232          284
## 39           317          269
## 40           193          206
## 41           273          274
## 42           239          202
## 43           179          196
## 44           179          239
## 45           212          181
## 46           254          126
## 47           260          310
## 48           180          225
## 49           169          183
## 50           236          224
## 51           208          279
## 52           153          204
## 53           138          222
## 54           236          216
## 55           269          207
## 56           216          211
## 57           183          251
## 58           226          218
## 59           250          294
## 60           244          201
## 61           178          116
## 62           232          241
## 63           237          212
## 64           177          238
## 65           193          172
## 66           297          300
## 67           151          182
## 68           304          288
## 69           211          204
## 70           280          196
## 71           204          138
## 72           218          234
## 73           220          227
## 74           246          222
## 75           191          157
## 76           204          298
## 77           291          240
## 78           184          229
## 79           249          249
## 80           248          233
## 81           218          258
## 82           219          246
## 83           180          136
## 84           180          211
## 85           292          182
## 86           234          235
## 87           195          235
## 88           173          221
## 89           216          244
## 90           209          186
## 91           175          191
## 92           307          244
## 93           316          259
## 94           199          184
## 95           194          214
## 96           173          191
## 97           200          194
## 98           322          273
## 99           123          181
## 100          286          281
## 101          129          160
```

The expression `read.csv(...)` is a [function call](reference.html#function-call) that asks R to run the function `read.csv`.

`read.csv` has two [arguments](reference.html#argument): the name of the file we want to read, and whether the first line of the file contains names for the columns of data.
The filename needs to be a character string (or [string](reference.html#string) for short), so we put it in quotes. Assigning the second argument, `header`, to be `FALSE` indicates that the data file does not have column headers. We'll talk more about the value `FALSE`, and its converse `TRUE`, in lesson 04.

> ## Tip {.callout}
>
> `read.csv` actually has many more arguments that you may find useful when
> importing your own data in the future. You can learn more about these
> options in this supplementary [lesson](01-supp-read-write-csv.html).

The utility of a function is that it will perform its given action on whatever value is passed to the named argument(s).
For example, in this case if we provided the name of a different file to the argument `file`, `read.csv` would read it instead.
We'll learn more of the details about functions and their arguments in the next lesson.

Since we didn't tell it to do anything else with the function's output, the console will display the full contents of the file `sample.csv`.
Try it out.

`read.csv` read the file, but we can't use data unless we assign it to a variable.
A variable is just a name for a value, such as `x`, `current_temperature`, or `subject_id`.
We can create a new variable simply by assigning a value to it using `<-`



```r
weight_kg <- 55
```

Once a variable has a value, we can print it by typing the name of the variable and hitting `Enter` (or `return`).
In general, R will print to the console any object returned by a function or operation *unless* we assign it to a variable.


```r
weight_kg
```

```
## [1] 55
```

We can do arithmetic with the variable:


```r
# weight in pounds:
2.2 * weight_kg
```

```
## [1] 121
```

> ## Tip {.callout}
>
> We can add comments to our code using the `#` character. It is useful to
> document our code in this way so that others (and us the next time we
> read it) have an easier time following what the code is doing.

We can also change an object's value by assigning it a new value:


```r
weight_kg <- 57.5
# weight in kilograms is now
weight_kg
```

```
## [1] 57.5
```

If we imagine the variable as a sticky note with a name written on it,
assignment is like putting the sticky note on a particular value:

<img src="fig/python-sticky-note-variables-01.svg" alt="Variables as Sticky Notes" />

This means that assigning a value to one object does not change the values of other variables.
For example, let's store the subject's weight in pounds in a variable:


```r
weight_lb <- 2.2 * weight_kg
# weight in kg...
weight_kg
```

```
## [1] 57.5
```

```r
# ...and in pounds
weight_lb
```

```
## [1] 126.5
```

<img src="fig/python-sticky-note-variables-02.svg" alt="Creating Another Variable" />

and then change `weight_kg`:


```r
weight_kg <- 100.0
# weight in kg now...
weight_kg
```

```
## [1] 100
```

```r
# ...and weight in pounds still
weight_lb
```

```
## [1] 126.5
```

<img src="fig/python-sticky-note-variables-03.svg" alt="Updating a Variable" />

Since `weight_lb` doesn't "remember" where its value came from, it isn't automatically updated when `weight_kg` changes.
This is different from the way spreadsheets work.

> ## Tip {.callout} 
>An alternative way to print the value of a variable is to use () around the assignment statement. As an example: `(total_weight <- weight_kg + weight_lb)`, adds the values of `weight_kg` and `weight_lb`, assigns the result to the `total_weight`, and finally prints the assigned value of the variable `total_weight`.


Now that we know how to assign things to variables, let's re-run `read.csv` and save its result:


```r
aneurism <- read.csv(file = "sample.csv")
```

This statement doesn't produce any output because assignment doesn't display anything.
If we want to check that our data has been loaded, we can print the variable's value.
However, for large data sets it is convenient to use the function `head` to display only the first few rows of data.


```r
head(aneurism)
```

```
##       ID Gender      Group BloodPressure  Age Aneurisms_q1 Aneurisms_q2
## 1 Sub001      m    Control           132 16.0          114          140
## 2 Sub002      m Treatment2           139 17.2          148          209
## 3 Sub003      m Treatment2           130 19.5          196          251
## 4 Sub004      f Treatment1           105 15.7          199          140
## 5 Sub005      m Treatment1           125 19.9          188          120
## 6 Sub006      M Treatment2           112 14.3          260          266
##   Aneurisms_q3 Aneurisms_q4
## 1          202          237
## 2          248          248
## 3          122          177
## 4          233          220
## 5          222          228
## 6          320          294
```

> ## Challenge - Assigning values to variables {.challenge}
>
> Draw diagrams showing what variables refer to what values after each statement in the following program:
>

```r
mass <- 47.5
age <- 122
mass <- mass * 2.0
age <- age - 20
```

### Manipulating Data

Now that our data is loaded in memory, we can start doing things with it.
First, let's ask what type of thing `aneurism` is:


```r
class(aneurism)
```

```
## [1] "data.frame"
```

The output tells us that is a data frame. Think of this structure as a spreadsheet in MS Excel that many of us are familiar with.
Data frames are very useful for storing data and you will find them elsewhere when programming in R. A typical data frame of experimental data contains individual observations in rows and variables in columns.

We can see the dimensions, or [shape](reference.html#shape-(of-an-array)), of the data frame with the function `dim`:


```r
dim(aneurism)
```

```
## [1] 100   9
```

This tells us that our data frame, `aneurism`, has 100 rows and 9 columns.

If we want to get a single value from the data frame, we can provide an [index](reference.html#index) in square brackets, just as we do in math:


```r
# first value in aneurism
aneurism[1, 1]
```

```
## [1] Sub001
## 100 Levels: Sub001 Sub002 Sub003 Sub004 Sub005 Sub006 Sub007 ... Sub100
```

```r
# middle value in aneurism
aneurism[30, 20]
```

```
## NULL
```

An index like `[30, 20]` selects a single element of a data frame, but we can select whole sections as well.
For example, we can select the first ten days (columns) of values for the first four patients (rows) like this:


```r
aneurism[30:40, 1:3]
```

```
##        ID Gender      Group
## 30 Sub030      f    Control
## 31 Sub031      f Treatment1
## 32 Sub032      m Treatment1
## 33 Sub033      m Treatment2
## 34 Sub034      m Treatment1
## 35 Sub035      m Treatment1
## 36 Sub036      f    Control
## 37 Sub037      f Treatment2
## 38 Sub038      m Treatment2
## 39 Sub039      M Treatment1
## 40 Sub040      m Treatment2
```

The [slice](reference.html#slice) `1:4` means, "Start at index 1 and go to index 4."

The slice does not need to start at 1, e.g. the line below selects rows 5 through 10:


```r
aneurism[1:5, 6:9]
```

```
##   Aneurisms_q1 Aneurisms_q2 Aneurisms_q3 Aneurisms_q4
## 1          114          140          202          237
## 2          148          209          248          248
## 3          196          251          122          177
## 4          199          140          233          220
## 5          188          120          222          228
```
We can use the function `c`, which stands for **c**ombine, to select non-contiguous values:


```r
aneurism[c(1, 30, 54, 72), c(2, 4, 5)]
```

```
##    Gender BloodPressure  Age
## 1       m           132 16.0
## 30      f           108 18.6
## 54      f           105 12.2
## 72      m           116 17.4
```

We also don't have to provide a slice for either the rows or the columns.
If we don't include a slice for the rows, R returns all the rows; if we don't include a slice for the columns, R returns all the columns.
If we don't provide a slice for either rows or columns, e.g. `aneurism[, ]`, R returns the full data frame.


```r
# All columns from row 5
aneurism[5, ]
```

```
##       ID Gender      Group BloodPressure  Age Aneurisms_q1 Aneurisms_q2
## 5 Sub005      m Treatment1           125 19.9          188          120
##   Aneurisms_q3 Aneurisms_q4
## 5          222          228
```

```r
# All rows from column 16
aneurism[, 6]
```

```
##   [1] 114 148 196 199 188 260 135 216 117 188 134 152 112 109 146  97 165
##  [18] 158 178 107 174  97 187 188 114 115 128 112 136 103 132 118 166 152
##  [35] 191 152 161 239 132 168 140 166 141 161 103 231 192 178 167 135 150
##  [52] 192 153 205 117 199 182 180 111 101 166 158 189 189 239 185 224 104
##  [69] 222 107 153 118 102 188 180 178 168 118 169 156 232 188 169 241  65
##  [86] 225 104 179 103 112 226 228 209 153 111 148 141 193 130 126
```

### Adding Elements

The function `c()` (for combine) can also be used to add elements to a vector.


```r
z <- 1:10
z <- c(z, 11)
z
```

```
##  [1]  1  2  3  4  5  6  7  8  9 10 11
```

```r
z <- c(0, z)
z
```

```
##  [1]  0  1  2  3  4  5  6  7  8  9 10 11
```

> ## Tip {.callout} 
>An alternative way to get numbers in a sequence is to use `seq()`. Try the expression `seq(from = 1, to = 10, by = 0.1)` 


### Addressing by Name

Columns in an R data frame are named.


```r
colnames(aneurism)
```

```
## [1] "ID"            "Gender"        "Group"         "BloodPressure"
## [5] "Age"           "Aneurisms_q1"  "Aneurisms_q2"  "Aneurisms_q3" 
## [9] "Aneurisms_q4"
```

> ## Tip {.callout} 
>
> If names are not specified e.g. using `headers=FALSE` in a `read.csv()` function, R assigns default names `V1,V2,...,Vn`

We usually use the `$` operator to address a column by name


```r
aneurism$Gender
```

```
##   [1] m m m f m M f m m f m f f m m m f m m F f m f f m M M f m f f m m m m
##  [36] f f m M m f m m m f f M M m m m f f f m f m m m f f f f M f m f f M m
##  [71] m m F m m f M M M f m M M m m f f f m m f m F f m m F m M M
## Levels: f F m M
```

Named addressing can also be used in square brackets.

```r
head(aneurism[ , c('Age','Gender')])
```

```
##    Age Gender
## 1 16.0      m
## 2 17.2      m
## 3 19.5      m
## 4 15.7      f
## 5 19.9      m
## 6 14.3      M
```

> ## Best Practice {.callout} 
>
> Best practice is to address columns by name, often you will create or delete columns and the column position will change.


We can use logical vectors to select data from a data frame.


```r
index <- aneurism$Group == 'Control'
aneurism[index,]$BloodPressure
```

```
##  [1] 132 173 129  77 158  81 137 111 135 108 133 139 126 125  99 122 155
## [18] 133  94  98  74 116  97 104 117  90 150 116 108 102
```

Often this operation is written as one line of code:


```r
aneurism[aneurism$Group=='Control',]$BloodPressure
```

```
##  [1] 132 173 129  77 158  81 137 111 135 108 133 139 126 125  99 122 155
## [18] 133  94  98  74 116  97 104 117  90 150 116 108 102
```

> ## Challenge - Using logical indexes {.challenge}
> 1. Create a scatterplot showing BloodPressure for subjects not in the control group.
> 2. How many ways are there to index this set of subjects?


We are studying aneurism patients. Each row holds the observations for just one patient.

Now let's perform some common mathematical operations to learn about our data.
When analyzing data we often want to look at partial statistics, such as the maximum value per patient or the average value per day.
One way to do this is to select the data we want to create a new temporary data frame, and then perform the calculation on this subset:


```r
# first row, all of the columns
BloodP <- aneurism$BloodPressure
# max inflammation for patient 1
max(BloodP)
```

```
## [1] 173
```

We don't actually need to store the row in a variable of its own.
Instead, we can combine the selection and the function call:


```r
# max inflammation for patient 2
max(aneurism$BloodPressure)
```

```
## [1] 173
```

R also has functions for other common calculations, e.g. finding the minimum, mean, median, and standard deviation of the data:


```r
# minimum patient age
min(aneurism$Age)
```

```
## [1] 12.1
```

```r
# mean patient age
mean(aneurism$Age)
```

```
## [1] 16.42
```

```r
# median patient age
median(aneurism$Age)
```

```
## [1] 16.65
```

```r
# standard deviation of patient age
sd(aneurism$Ag)
```

```
## [1] 2.209529
```
