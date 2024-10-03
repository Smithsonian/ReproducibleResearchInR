---
title: 'Module 4:  Filtering and Subsetting Data'
author: "Brian P Steves"
date: "2024-10-03"
output:
  html_document:
    keep_md: yes
---


We briefly discussed selecting data within an object in Module 2.  Here we will discuss more advanced methods to subsetting data. Because most of the data we will be using in R will be in the form of data frames we will concentrate on data frame methods for filtering and subsetting.


##  Determining the structure of an object

In order to understand how to select portions of a data object, you will need to know details about the structure of that object first.  The str() function accomplishes that.


```r
# Create a series of equally sized vectors
sites<-c("Site A", "Site B")
dates<-as.Date(c("12Mar2013","04Apr2013"),"%d%b%Y")
lat=c(45, 47)
lon=c(-124, -125)
treatment=c(T,F)

# Combine the vectors into a data frame
dat<-data.frame(sites, dates, lat, lon, treatment)

# Use str() on some of the vectors and the data frame
str(sites)
```

```
##  chr [1:2] "Site A" "Site B"
```

```r
str(lat)
```

```
##  num [1:2] 45 47
```

```r
str(dat)
```

```
## 'data.frame':	2 obs. of  5 variables:
##  $ sites    : chr  "Site A" "Site B"
##  $ dates    : Date, format: "2013-03-12" "2013-04-04"
##  $ lat      : num  45 47
##  $ lon      : num  -124 -125
##  $ treatment: logi  TRUE FALSE
```

```r
# The name() function is similar but only provides the names of the various data frame columns
names(dat)
```

```
## [1] "sites"     "dates"     "lat"       "lon"       "treatment"
```

```r
# You can also use name() to reassign the names of the data frame columns

names(dat)<-c("SiteName", "VisitDate", "Latitude", "Longitude", "TreatmentApplied")

str(dat)
```

```
## 'data.frame':	2 obs. of  5 variables:
##  $ SiteName        : chr  "Site A" "Site B"
##  $ VisitDate       : Date, format: "2013-03-12" "2013-04-04"
##  $ Latitude        : num  45 47
##  $ Longitude       : num  -124 -125
##  $ TreatmentApplied: logi  TRUE FALSE
```


## Head and Tail

Large data frames take a long time to print out to the screen.  Because of this, sometimes you just want to view the first portion (the head) or the last portion (the tail) of a data frame.  To get a sense of what the data looks like.   


```r
data(iris)

# How many rows of data using nrow()
nrow(iris)
```

```
## [1] 150
```

```r
# too much to show on screen


# The head (beginning) of the data
head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

```r
# The tail (end) of the data
tail(iris)
```

```
##     Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
## 145          6.7         3.3          5.7         2.5 virginica
## 146          6.7         3.0          5.2         2.3 virginica
## 147          6.3         2.5          5.0         1.9 virginica
## 148          6.5         3.0          5.2         2.0 virginica
## 149          6.2         3.4          5.4         2.3 virginica
## 150          5.9         3.0          5.1         1.8 virginica
```

```r
# the defualt is 6 rows of data, but you can change this by specifing an n value

head(iris, n=20)
```

```
##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1           5.1         3.5          1.4         0.2  setosa
## 2           4.9         3.0          1.4         0.2  setosa
## 3           4.7         3.2          1.3         0.2  setosa
## 4           4.6         3.1          1.5         0.2  setosa
## 5           5.0         3.6          1.4         0.2  setosa
## 6           5.4         3.9          1.7         0.4  setosa
## 7           4.6         3.4          1.4         0.3  setosa
## 8           5.0         3.4          1.5         0.2  setosa
## 9           4.4         2.9          1.4         0.2  setosa
## 10          4.9         3.1          1.5         0.1  setosa
## 11          5.4         3.7          1.5         0.2  setosa
## 12          4.8         3.4          1.6         0.2  setosa
## 13          4.8         3.0          1.4         0.1  setosa
## 14          4.3         3.0          1.1         0.1  setosa
## 15          5.8         4.0          1.2         0.2  setosa
## 16          5.7         4.4          1.5         0.4  setosa
## 17          5.4         3.9          1.3         0.4  setosa
## 18          5.1         3.5          1.4         0.3  setosa
## 19          5.7         3.8          1.7         0.3  setosa
## 20          5.1         3.8          1.5         0.3  setosa
```

##  Selecting Variables (data frame columns)

### Selecting Single columns using Base R


```r
# By index
dat[1]
```

```
##   SiteName
## 1   Site A
## 2   Site B
```

```r
# By Name
dat["SiteName"]
```

```
##   SiteName
## 1   Site A
## 2   Site B
```

```r
# Using the $ operator

dat$SiteName
```

```
## [1] "Site A" "Site B"
```

### By Name


```r
dat[c("SiteName","TreatmentApplied")]
```

```
##   SiteName TreatmentApplied
## 1   Site A             TRUE
## 2   Site B            FALSE
```

```r
# Alternatively you can use matrix R,C notation

dat[,c("SiteName","TreatmentApplied")]
```

```
##   SiteName TreatmentApplied
## 1   Site A             TRUE
## 2   Site B            FALSE
```

### By column number like a matrix


```r
dat[,c(1,5)]
```

```
##   SiteName TreatmentApplied
## 1   Site A             TRUE
## 2   Site B            FALSE
```

### By Logical Assignment


```r
dat[c(T,F,F,F,T)]
```

```
##   SiteName TreatmentApplied
## 1   Site A             TRUE
## 2   Site B            FALSE
```

##  Droping Variables

### Excluding Variables


```r
# we can use negative indexes

