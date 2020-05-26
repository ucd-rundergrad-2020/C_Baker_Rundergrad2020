---
title: "Functions + Loops"
author: "Cassandra"
date: "5/18/2020"
output: 
  html_document: 
    keep_md: yes
editor_options: 
  chunk_output_type: console
---




```r
library(tidyverse)
library(lubridate)
library(nycflights13)
```


## Chapter 19 

### 19.2.1 

**3. Practice turning the following code snippets into functions. Think about what each function does. What would you call it? How many arguments does it need? Can you rewrite it to be more expressive or less duplicative?** 
```
mean(is.na(x))

x / sum(x, na.rm = TRUE)

sd(x, na.rm = TRUE) / mean(x, na.rm = TRUE)
```


```r
test_vector <- sample(c(rnorm(20), rep(NA, 40)))
test_numbers <- sample(1:100, size = 20)

prop_missing <- function(x) {
  mean(is.na(x))
}

prop_missing(test_vector)
```

```
## [1] 0.6666667
```

```r
prop_missing(test_numbers)
```

```
## [1] 0
```


```r
prop_rescale <- function(x) {
  x / sum(x, na.rm = TRUE)
}

prop_rescale(test_vector)
```

```
##  [1] -0.091337180           NA           NA           NA           NA
##  [6]  0.006411629           NA  0.461682883           NA           NA
## [11]           NA  0.111919227           NA           NA           NA
## [16]           NA           NA           NA           NA  0.260547625
## [21]  0.316221887           NA -0.182143107           NA  0.584922174
## [26] -0.214544818 -0.688057559           NA           NA  0.057703661
## [31]           NA           NA -0.494119462  0.317667405           NA
## [36]  0.041676109           NA           NA -0.084763891           NA
## [41]           NA           NA           NA           NA           NA
## [46]           NA           NA -0.127919267           NA           NA
## [51]           NA           NA           NA  0.497453484           NA
## [56]  0.208948337  0.138262796 -0.120531933           NA           NA
```

```r
prop_rescale(test_numbers)
```

```
##  [1] 0.082004556 0.026195900 0.059225513 0.101366743 0.039863326 0.094533030
##  [7] 0.067198178 0.020501139 0.004555809 0.099088838 0.041002278 0.050113895
## [13] 0.010250569 0.001138952 0.047835991 0.075170843 0.034168565 0.088838269
## [19] 0.014806378 0.042141230
```


```r
coeff_var <- function(x) {
  sd(x, na.rm = TRUE) / mean(x, na.rm = TRUE)
}

coeff_var(test_vector)
```

```
## [1] -6.39926
```

```r
coeff_var(test_numbers)
```

```
## [1] 0.6454279
```

### 19.4.4

**2. Write a greeting function that says “good morning”, “good afternoon”, or “good evening”, depending on the time of day. (Hint: use a time argument that defaults to `lubridate::now()`. That will make it easier to test your function.)**    

```r
greeting <- function(x) {
  time <- as.integer(format(now(), "%H%M"))
  if (time < 1200) {
    print("Good morning")
  } else if (time >= 1700) {
    print("Good evening") 
  } else {
    print("Good afternoon")
  }
}

now()
```

```
## [1] "2020-05-25 23:52:53 PDT"
```

```r
greeting()
```

```
## [1] "Good evening"
```

**3. Implement a `fizzbuzz` function. It takes a single number as input. If the number is divisible by three, it returns “fizz”. If it’s divisible by five it returns “buzz”. If it’s divisible by three and five, it returns “fizzbuzz”. Otherwise, it returns the number. Make sure you first write working code before you create the function.**   

```r
fizzbuzz <- function(x) {
  three <- x%%3 == 0 
  five <- x%%5 == 0 
  if (three == TRUE && five == FALSE) {
    print("fizz")
  } else if (three == FALSE && five == TRUE) {
    print("buzz")
  } else if (three == TRUE && five == TRUE) {
    print("fizzbuzz")
  } else {
    print(x)
  }
}

fizzbuzz(30)
```

```
## [1] "fizzbuzz"
```

```r
fizzbuzz(25)
```

```
## [1] "buzz"
```

```r
fizzbuzz(21)
```

```
## [1] "fizz"
```

```r
fizzbuzz(7)
```

```
## [1] 7
```

## Chapter 21

### 21.2.1    

**1. Write for loops to:**

  1. Compute the mean of every column in mtcars.
  2. Determine the type of each column in nycflights13::flights.
  3. Compute the number of unique values in each column of iris.
  4. Generate 10 random normals from distributions with means of -10, 0, 10, and 100.  
  
**Think about the output, sequence, and body before you start writing the loop.**     

```r
# 1. compute the mean of every column in mtcars 
col_mean <- vector("double", ncol(mtcars)) 
for (i in seq_along(mtcars)) {
  col_mean[[i]] <- mean(mtcars[[i]])
}
col_mean
```

```
##  [1]  20.090625   6.187500 230.721875 146.687500   3.596563   3.217250
##  [7]  17.848750   0.437500   0.406250   3.687500   2.812500
```

