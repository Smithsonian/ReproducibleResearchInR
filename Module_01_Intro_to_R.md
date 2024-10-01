---
title: 'Module 1:  Introduction to R'
author: "Brian P Steves"
date: "2024-09-27"
output:
  html_document:
    keep_md: yes
---



Module 1: Introduction to R
====================

## 1 Installing R

R is open source, free, and installs on most computing platforms including Linux, Windows and MacOS.  You should be able to find a compatible download of the most recent version of R at the follwing URL.

http://www.r-project.org/

Follow the instructions provided for you operating system.

## 2 Installing RStudio IDE (inegrated development environment)
RStudio  an integrated development environment for R meaning it provides a suite of tools to help you interact with R.  

It contains a code editor with sntax highlighting, code completion and smart indentation.   It also provides a well thought out layout for you to access your command history, current list of objects, plots, help, files, packages, etc.. from within on application.

There are even some more advanced features concerning report generation and version control integration which we will cover towards the end of class.
  
RStudio is also free, available for Windows, MacOS, and linux and can be downloaded for installation from the following URL. 

http://www.rstudio.com/


Follow the instructions provided for you operating system.

## 3 Basics of R

### 3.1  Interactive R on the Console

In other words, entering code line by line rather than from a script.

#### 3.1.1   Starting and stopping R

To start R from the command line simply type "R" and you'll get something like the following.

```{}
R version 3.0.3 (2014-03-06) -- "Warm Puppy"
Copyright (C) 2014 The R Foundation for Statistical Computing
Platform: x86_64-pc-linux-gnu (64-bit)

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
```

In RStudio, this console has its own window called "Console" and should start up automatically when you start RStudio.

To quit R use the following command at the console prompt


```r
q()
```
 of if you quit RStudio it will quit you out of R.


#### 3.1.2  Getting help in R

You can get help on a specific topic using the "help()" function.  An alternative shortcut to help is "?"


```r
help("lm")
```
While using "?" is usually easier, there are time when the full help function is better.   For example "?if" will not evaluate while "help('if')" returns a help file about "Control Flow" which is probably what you want.


You can also search the help files using "help.search()" function when you don't know the exact command you want help on.  The short cut to this is to use "??".


```r
help.search("lm")
```

To run examples from a paticular function...


```r
example("lm")
```


#### 3.1.3  Assignment of data structures to objects

To can assign a data structure to an object using "<-" or "->" or the "assign()" function.  The following are all equivalent.


```r
x<-c(10,7,4,5)

c(10,7,4,5) -> x

assign("x", c(10,7,4,5))
```

Calling the object by name with print it


```r
x
```

```
## [1] 10  7  4  5
```

If you don't assign a result to an object the resulting value is printed and lost.


```r
c(10,7,4,5)
```

```
## [1] 10  7  4  5
```


#### 3.1.4  Listing of Objects

All of the current ojects in memory can be listed using the "ls()" or "objects()" functions.


```r
ls()
```

```
## [1] "x"
```

#### 3.1.5  Recalling previous commands

While at the console, the up and down arrows will cycle the command prompt with the previously executed commands.


### 3.2  R Script files

Entering lines of code into the console might be fun but we can combine a series of commands into an R script file.  These files are simply text files that end with the ".r" or ".R" extension and contain a series of R commands.

Once an R script is written and saved it can be evaluated in R using the "source()" command.

If you plan on running more than a couple lines of code it really helps to use script files as it is much easier to edit a script file and rerun it than it is to retype a long series of commands over again.


```r
source("myScript.R")
```

## 4  Contributed Packages

One of the great things about R is the diversity of code that has been written and is freely available to everyone.   The most common way people share R code is as a package of functions, usually with a unifing theme.

### 4.1 Finding Packages

#### 4.1.1 CRAN Task Views
Finding an appropriate package can be a bit of hit or miss as the quality ranges from exceptional to awful. One good place to start are the "Task Views" maintained on the main R project server.

http://cran.r-project.org/web/views/

For example, if you are interested in "Reproducible Research" there is a Task View for that...
http://cran.r-project.org/web/views/ReproducibleResearch.html

This task view is an annotated list of packages that relate to reproducible research.

Another important task view for ecologists and environmental scientists is the "Analysis of Ecological and Environmental Data" task view...

http://cran.r-project.org/web/views/Environmetrics.html


#### 4.1.2 Searching Google
If you already know which statistical technique you are looking to employ but don't know which R package might need you can always search Google for it.  Unfortunately, the letter "R" isn't much of a unique name for a Google search on R code. However, if you change "R" to  "CRAN R" in that query to refer to the "Comprehensive R Archive Network" you will often get better results.

### 4.2 Installing Packages
Once you know which R package you want to install you use the "install.packages()" command to install it.


```r
install.packages("vegan", repos='http://cran.us.r-project.org')
```

```
## 
##   There is a binary version available but the source version is later:
##       binary source needs_compilation
## vegan  2.6-4  2.6-8              TRUE
```
If you haven't told R or RStudio where you want to download this package from, it may ask you for you to select a mirror.  You'll probably want to pick either the closest mirror server or one that you feel is the quickest.    Once the package is downloaded, R will attempt to install it on your computer.  If anything goes wrong in the installation an error will be reported.  Packages can be installed for all users on the computer or just one specific user.  If you don't have full admin rights on your computer your package will be installed in a local user library of packages.

### 4.3 Loading Packages
To load an install package for use you use the "library()" function.


```r
library(vegan)
```

##  Homework

1. Install the latest versions of R onto your computer.
2. Install the latest version of RStudio onto your computer.
3. Find and install at least one R package.