dat[c(-1,-4)]
```

```
##    VisitDate Latitude TreatmentApplied
## 1 2013-03-12       45             TRUE
## 2 2013-04-04       47            FALSE
```

```r
# or we can use logical assignment

dropcols<-names(dat) %in% c("Latitude","Longitude")
dropcols
```

```
## [1] FALSE FALSE  TRUE  TRUE FALSE
```

```r
dropcols2<-c("Latitude","Longitude")

# this is the similar to a logical assignment for selecting columns but instead a "True" is a column we want to drop 
dat[c(F,F,T,T,F)]
```

```
##   Latitude Longitude
## 1       45      -124
## 2       47      -125
```

```r
# We use the ! to denote a logical negation or "not"
# Here we specify that we want to select "not the dropcols"
dat[!dropcols]
```

```
##   SiteName  VisitDate TreatmentApplied
## 1   Site A 2013-03-12             TRUE
## 2   Site B 2013-04-04            FALSE
```


### Dropping Variables permentantly


```r
# One option is reassignment

dat<-dat[!dropcols]

# rebuild the data frame
dat<-data.frame(sites, dates, lat, lon, treatment)
names(dat)<-c("SiteName", "VisitDate", "Latitude", "Longitude", "TreatmentApplied")

# the other option is to set some columns to null

dat$TreatmentApplied <-NULL
dat
```

```
##   SiteName  VisitDate Latitude Longitude
## 1   Site A 2013-03-12       45      -124
## 2   Site B 2013-04-04       47      -125
```

```r
# But you can't do this with more than one column at a time

dat[c("Latitude","Longitude")]<-NULL

# However you can chain these

dat$Latitude<-dat$Longitude<-NULL
dat
```

```
##   SiteName  VisitDate
## 1   Site A 2013-03-12
## 2   Site B 2013-04-04
```

## selecting columns using Tidyverse's 'dplyr' package.  


```r
library(dplyr)
```

```
## 
## Attaching package: 'dplyr'
```

```
## The following objects are masked from 'package:stats':
## 
##     filter, lag
```

```
## The following objects are masked from 'package:base':
## 
##     intersect, setdiff, setequal, union
```

```r
dat<-data.frame(sites, dates, lat, lon, treatment)
names(dat)<-c("SiteName", "VisitDate", "Latitude", "Longitude", "TreatmentApplied")

select(dat, SiteName, Latitude)
```

```
##   SiteName Latitude
## 1   Site A       45
## 2   Site B       47
```

Note that the first input to the select function is the name of the data frame.

The dplyr package uses a new type of notation called piping using "%>%" between expressions. This eliminates the need to nest functions within each other and streamlines a lot of coding.


```r
dat %>% select(Latitude, Longitude)
```

```
##   Latitude Longitude
## 1       45      -124
## 2       47      -125
```
Note that we start with the data frame and then pipe in the 'select' function. In doing so we don't need to include the data frame name as the first input of the the select function. The result of this bit of code can then be piped into more dplyr expressions (more on that later)


The dplyr select() function will accept a wide range of helper functions that help select columns based on criteria.


```r
head(iris)
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

```r
iris %>% select(contains("Sepal")) %>% head()
```

```
##   Sepal.Length Sepal.Width
## 1          5.1         3.5
## 2          4.9         3.0
## 3          4.7         3.2
## 4          4.6         3.1
## 5          5.0         3.6
## 6          5.4         3.9
```

```r
iris %>% select(contains("Width")) %>% head()
```

```
##   Sepal.Width Petal.Width
## 1         3.5         0.2
## 2         3.0         0.2
## 3         3.2         0.2
## 4         3.1         0.2
## 5         3.6         0.2
## 6         3.9         0.4
```

```r
# all columns except "Species"
iris %>% select(-Species) %>% head()
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width
## 1          5.1         3.5          1.4         0.2
## 2          4.9         3.0          1.4         0.2
## 3          4.7         3.2          1.3         0.2
## 4          4.6         3.1          1.5         0.2
## 5          5.0         3.6          1.4         0.2
## 6          5.4         3.9          1.7         0.4
```

```r
# select Species and then the two middle measurement columns
iris %>% select(Species, Sepal.Width:Petal.Length) %>% head()
```

```
##   Species Sepal.Width Petal.Length
## 1  setosa         3.5          1.4
## 2  setosa         3.0          1.4
## 3  setosa         3.2          1.3
## 4  setosa         3.1          1.5
## 5  setosa         3.6          1.4
## 6  setosa         3.9          1.7
```



##  Selecting Observations (data frame rows) firs using Base R


```r
# loading some real data with lots of records
library(readr)
mtcars <- read_csv(readr_example("mtcars.csv"))
```

```
## Rows: 32 Columns: 11
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (11): mpg, cyl, disp, hp, drat, wt, qsec, vs, am, gear, carb
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
str(mtcars)
```

```
## spec_tbl_df [32 × 11] (S3: spec_tbl_df/tbl_df/tbl/data.frame)
##  $ mpg : num [1:32] 21 21 22.8 21.4 18.7 18.1 14.3 24.4 22.8 19.2 ...
##  $ cyl : num [1:32] 6 6 4 6 8 6 8 4 4 6 ...
##  $ disp: num [1:32] 160 160 108 258 360 ...
##  $ hp  : num [1:32] 110 110 93 110 175 105 245 62 95 123 ...
##  $ drat: num [1:32] 3.9 3.9 3.85 3.08 3.15 2.76 3.21 3.69 3.92 3.92 ...
##  $ wt  : num [1:32] 2.62 2.88 2.32 3.21 3.44 ...
##  $ qsec: num [1:32] 16.5 17 18.6 19.4 17 ...
##  $ vs  : num [1:32] 0 0 1 1 0 1 0 1 1 1 ...
##  $ am  : num [1:32] 1 1 1 0 0 0 0 0 0 0 ...
##  $ gear: num [1:32] 4 4 4 3 3 3 3 4 4 4 ...
##  $ carb: num [1:32] 4 4 1 1 2 1 4 2 2 4 ...
##  - attr(*, "spec")=
##   .. cols(
##   ..   mpg = col_double(),
##   ..   cyl = col_double(),
##   ..   disp = col_double(),
##   ..   hp = col_double(),
##   ..   drat = col_double(),
##   ..   wt = col_double(),
##   ..   qsec = col_double(),
##   ..   vs = col_double(),
##   ..   am = col_double(),
##   ..   gear = col_double(),
##   ..   carb = col_double()
##   .. )
##  - attr(*, "problems")=<externalptr>
```