```r
# can it be prettier? 
cars_mean <- tibble(
  col = colnames(mtcars),
  col_mean = vector("double", length = ncol(mtcars))
)

for (i in seq_along(mtcars)) {
  cars_mean$col_mean[[i]] <- mean(mtcars[[i]])
}
cars_mean
```

```
## # A tibble: 11 x 2
##    col   col_mean
##    <chr>    <dbl>
##  1 mpg     20.1  
##  2 cyl      6.19 
##  3 disp   231.   
##  4 hp     147.   
##  5 drat     3.60 
##  6 wt       3.22 
##  7 qsec    17.8  
##  8 vs       0.438
##  9 am       0.406
## 10 gear     3.69 
## 11 carb     2.81
```

```r
# the numbers aren't pretty, but it's nice to have the column names... 
```


```r
# 2. determine the type of each column in flights 
col_type <- vector("character", ncol(flights))
for (i in seq_along(flights)) {
  col_type[[i]] <- typeof(flights[[i]])
}
col_type
```

```
##  [1] "integer"   "integer"   "integer"   "integer"   "integer"   "double"   
##  [7] "integer"   "integer"   "double"    "character" "integer"   "character"
## [13] "character" "character" "double"    "double"    "double"    "double"   
## [19] "double"
```

```r
# add some names too 
flights_type <- tibble(
  col = colnames(flights),
  col_type = vector("character", length = ncol(flights))
)

for (i in seq_along(flights)) {
  flights_type$col_type[[i]] <- typeof(flights[[i]])
}
flights_type
```

```
## # A tibble: 19 x 2
##    col            col_type 
##    <chr>          <chr>    
##  1 year           integer  
##  2 month          integer  
##  3 day            integer  
##  4 dep_time       integer  
##  5 sched_dep_time integer  
##  6 dep_delay      double   
##  7 arr_time       integer  
##  8 sched_arr_time integer  
##  9 arr_delay      double   
## 10 carrier        character
## 11 flight         integer  
## 12 tailnum        character
## 13 origin         character
## 14 dest           character
## 15 air_time       double   
## 16 distance       double   
## 17 hour           double   
## 18 minute         double   
## 19 time_hour      double
```

### 21.3.5 

**3. Write a function that prints the mean of each numeric column in a data frame, along with its name. For example, `show_mean(iris)` would print:** 
```
show_mean(iris)
#> Sepal.Length: 5.84
#> Sepal.Width:  3.06
#> Petal.Length: 3.76
#> Petal.Width:  1.20
```


```r
# preliminary function to get numeric column names and means 
find_mean <- function(df) {
  num_col <- select_if(df, is.numeric)
  avg <- vector("double", length = ncol(num_col))
  names(avg) <- names(num_col)
  for (i in seq_along(num_col)) {
    avg[[i]] <- mean(num_col[[i]])
  }
  avg
}

find_mean(iris)
```

```
## Sepal.Length  Sepal.Width Petal.Length  Petal.Width 
##     5.843333     3.057333     3.758000     1.199333
```

```r
# trying to match R4DS output
show_mean <- function(df) {
  num_col <- select_if(df, is.numeric)
  avg <- tibble(
    col_name = names(num_col),
    col_mean = NA
  )
  for (i in seq_along(num_col)) {
    avg$col_mean[[i]] <- round(mean(num_col[[i]]), digits = 2)
  }
  for (i in seq_along(num_col)) {
    cat(avg$col_name[[i]], ": \t", avg$col_mean[[i]], "\n")
  }
}

show_mean(iris)
```

```
## Sepal.Length : 	 5.84 
## Sepal.Width : 	 3.06 
## Petal.Length : 	 3.76 
## Petal.Width : 	 1.2
```

```r
# eh this is good enough for me
```

### 21.5.3    

**1. Write code that uses one of the map functions to:** 

  1. Compute the mean of every column in mtcars.
  2. Determine the type of each column in nycflights13::flights.
  3. Compute the number of unique values in each column of iris.
  4. Generate 10 random normals from distributions with means of -10, 0, 10, and 100.    
  

```r
# 1. compute the mean of every column in mtcars 
map_dbl(mtcars, mean)
```

```
##        mpg        cyl       disp         hp       drat         wt       qsec 
##  20.090625   6.187500 230.721875 146.687500   3.596563   3.217250  17.848750 
##         vs         am       gear       carb 
##   0.437500   0.406250   3.687500   2.812500
```

```r
# wow, so fast 
```


```r
# 2. determine the type of each column in flights
map_chr(flights, typeof)
```

```
##           year          month            day       dep_time sched_dep_time 
##      "integer"      "integer"      "integer"      "integer"      "integer" 
##      dep_delay       arr_time sched_arr_time      arr_delay        carrier 
##       "double"      "integer"      "integer"       "double"    "character" 
##         flight        tailnum         origin           dest       air_time 
##      "integer"    "character"    "character"    "character"       "double" 
##       distance           hour         minute      time_hour 
##       "double"       "double"       "double"       "double"
```