### By index


```r
# select first two records
mtcars[1:2,]
```

```
## # A tibble: 2 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1    21     6   160   110   3.9  2.62  16.5     0     1     4     4
## 2    21     6   160   110   3.9  2.88  17.0     0     1     4     4
```

```r
# selecting second and fourth records
mtcars[c(2,4),]
```

```
## # A tibble: 2 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  21       6   160   110  3.9   2.88  17.0     0     1     4     4
## 2  21.4     6   258   110  3.08  3.22  19.4     1     0     3     1
```

```r
# selecting not the third and fifth record
mtcars[c(-3,-5),]
```

```
## # A tibble: 30 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
##  3  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
##  4  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
##  5  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  6  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
##  7  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
##  8  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
##  9  17.8     6  168.   123  3.92  3.44  18.9     1     0     4     4
## 10  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
## # … with 20 more rows
```

### By value


```r
# Selecting cars with 4 cylinders
mtcars[mtcars$cyl == 4,]
```

```
## # A tibble: 11 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  22.8     4 108      93  3.85  2.32  18.6     1     1     4     1
##  2  24.4     4 147.     62  3.69  3.19  20       1     0     4     2
##  3  22.8     4 141.     95  3.92  3.15  22.9     1     0     4     2
##  4  32.4     4  78.7    66  4.08  2.2   19.5     1     1     4     1
##  5  30.4     4  75.7    52  4.93  1.62  18.5     1     1     4     2
##  6  33.9     4  71.1    65  4.22  1.84  19.9     1     1     4     1
##  7  21.5     4 120.     97  3.7   2.46  20.0     1     0     3     1
##  8  27.3     4  79      66  4.08  1.94  18.9     1     1     4     1
##  9  26       4 120.     91  4.43  2.14  16.7     0     1     5     2
## 10  30.4     4  95.1   113  3.77  1.51  16.9     1     1     5     2
## 11  21.4     4 121     109  4.11  2.78  18.6     1     1     4     2
```

```r
# Using & to combine conditions
mtcars[mtcars$cyl == 4 & mtcars$mpg > 30,]
```

```
## # A tibble: 4 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  32.4     4  78.7    66  4.08  2.2   19.5     1     1     4     1
## 2  30.4     4  75.7    52  4.93  1.62  18.5     1     1     4     2
## 3  33.9     4  71.1    65  4.22  1.84  19.9     1     1     4     1
## 4  30.4     4  95.1   113  3.77  1.51  16.9     1     1     5     2
```

##  Selecting Observations and Variables


```r
# mpg and hp for 4 cylinder cars 

mtcars[mtcars$cyl == 4,c("mpg","hp")]
```

```
## # A tibble: 11 × 2
##      mpg    hp
##    <dbl> <dbl>
##  1  22.8    93
##  2  24.4    62
##  3  22.8    95
##  4  32.4    66
##  5  30.4    52
##  6  33.9    65
##  7  21.5    97
##  8  27.3    66
##  9  26      91
## 10  30.4   113
## 11  21.4   109
```

```r
# Number of gears for 4 cylinder cars
mtcars[mtcars$cyl == 4,]$gear
```

```
##  [1] 4 4 4 4 4 4 3 4 5 5 4
```

##  Subset Function

The subset() function is a shortcut to selecting observations and variables


```r
# this isn't any shorter than the previous method of finding the cars based on cyl, hp, mpg.

subset(mtcars, cyl == 4, select=c(mpg, hp))
```

```
## # A tibble: 11 × 2
##      mpg    hp
##    <dbl> <dbl>
##  1  22.8    93
##  2  24.4    62
##  3  22.8    95
##  4  32.4    66
##  5  30.4    52
##  6  33.9    65
##  7  21.5    97
##  8  27.3    66
##  9  26      91
## 10  30.4   113
## 11  21.4   109
```

```r
# we can also drop columns using the select option

subset(mtcars, cyl==4, select=c(-mpg, -hp))
```

```
## # A tibble: 11 × 9
##      cyl  disp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1     4 108    3.85  2.32  18.6     1     1     4     1
##  2     4 147.   3.69  3.19  20       1     0     4     2
##  3     4 141.   3.92  3.15  22.9     1     0     4     2
##  4     4  78.7  4.08  2.2   19.5     1     1     4     1
##  5     4  75.7  4.93  1.62  18.5     1     1     4     2
##  6     4  71.1  4.22  1.84  19.9     1     1     4     1
##  7     4 120.   3.7   2.46  20.0     1     0     3     1
##  8     4  79    4.08  1.94  18.9     1     1     4     1
##  9     4 120.   4.43  2.14  16.7     0     1     5     2
## 10     4  95.1  3.77  1.51  16.9     1     1     5     2
## 11     4 121    4.11  2.78  18.6     1     1     4     2
```

```r
# Subset makes it easier to combine multiple conditions

subset(mtcars, cyl==4 & mpg > 30 & hp > 100)
```

```
## # A tibble: 1 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  30.4     4  95.1   113  3.77  1.51  16.9     1     1     5     2
```

```r
# You can even do "OR" conditions using the "|" operator
# here we are selecting where cyl  = 4 or mpg < 15

subset(mtcars, cyl ==4 | mpg < 15)
```

```
## # A tibble: 16 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  22.8     4 108      93  3.85  2.32  18.6     1     1     4     1
##  2  14.3     8 360     245  3.21  3.57  15.8     0     0     3     4
##  3  24.4     4 147.     62  3.69  3.19  20       1     0     4     2
##  4  22.8     4 141.     95  3.92  3.15  22.9     1     0     4     2
##  5  10.4     8 472     205  2.93  5.25  18.0     0     0     3     4
##  6  10.4     8 460     215  3     5.42  17.8     0     0     3     4
##  7  14.7     8 440     230  3.23  5.34  17.4     0     0     3     4
##  8  32.4     4  78.7    66  4.08  2.2   19.5     1     1     4     1
##  9  30.4     4  75.7    52  4.93  1.62  18.5     1     1     4     2
## 10  33.9     4  71.1    65  4.22  1.84  19.9     1     1     4     1
## 11  21.5     4 120.     97  3.7   2.46  20.0     1     0     3     1
## 12  13.3     8 350     245  3.73  3.84  15.4     0     0     3     4
## 13  27.3     4  79      66  4.08  1.94  18.9     1     1     4     1
## 14  26       4 120.     91  4.43  2.14  16.7     0     1     5     2
## 15  30.4     4  95.1   113  3.77  1.51  16.9     1     1     5     2
## 16  21.4     4 121     109  4.11  2.78  18.6     1     1     4     2
```
 Remember you can combine a series of logical operators ( "|" and "&")
 it helps if you know some logic to help simply your expressions
 for example...
 
 !(a & b) is the same as !a | !b
 !(a | b) is the same as !a & !b 


```r
 subset(mtcars, !(cyl  == 4 & gear == 4))
```

```
## # A tibble: 24 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
##  3  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
##  4  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
##  5  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
##  6  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  7  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
##  8  17.8     6  168.   123  3.92  3.44  18.9     1     0     4     4
##  9  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
## 10  17.3     8  276.   180  3.07  3.73  17.6     0     0     3     3
## # … with 14 more rows
```

```r
 # is the same as 

 subset(mtcars, !cyl == 4 | !gear == 4 )
```

```
## # A tibble: 24 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
##  3  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
##  4  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
##  5  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
##  6  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  7  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
##  8  17.8     6  168.   123  3.92  3.44  18.9     1     0     4     4
##  9  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
## 10  17.3     8  276.   180  3.07  3.73  17.6     0     0     3     3
## # … with 14 more rows
```

```r
 # and likewise

 subset(mtcars, !(cyl == 4 | gear == 4))
```

```
## # A tibble: 17 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
##  2  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
##  3  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
##  4  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  5  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
##  6  17.3     8  276.   180  3.07  3.73  17.6     0     0     3     3
##  7  15.2     8  276.   180  3.07  3.78  18       0     0     3     3
##  8  10.4     8  472    205  2.93  5.25  18.0     0     0     3     4
##  9  10.4     8  460    215  3     5.42  17.8     0     0     3     4
## 10  14.7     8  440    230  3.23  5.34  17.4     0     0     3     4
## 11  15.5     8  318    150  2.76  3.52  16.9     0     0     3     2
## 12  15.2     8  304    150  3.15  3.44  17.3     0     0     3     2
## 13  13.3     8  350    245  3.73  3.84  15.4     0     0     3     4
## 14  19.2     8  400    175  3.08  3.84  17.0     0     0     3     2
## 15  15.8     8  351    264  4.22  3.17  14.5     0     1     5     4
## 16  19.7     6  145    175  3.62  2.77  15.5     0     1     5     6
## 17  15       8  301    335  3.54  3.57  14.6     0     1     5     8
```

```r
 # is the same as 

 subset(mtcars, !cyl == 4 & !gear == 4)
```

```
## # A tibble: 17 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
##  2  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
##  3  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
##  4  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  5  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
##  6  17.3     8  276.   180  3.07  3.73  17.6     0     0     3     3
##  7  15.2     8  276.   180  3.07  3.78  18       0     0     3     3
##  8  10.4     8  472    205  2.93  5.25  18.0     0     0     3     4
##  9  10.4     8  460    215  3     5.42  17.8     0     0     3     4
## 10  14.7     8  440    230  3.23  5.34  17.4     0     0     3     4
## 11  15.5     8  318    150  2.76  3.52  16.9     0     0     3     2
## 12  15.2     8  304    150  3.15  3.44  17.3     0     0     3     2
## 13  13.3     8  350    245  3.73  3.84  15.4     0     0     3     4
## 14  19.2     8  400    175  3.08  3.84  17.0     0     0     3     2
## 15  15.8     8  351    264  4.22  3.17  14.5     0     1     5     4
## 16  19.7     6  145    175  3.62  2.77  15.5     0     1     5     6
## 17  15       8  301    335  3.54  3.57  14.6     0     1     5     8
```

You can also use the %in% operator to match multiple values at once.


```r
hp_of_interest<-c(110, 180, 245)
subset(mtcars, hp %in% hp_of_interest)
```

```
## # A tibble: 8 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
## 2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
## 3  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
## 4  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
## 5  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
## 6  17.3     8  276.   180  3.07  3.73  17.6     0     0     3     3
## 7  15.2     8  276.   180  3.07  3.78  18       0     0     3     3
## 8  13.3     8  350    245  3.73  3.84  15.4     0     0     3     4
```

```r
# is the same as 
subset(mtcars, hp == 110 | hp == 180 | hp == 245)
```

```
## # A tibble: 8 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
## 2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
## 3  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
## 4  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
## 5  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
## 6  17.3     8  276.   180  3.07  3.73  17.6     0     0     3     3
## 7  15.2     8  276.   180  3.07  3.78  18       0     0     3     3
## 8  13.3     8  350    245  3.73  3.84  15.4     0     0     3     4
```

## subsetting data using tidyverse's dplyr

Use commas to separate "and" statements.
Use | to separate "or" statements.


```r
mtcars %>% filter(hp == 110)
```

```
## # A tibble: 3 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  21       6   160   110  3.9   2.62  16.5     0     1     4     4
## 2  21       6   160   110  3.9   2.88  17.0     0     1     4     4
## 3  21.4     6   258   110  3.08  3.22  19.4     1     0     3     1
```

```r
mtcars %>% filter(hp < 110,cyl == 4, wt>3)
```

```
## # A tibble: 2 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
## 2  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
```

```r
mtcars %>% filter(hp > 100 | cyl == 4)
```

```
## # A tibble: 32 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
##  2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
##  3  22.8     4  108     93  3.85  2.32  18.6     1     1     4     1
##  4  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
##  5  18.7     8  360    175  3.15  3.44  17.0     0     0     3     2
##  6  18.1     6  225    105  2.76  3.46  20.2     1     0     3     1
##  7  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  8  24.4     4  147.    62  3.69  3.19  20       1     0     4     2
##  9  22.8     4  141.    95  3.92  3.15  22.9     1     0     4     2
## 10  19.2     6  168.   123  3.92  3.44  18.3     1     0     4     4
## # … with 22 more rows
```

```r
mtcars %>% filter(hp %in% hp_of_interest)
```

```
## # A tibble: 8 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  21       6  160    110  3.9   2.62  16.5     0     1     4     4
## 2  21       6  160    110  3.9   2.88  17.0     0     1     4     4
## 3  21.4     6  258    110  3.08  3.22  19.4     1     0     3     1
## 4  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
## 5  16.4     8  276.   180  3.07  4.07  17.4     0     0     3     3
## 6  17.3     8  276.   180  3.07  3.73  17.6     0     0     3     3
## 7  15.2     8  276.   180  3.07  3.78  18       0     0     3     3
## 8  13.3     8  350    245  3.73  3.84  15.4     0     0     3     4
```

## combining dplyr filter and select


```r
mtcars %>% filter(cyl == 4) %>% select(cyl, mpg, hp)
```

```
## # A tibble: 11 × 3
##      cyl   mpg    hp
##    <dbl> <dbl> <dbl>
##  1     4  22.8    93
##  2     4  24.4    62
##  3     4  22.8    95
##  4     4  32.4    66
##  5     4  30.4    52
##  6     4  33.9    65
##  7     4  21.5    97
##  8     4  27.3    66
##  9     4  26      91
## 10     4  30.4   113
## 11     4  21.4   109
```




##  Random samples in Base R
Sometimes you will want a random subset of your data.  To do this, use the sample() function without replacement.


```r
# first determine how many rows of data you have
rowcount<-nrow(mtcars)

# select two random rows
randomrows<-sample(rowcount, 2)

# use the "randomrows" to select those rows from the data frame
mtcars[randomrows,]
```

```
## # A tibble: 2 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  18.1     6   225   105  2.76  3.46  20.2     1     0     3     1
## 2  13.3     8   350   245  3.73  3.84  15.4     0     0     3     4
```

## Select random rows in dplyr using slice_sample() function

We'll randomly select two rows and do it twice so show that they are random


```r
mtcars %>% slice_sample(n=2)
```

```
## # A tibble: 2 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  21       6  160    110  3.9   2.88  17.0     0     1     4     4
## 2  15.2     8  276.   180  3.07  3.78  18       0     0     3     3
```

```r
mtcars %>% slice_sample(n=2)
```

```
## # A tibble: 2 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  22.8     4   108    93  3.85  2.32  18.6     1     1     4     1
## 2  21       6   160   110  3.9   2.88  17.0     0     1     4     4
```
Can also slice a proportion of the data.  Here 10% of 32 records returns 3 random records

```r
mtcars %>% slice_sample(prop=0.1)
```

```
## # A tibble: 3 × 11
##     mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##   <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
## 1  13.3     8   350   245  3.73  3.84  15.4     0     0     3     4
## 2  15.2     8   304   150  3.15  3.44  17.3     0     0     3     2
## 3  10.4     8   472   205  2.93  5.25  18.0     0     0     3     4
```



## Head, Tail, Glimpse with dplyr

head and tail can be passed into the pipe using %>%


```r
iris %>% head()
```

```
##   Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1          5.1         3.5          1.4         0.2  setosa
## 2          4.9         3.0          1.4         0.2  setosa
## 3          4.7         3.2          1.3         0.2  setosa
## 4          4.6         3.1          1.5         0.2  setosa
## 5          5.0         3.6          1.4         0.2  setosa
## 6          5.4         3.9          1.7         0.4  setosa
```

```r
iris %>% tail()
```

```
##     Sepal.Length Sepal.Width Petal.Length Petal.Width   Species
## 145          6.7         3.3          5.7         2.5 virginica
## 146          6.7         3.0          5.2         2.3 virginica
## 147          6.3         2.5          5.0         1.9 virginica
## 148          6.5         3.0          5.2         2.0 virginica
## 149          6.2         3.4          5.4         2.3 virginica
## 150          5.9         3.0          5.1         1.8 virginica
```

```r
iris %>% head(n=20)
```

```
##    Sepal.Length Sepal.Width Petal.Length Petal.Width Species
## 1           5.1         3.5          1.4         0.2  setosa
## 2           4.9         3.0          1.4         0.2  setosa
## 3           4.7         3.2          1.3         0.2  setosa
## 4           4.6         3.1          1.5         0.2  setosa
## 5           5.0         3.6          1.4         0.2  setosa
## 6           5.4         3.9          1.7         0.4  setosa
## 7           4.6         3.4          1.4         0.3  setosa
## 8           5.0         3.4          1.5         0.2  setosa
## 9           4.4         2.9          1.4         0.2  setosa
## 10          4.9         3.1          1.5         0.1  setosa
## 11          5.4         3.7          1.5         0.2  setosa
## 12          4.8         3.4          1.6         0.2  setosa
## 13          4.8         3.0          1.4         0.1  setosa
## 14          4.3         3.0          1.1         0.1  setosa
## 15          5.8         4.0          1.2         0.2  setosa
## 16          5.7         4.4          1.5         0.4  setosa
## 17          5.4         3.9          1.3         0.4  setosa
## 18          5.1         3.5          1.4         0.3  setosa
## 19          5.7         3.8          1.7         0.3  setosa
## 20          5.1         3.8          1.5         0.3  setosa
```

dplyr also has the "glimpse()" function that gives an alternative view of the data


```r
iris %>% glimpse()
```

```
## Rows: 150
## Columns: 5
## $ Sepal.Length <dbl> 5.1, 4.9, 4.7, 4.6, 5.0, 5.4, 4.6, 5.0, 4.4, 4.9, 5.4, 4.…
## $ Sepal.Width  <dbl> 3.5, 3.0, 3.2, 3.1, 3.6, 3.9, 3.4, 3.4, 2.9, 3.1, 3.7, 3.…
## $ Petal.Length <dbl> 1.4, 1.4, 1.3, 1.5, 1.4, 1.7, 1.4, 1.5, 1.4, 1.5, 1.5, 1.…
## $ Petal.Width  <dbl> 0.2, 0.2, 0.2, 0.2, 0.2, 0.4, 0.3, 0.2, 0.2, 0.1, 0.2, 0.…
## $ Species      <fct> setosa, setosa, setosa, setosa, setosa, setosa, setosa, s…
```


##  Assigning and Subsetting

Sometimes you want to select data so that you can reassign values in the data frame. This is useful when you are cleaning up your data.


```r
# for example, sometimes you want to replace NA values with 0's

data3<-data.frame(site=c(1,1,1,2,2,2),count=c(2,4,3,NA,5,NA))
data3
```

```
##   site count
## 1    1     2
## 2    1     4
## 3    1     3
## 4    2    NA
## 5    2     5
## 6    2    NA
```

```r
# to select rows where count is NA you can use the is.na() function

data3[is.na(data3$count),]
```

```
##   site count
## 4    2    NA
## 6    2    NA
```

```r
# to set count to zero where count was NA

data3[is.na(data3$count),]$count<-0

data3
```

```
##   site count
## 1    1     2
## 2    1     4
## 3    1     3
## 4    2     0
## 5    2     5
## 6    2     0
```

This is much easier with dplyr using mutate() and replace()

The usage is replace(variable, condition, replacement)


```r
data3<-data.frame(site=c(1,1,1,2,2,2),count=c(2,4,3,NA,5,NA))

data3 %>% mutate(count = replace(count, is.na(count), 0))
```

```
##   site count
## 1    1     2
## 2    1     4
## 3    1     3
## 4    2     0
## 5    2     5
## 6    2     0
```

```r
data3 %>% mutate(count = replace(count, site==2, 100))
```

```
##   site count
## 1    1     2
## 2    1     4
## 3    1     3
## 4    2   100
## 5    2   100
## 6    2   100
```

Mutate can also be used to create new variables

```r
iris %>% mutate(Sepal.Area = Sepal.Length * Sepal.Width)
```

```
##     Sepal.Length Sepal.Width Petal.Length Petal.Width    Species Sepal.Area
## 1            5.1         3.5          1.4         0.2     setosa      17.85
## 2            4.9         3.0          1.4         0.2     setosa      14.70
## 3            4.7         3.2          1.3         0.2     setosa      15.04
## 4            4.6         3.1          1.5         0.2     setosa      14.26
## 5            5.0         3.6          1.4         0.2     setosa      18.00
## 6            5.4         3.9          1.7         0.4     setosa      21.06
## 7            4.6         3.4          1.4         0.3     setosa      15.64
## 8            5.0         3.4          1.5         0.2     setosa      17.00
## 9            4.4         2.9          1.4         0.2     setosa      12.76
## 10           4.9         3.1          1.5         0.1     setosa      15.19
## 11           5.4         3.7          1.5         0.2     setosa      19.98
## 12           4.8         3.4          1.6         0.2     setosa      16.32
## 13           4.8         3.0          1.4         0.1     setosa      14.40
## 14           4.3         3.0          1.1         0.1     setosa      12.90
## 15           5.8         4.0          1.2         0.2     setosa      23.20
## 16           5.7         4.4          1.5         0.4     setosa      25.08
## 17           5.4         3.9          1.3         0.4     setosa      21.06
## 18           5.1         3.5          1.4         0.3     setosa      17.85
## 19           5.7         3.8          1.7         0.3     setosa      21.66
## 20           5.1         3.8          1.5         0.3     setosa      19.38
## 21           5.4         3.4          1.7         0.2     setosa      18.36
## 22           5.1         3.7          1.5         0.4     setosa      18.87
## 23           4.6         3.6          1.0         0.2     setosa      16.56
## 24           5.1         3.3          1.7         0.5     setosa      16.83
## 25           4.8         3.4          1.9         0.2     setosa      16.32
## 26           5.0         3.0          1.6         0.2     setosa      15.00
## 27           5.0         3.4          1.6         0.4     setosa      17.00
## 28           5.2         3.5          1.5         0.2     setosa      18.20
## 29           5.2         3.4          1.4         0.2     setosa      17.68
## 30           4.7         3.2          1.6         0.2     setosa      15.04
## 31           4.8         3.1          1.6         0.2     setosa      14.88
## 32           5.4         3.4          1.5         0.4     setosa      18.36
## 33           5.2         4.1          1.5         0.1     setosa      21.32
## 34           5.5         4.2          1.4         0.2     setosa      23.10
## 35           4.9         3.1          1.5         0.2     setosa      15.19
## 36           5.0         3.2          1.2         0.2     setosa      16.00
## 37           5.5         3.5          1.3         0.2     setosa      19.25
## 38           4.9         3.6          1.4         0.1     setosa      17.64
## 39           4.4         3.0          1.3         0.2     setosa      13.20
## 40           5.1         3.4          1.5         0.2     setosa      17.34
## 41           5.0         3.5          1.3         0.3     setosa      17.50
## 42           4.5         2.3          1.3         0.3     setosa      10.35
## 43           4.4         3.2          1.3         0.2     setosa      14.08
## 44           5.0         3.5          1.6         0.6     setosa      17.50
## 45           5.1         3.8          1.9         0.4     setosa      19.38
## 46           4.8         3.0          1.4         0.3     setosa      14.40
## 47           5.1         3.8          1.6         0.2     setosa      19.38
## 48           4.6         3.2          1.4         0.2     setosa      14.72
## 49           5.3         3.7          1.5         0.2     setosa      19.61
## 50           5.0         3.3          1.4         0.2     setosa      16.50
## 51           7.0         3.2          4.7         1.4 versicolor      22.40
## 52           6.4         3.2          4.5         1.5 versicolor      20.48
## 53           6.9         3.1          4.9         1.5 versicolor      21.39
## 54           5.5         2.3          4.0         1.3 versicolor      12.65
## 55           6.5         2.8          4.6         1.5 versicolor      18.20
## 56           5.7         2.8          4.5         1.3 versicolor      15.96
## 57           6.3         3.3          4.7         1.6 versicolor      20.79
## 58           4.9         2.4          3.3         1.0 versicolor      11.76
## 59           6.6         2.9          4.6         1.3 versicolor      19.14
## 60           5.2         2.7          3.9         1.4 versicolor      14.04
## 61           5.0         2.0          3.5         1.0 versicolor      10.00
## 62           5.9         3.0          4.2         1.5 versicolor      17.70
## 63           6.0         2.2          4.0         1.0 versicolor      13.20
## 64           6.1         2.9          4.7         1.4 versicolor      17.69
## 65           5.6         2.9          3.6         1.3 versicolor      16.24
## 66           6.7         3.1          4.4         1.4 versicolor      20.77
## 67           5.6         3.0          4.5         1.5 versicolor      16.80
## 68           5.8         2.7          4.1         1.0 versicolor      15.66
## 69           6.2         2.2          4.5         1.5 versicolor      13.64
## 70           5.6         2.5          3.9         1.1 versicolor      14.00
## 71           5.9         3.2          4.8         1.8 versicolor      18.88
## 72           6.1         2.8          4.0         1.3 versicolor      17.08
## 73           6.3         2.5          4.9         1.5 versicolor      15.75
## 74           6.1         2.8          4.7         1.2 versicolor      17.08
## 75           6.4         2.9          4.3         1.3 versicolor      18.56
## 76           6.6         3.0          4.4         1.4 versicolor      19.80
## 77           6.8         2.8          4.8         1.4 versicolor      19.04
## 78           6.7         3.0          5.0         1.7 versicolor      20.10
## 79           6.0         2.9          4.5         1.5 versicolor      17.40
## 80           5.7         2.6          3.5         1.0 versicolor      14.82
## 81           5.5         2.4          3.8         1.1 versicolor      13.20
## 82           5.5         2.4          3.7         1.0 versicolor      13.20
## 83           5.8         2.7          3.9         1.2 versicolor      15.66
## 84           6.0         2.7          5.1         1.6 versicolor      16.20
## 85           5.4         3.0          4.5         1.5 versicolor      16.20
## 86           6.0         3.4          4.5         1.6 versicolor      20.40
## 87           6.7         3.1          4.7         1.5 versicolor      20.77
## 88           6.3         2.3          4.4         1.3 versicolor      14.49
## 89           5.6         3.0          4.1         1.3 versicolor      16.80
## 90           5.5         2.5          4.0         1.3 versicolor      13.75
## 91           5.5         2.6          4.4         1.2 versicolor      14.30
## 92           6.1         3.0          4.6         1.4 versicolor      18.30
## 93           5.8         2.6          4.0         1.2 versicolor      15.08
## 94           5.0         2.3          3.3         1.0 versicolor      11.50
## 95           5.6         2.7          4.2         1.3 versicolor      15.12
## 96           5.7         3.0          4.2         1.2 versicolor      17.10
## 97           5.7         2.9          4.2         1.3 versicolor      16.53
## 98           6.2         2.9          4.3         1.3 versicolor      17.98
## 99           5.1         2.5          3.0         1.1 versicolor      12.75
## 100          5.7         2.8          4.1         1.3 versicolor      15.96
## 101          6.3         3.3          6.0         2.5  virginica      20.79
## 102          5.8         2.7          5.1         1.9  virginica      15.66
## 103          7.1         3.0          5.9         2.1  virginica      21.30
## 104          6.3         2.9          5.6         1.8  virginica      18.27
## 105          6.5         3.0          5.8         2.2  virginica      19.50
## 106          7.6         3.0          6.6         2.1  virginica      22.80
## 107          4.9         2.5          4.5         1.7  virginica      12.25
## 108          7.3         2.9          6.3         1.8  virginica      21.17
## 109          6.7         2.5          5.8         1.8  virginica      16.75
## 110          7.2         3.6          6.1         2.5  virginica      25.92
## 111          6.5         3.2          5.1         2.0  virginica      20.80
## 112          6.4         2.7          5.3         1.9  virginica      17.28
## 113          6.8         3.0          5.5         2.1  virginica      20.40
## 114          5.7         2.5          5.0         2.0  virginica      14.25
## 115          5.8         2.8          5.1         2.4  virginica      16.24
## 116          6.4         3.2          5.3         2.3  virginica      20.48
## 117          6.5         3.0          5.5         1.8  virginica      19.50
## 118          7.7         3.8          6.7         2.2  virginica      29.26
## 119          7.7         2.6          6.9         2.3  virginica      20.02
## 120          6.0         2.2          5.0         1.5  virginica      13.20
## 121          6.9         3.2          5.7         2.3  virginica      22.08
## 122          5.6         2.8          4.9         2.0  virginica      15.68
## 123          7.7         2.8          6.7         2.0  virginica      21.56
## 124          6.3         2.7          4.9         1.8  virginica      17.01
## 125          6.7         3.3          5.7         2.1  virginica      22.11
## 126          7.2         3.2          6.0         1.8  virginica      23.04
## 127          6.2         2.8          4.8         1.8  virginica      17.36
## 128          6.1         3.0          4.9         1.8  virginica      18.30
## 129          6.4         2.8          5.6         2.1  virginica      17.92
## 130          7.2         3.0          5.8         1.6  virginica      21.60
## 131          7.4         2.8          6.1         1.9  virginica      20.72
## 132          7.9         3.8          6.4         2.0  virginica      30.02
## 133          6.4         2.8          5.6         2.2  virginica      17.92
## 134          6.3         2.8          5.1         1.5  virginica      17.64
## 135          6.1         2.6          5.6         1.4  virginica      15.86
## 136          7.7         3.0          6.1         2.3  virginica      23.10
## 137          6.3         3.4          5.6         2.4  virginica      21.42
## 138          6.4         3.1          5.5         1.8  virginica      19.84
## 139          6.0         3.0          4.8         1.8  virginica      18.00
## 140          6.9         3.1          5.4         2.1  virginica      21.39
## 141          6.7         3.1          5.6         2.4  virginica      20.77
## 142          6.9         3.1          5.1         2.3  virginica      21.39
## 143          5.8         2.7          5.1         1.9  virginica      15.66
## 144          6.8         3.2          5.9         2.3  virginica      21.76
## 145          6.7         3.3          5.7         2.5  virginica      22.11
## 146          6.7         3.0          5.2         2.3  virginica      20.10
## 147          6.3         2.5          5.0         1.9  virginica      15.75
## 148          6.5         3.0          5.2         2.0  virginica      19.50
## 149          6.2         3.4          5.4         2.3  virginica      21.08
## 150          5.9         3.0          5.1         1.8  virginica      17.70
```



##  Ordering

Ordering data in base R is annoying. I'm not even going to bother showing it to you. But it's pretty simple with dplyr's arrange() function.


```r
# ascending
mtcars %>% arrange(mpg)  
```

```
## # A tibble: 32 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  10.4     8  472    205  2.93  5.25  18.0     0     0     3     4
##  2  10.4     8  460    215  3     5.42  17.8     0     0     3     4
##  3  13.3     8  350    245  3.73  3.84  15.4     0     0     3     4
##  4  14.3     8  360    245  3.21  3.57  15.8     0     0     3     4
##  5  14.7     8  440    230  3.23  5.34  17.4     0     0     3     4
##  6  15       8  301    335  3.54  3.57  14.6     0     1     5     8
##  7  15.2     8  276.   180  3.07  3.78  18       0     0     3     3
##  8  15.2     8  304    150  3.15  3.44  17.3     0     0     3     2
##  9  15.5     8  318    150  2.76  3.52  16.9     0     0     3     2
## 10  15.8     8  351    264  4.22  3.17  14.5     0     1     5     4
## # … with 22 more rows
```

```r
#descending
mtcars %>% arrange(desc(mpg))
```

```
## # A tibble: 32 × 11
##      mpg   cyl  disp    hp  drat    wt  qsec    vs    am  gear  carb
##    <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl> <dbl>
##  1  33.9     4  71.1    65  4.22  1.84  19.9     1     1     4     1
##  2  32.4     4  78.7    66  4.08  2.2   19.5     1     1     4     1
##  3  30.4     4  75.7    52  4.93  1.62  18.5     1     1     4     2
##  4  30.4     4  95.1   113  3.77  1.51  16.9     1     1     5     2
##  5  27.3     4  79      66  4.08  1.94  18.9     1     1     4     1
##  6  26       4 120.     91  4.43  2.14  16.7     0     1     5     2
##  7  24.4     4 147.     62  3.69  3.19  20       1     0     4     2
##  8  22.8     4 108      93  3.85  2.32  18.6     1     1     4     1
##  9  22.8     4 141.     95  3.92  3.15  22.9     1     0     4     2
## 10  21.5     4 120.     97  3.7   2.46  20.0     1     0     3     1
## # … with 22 more rows
```


## Bonus Material

Here's a cheat sheet for wrangling data with dplyr.  

https://rstudio.github.io/cheatsheets/data-transformation.pdf

We still have much to cover with dplyr as well as the related package called tidyr.

## Homework

Using the data set you found, write  R code to create 3 interesting subsets of data that you might want to use for later analysis.  Use which ever methods make the most sense to you but be sure to assign these subsets to new variables with meaningful names. Remember to add code to import this data first.




