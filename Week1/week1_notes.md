---
title: "Week1: Markdown + Swirl"
author: "Cassandra"
date: "4/13/2020"
output: 
  html_document: 
    keep_md: yes
editor_options: 
  chunk_output_type: console
---



## Markdown Tutorial

### Bold and Italics

To include *italics*, use `_` or `*`.  
To include **bold**, use `__` or `**`.  
To make **_bold italics_**, it is most clear to use `_` for one format and `*` for the other.  

### Headers

Use `#` to denote headers. There are six sizes of headers, formatted by the corresponding number of `#` before the header.   
**Note:** R markdown will not read headers correctly when knitting unless there is a space between the `#` and your header characters.  

### Links

To make an inline link, write the text you'd like to display in `[]`, followed by the link in `()`.    
If you get stuck with something,try [searching](www.google.com) for answers! 

Reference links are the other type of link and reference one "master" link at the bottom of your document that won't show up in the finished file. This is useful for easily updating multiple links to change the destination.   
To create a reference link, write the text you'd like to display in `[]`, followed by a reference tag in `[]`. Then at the bottom of your document, direct your tag to a website with `[tag]: website_url`.  
Remember to commit and push changes to [Github][Rundergrad-Github]!  

### Images 

Similar to links, you can include inline image links in markdown by placing `!` before the link. Instead of placing the inline text in the `[]`, include text to explain the image for the visually impaired.   
Why is Github's mascot an octocat?  
![Github octocat](https://octodex.github.com/images/original.png)   

Images can also be included as reference images, similar to links, by placing `!` before the link.  
My vote for Rundergrad mascot.  
![sleeping Kit][Kit]

### Blockquotes 

To create a blockquote, place `>` in front of the text. If the blockquote spans multiple lines, include `>` at the start of each line (even blank lines) to ensure the quote is properly grouped together.  

As Garrett Grolemund and Hadley Wickham say:    

> "If you get stuck, start with Google."

### Lists 

To create an unordered list, use `*` in front of each item on a separate line. 

To create an ordered list, use numbers instead.   

You can even include additional paragraphs below a bullet point by indenting that line.  

**Black Milk Tea**  

* Ingredients   
  * 15g Black tea  
  * 130 mL whole milk   
  * 30 mL cane sugar  
* To make 
  1. Steep tea in 200 mL water for 10 minutes   
  2. To 150 mL hot tea, add whole milk   
  3. Add cane sugar  
    Don't forget to mix!
  4. Add 300 mL ice   
    Amount can vary based on personal preference  

### Paragraphs 

Both hard breaks and soft breaks will start a new line, but they have different appearances. To introduce a hard break, skip a line between two text chunks to create a new paragraph. If you want to start a new line but group two text chunks together, introduce a soft break by adding two spaces to the end of your text line.  

Hard breaks are required for bullet points to render correctly, but soft breaks can be useful for:   

  * Keeping bullet points and notes together  
    when you want to add an indented paragraph  
  * Otherwise, they end up spaced out  
  
    so the text isn't grouped together as nicely 
    
## Swirl 

### R Programming 

**Shortcuts**  

* Assignment operator: `Alt` + `-` = ` <- `  
* Pipe: `Ctrl` + `Shift` + `M` = ` %>% `  
* New code chunk: `Ctrl` + `Alt` + `I` 

**Tips**  

* Use `?` to find the help file for a function.   
  Don't include parentheses after the function name.  
  To view the help file for operators, surround the operator with `` ` ``.
* Use `Tab` to automatically complete names/functions.  
  If you press `Tab` and wait it will show a list of possible endings to what you've started typing.  
  Then you can select the option you want instead of typing the whole thing out.  
* Use the up arrow to cycle through previously entered commands.   
  This is useful for re-running an earlier command or editing the command if you made a mistake.

#### 1. Basic Building Blocks 

When assigning something to a variable, R will store the result instead of outputting it. If you want R to create the variable and output the result at the same time, surround your assignment with `()`.   

```r
(x <- 5+7)
```

```
## [1] 12
```

Create a vector with `c()` to concatenate multiple values together.  

```r
z <- c(1.1, 9, 3.14)
```

Vectors can be used for downstream calculations.  

```r
c(z, 555, z)
```

```
## [1]   1.10   9.00   3.14 555.00   1.10   9.00   3.14
```

```r
z * 2 + 100
```

```
## [1] 102.20 118.00 106.28
```

**Note:** When R is performing operations on vectors, it will do so for each element of the vector. If you are working with two vectors of different lengths, R will recycle the shorter vector to be the same length as the longer vector.  

```r
c(1, 2, 3, 4) + c(0, 10)
```

```
## [1]  1 12  3 14
```

#### 3. Sequences of Numbers

Create a basic sequence of numbers in increments of 1 using `:`.   

```r
pi:10 
```

```
## [1] 3.141593 4.141593 5.141593 6.141593 7.141593 8.141593 9.141593
```

Use `seq()` to create a more advanced sequence of numbers.  

```r
seq(0, 10, by = 0.5)
```

```
##  [1]  0.0  0.5  1.0  1.5  2.0  2.5  3.0  3.5  4.0  4.5  5.0  5.5  6.0  6.5  7.0
## [16]  7.5  8.0  8.5  9.0  9.5 10.0
```

```r
my_seq <- seq(0, 10, length = 30)
```

There are often multiple ways to code the same solution to a problem. For example, a few ways to generate a sequence the same length as `my_seq`.  
```
1:length(my_seq)  
seq(along.with = my_seq)  
seq_along(my_seq)
```

Use `rep()` to create a vector of replicates.  

```r
rep(c(0, 1, 2), times = 10)
```

```
##  [1] 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2 0 1 2
```

```r
rep(c(0, 1, 2), each = 10)
```

```
##  [1] 0 0 0 0 0 0 0 0 0 0 1 1 1 1 1 1 1 1 1 1 2 2 2 2 2 2 2 2 2 2
```

#### 4. Vectors 

Atomic vectors are vectors with only one data type, while lists are vectors that may have multiple data types.  
**Data types:**  

* Numeric  
* Logical (T, F, NA)    
* Character  
  * Surround character strings with `"`
* Integer   
* Complex   

**Logical operators**   

* `>=`: greater than or equal to    
* `==`: equal to   
* `!=`: not equal to  
* `|`: or  
* `&`: and    

`paste()` is useful for pasting different elements together.  

```r
my_char <- c("My", "name", "is")
paste(my_char, collapse = " ")
```

```
## [1] "My name is"
```

```r
paste("Hello", "world!", sep = " ")
```

```
## [1] "Hello world!"
```

When using `paste()`, R will coerce numbers into characters.   

```r
paste(LETTERS, 1:4, sep = "-")
```

```
##  [1] "A-1" "B-2" "C-3" "D-4" "E-1" "F-2" "G-3" "H-4" "I-1" "J-2" "K-3" "L-4"
## [13] "M-1" "N-2" "O-3" "P-4" "Q-1" "R-2" "S-3" "T-4" "U-1" "V-2" "W-3" "X-4"
## [25] "Y-1" "Z-2"
```

#### 5. Missing Values

Missing values in R are represented as `NA`. Operations involving `NA` will return `NA`.  

```r
# randomly draw from a normal distribution 
y <- rnorm(1000)  
# create a vector of the same size with NAs
z <- rep(NA, 1000)

# randomly select 100 values from these two vectors 
my_data <- sample(c(y, z), 100)
```

Where are the `NA` values located?  

```r
(my_na <- is.na(my_data))
```

```
##   [1]  TRUE  TRUE FALSE  TRUE  TRUE FALSE  TRUE FALSE FALSE  TRUE FALSE FALSE
##  [13]  TRUE FALSE  TRUE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE  TRUE
##  [25]  TRUE  TRUE FALSE FALSE  TRUE FALSE FALSE  TRUE FALSE  TRUE  TRUE FALSE
##  [37]  TRUE  TRUE FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE FALSE
##  [49] FALSE FALSE FALSE FALSE FALSE  TRUE FALSE  TRUE  TRUE  TRUE FALSE FALSE
##  [61] FALSE  TRUE FALSE  TRUE FALSE FALSE FALSE FALSE FALSE  TRUE  TRUE FALSE
##  [73] FALSE FALSE FALSE  TRUE  TRUE  TRUE FALSE FALSE FALSE FALSE  TRUE FALSE
##  [85]  TRUE FALSE FALSE  TRUE FALSE FALSE FALSE  TRUE FALSE  TRUE FALSE  TRUE
##  [97]  TRUE  TRUE FALSE FALSE
```

`NA` is a placeholder, but not a true value. Be careful when working with `NA` in logical expressions because it can pollute the output.  

R counts `TRUE` as `1` and `FALSE` as `0`, so you can sum logical vectors to count the number of `TRUE` elements.  

```r
sum(my_na)
```

```
## [1] 43
```

`NaN` is an indicator for something that is not a number.  

```r
0/0
```

```
## [1] NaN
```

```r
Inf - Inf
```

```
## [1] NaN
```

#### 6. Subsetting Vectors  

Use `[]` to subset a vector.   

```r
x <- sample(c(rnorm(20), rep(NA, 20)))

# subset the first 10 elements of x
x[1:10]
```

```
##  [1]  0.4691343         NA -1.2076483         NA -0.1123363         NA
##  [7]         NA -0.2772630         NA -1.0376248
```

Make sure that you are subsetting for something within your dataset because R will not stop you from asking for an element that doesn't exist.       

```r
x[3000]
```

```
## [1] NA
```

Logical expressions can be used for subsetting.  

```r
# create a vector without NAs
y <- x[!is.na(x)]

# create a vector of positive values 
y[y > 0]
```

```
## [1] 0.4691343 0.4031867 1.8285717 0.7180715 0.6677884 0.8668702 0.1219628
## [8] 0.9679393
```

Multiple expressions can be used for simultaneous subsetting.  

```r
x[!is.na(x) & x > 0]
```

```
## [1] 0.4691343 0.4031867 1.8285717 0.7180715 0.6677884 0.8668702 0.1219628
## [8] 0.9679393
```

When subsetting, remove specific elements with `-`.  

```r
# remove the 2nd and 10th elements 
x[-c(2, 10)]
```

```
##  [1]  0.46913430 -1.20764828          NA -0.11233633          NA          NA
##  [7] -0.27726305          NA          NA -0.71456997          NA          NA
## [13] -1.51143457 -0.03104463          NA -0.62136557          NA          NA
## [19]  0.40318666          NA          NA          NA -0.72680075          NA
## [25]          NA  1.82857169          NA          NA  0.71807154 -1.57307549
## [31]          NA -0.07685980          NA  0.66778836  0.86687022  0.12196278
## [37]  0.96793932 -0.66929724
```

Named vectors have names assigned to the values.   

```r
vect <- c(foo = 11, bar = 2, norf = NA)

# check the names
names(vect)
```

```
## [1] "foo"  "bar"  "norf"
```

Names can also be added later to an existing vector.   

```r
vect2 <- c(11, 2, NA)
names(vect2) <- c("foo", "bar", "norf")

# check that vect and vect2 are the same
identical(vect, vect2)
```

```
## [1] TRUE
```

Names can be used for subsetting as well.  

```r
vect["bar"]
```

```
## bar 
##   2
```

#### 7. Matrices and Data Frames

Matrices contain one class of data, but data frames can contain many classes of data.  

Let's check out the dimensions of an object. When working in R, rows are the first value and columns are the second value.    

```r
my_matrix <- 1:20 
dim(my_matrix) <- c(4, 5)

# dimensions?
dim(my_matrix) 
```

```
## [1] 4 5
```

```r
# length? 
length(my_matrix)
```

```
## [1] 20
```

You can also see this with `attributes()`.   

```r
attributes(my_matrix) 
```

```
## $dim
## [1] 4 5
```

Use `class()` to check the type of an object.  

```r
class(my_matrix)
```

```
## [1] "matrix"
```

The same matrix can be created using `matrix()`.  

```r
my_matrix2 <- matrix(1:20, 4, 5)
```

Columns can be combined with `cbind()`.  

```r
patients <- c("Bill", "Gina", "Kelly", "Sean") 
cbind(patients, my_matrix)
```

```
##      patients                       
## [1,] "Bill"   "1" "5" "9"  "13" "17"
## [2,] "Gina"   "2" "6" "10" "14" "18"
## [3,] "Kelly"  "3" "7" "11" "15" "19"
## [4,] "Sean"   "4" "8" "12" "16" "20"
```

Sometimes R will coerce one data class into another without being asked.  
To combine multiple data classes together, create a data frame.  

```r
my_data <- data.frame(patients, my_matrix)
```

Row names or column names can be assigned to a data frame after it is created.   

```r
# create vector of column names
cnames <- c("patient", "age", "weight", "bp", "rating", "test")

# assign column names 
colnames(my_data) <- cnames
my_data
```

```
##   patient age weight bp rating test
## 1    Bill   1      5  9     13   17
## 2    Gina   2      6 10     14   18
## 3   Kelly   3      7 11     15   19
## 4    Sean   4      8 12     16   20
```

#### 8. Logic

Logical operators    

  * `==` is equal to  
  * `<` is less than  
  * `>` is greater than   
  * `<=` is less than or equal to    
  * `>=` is greater than or equal to    
  * `!=` is not equal to   
  * `&` is "and"   
  * `|` is "or"   
  
To evaluate and statements across an entire vector, use `&`. To evaluate and statements across only the first element of a vector, use `&&`.   

```r
TRUE & c(TRUE, FALSE, FALSE) 
```

```
## [1]  TRUE FALSE FALSE
```

```r
TRUE && c(TRUE, FALSE, FALSE)
```

```
## [1] TRUE
```

Similarly for or statements, use `|` or `||` respectively.   

```r
TRUE | c(TRUE, FALSE, FALSE) 
```

```
## [1] TRUE TRUE TRUE
```

```r
TRUE || c(TRUE, FALSE, FALSE)
```

```
## [1] TRUE
```

#### 12. Looking at Data 

As seen previously, use `dim()` to find the dimensions of a dataset. However, you can also separately check the number of rows or the number of columns using `nrow()` and `ncol()`. 

Check out the first six rows of a dataset with `head()` or look at the last six rows of a dataset with `tail()`.  

```r
head(diamonds)
```

```
## # A tibble: 6 x 10
##   carat cut       color clarity depth table price     x     y     z
##   <dbl> <ord>     <ord> <ord>   <dbl> <dbl> <int> <dbl> <dbl> <dbl>
## 1 0.23  Ideal     E     SI2      61.5    55   326  3.95  3.98  2.43
## 2 0.21  Premium   E     SI1      59.8    61   326  3.89  3.84  2.31
## 3 0.23  Good      E     VS1      56.9    65   327  4.05  4.07  2.31
## 4 0.290 Premium   I     VS2      62.4    58   334  4.2   4.23  2.63
## 5 0.31  Good      J     SI2      63.3    58   335  4.34  4.35  2.75
## 6 0.24  Very Good J     VVS2     62.8    57   336  3.94  3.96  2.48
```

To check out the distribution of data, use `summary()`.  

```r
summary(diamonds)  
```

```
##      carat               cut        color        clarity          depth      
##  Min.   :0.2000   Fair     : 1610   D: 6775   SI1    :13065   Min.   :43.00  
##  1st Qu.:0.4000   Good     : 4906   E: 9797   VS2    :12258   1st Qu.:61.00  
##  Median :0.7000   Very Good:12082   F: 9542   SI2    : 9194   Median :61.80  
##  Mean   :0.7979   Premium  :13791   G:11292   VS1    : 8171   Mean   :61.75  
##  3rd Qu.:1.0400   Ideal    :21551   H: 8304   VVS2   : 5066   3rd Qu.:62.50  
##  Max.   :5.0100                     I: 5422   VVS1   : 3655   Max.   :79.00  
##                                     J: 2808   (Other): 2531                  
##      table           price             x                y         
##  Min.   :43.00   Min.   :  326   Min.   : 0.000   Min.   : 0.000  
##  1st Qu.:56.00   1st Qu.:  950   1st Qu.: 4.710   1st Qu.: 4.720  
##  Median :57.00   Median : 2401   Median : 5.700   Median : 5.710  
##  Mean   :57.46   Mean   : 3933   Mean   : 5.731   Mean   : 5.735  
##  3rd Qu.:59.00   3rd Qu.: 5324   3rd Qu.: 6.540   3rd Qu.: 6.540  
##  Max.   :95.00   Max.   :18823   Max.   :10.740   Max.   :58.900  
##                                                                   
##        z         
##  Min.   : 0.000  
##  1st Qu.: 2.910  
##  Median : 3.530  
##  Mean   : 3.539  
##  3rd Qu.: 4.040  
##  Max.   :31.800  
## 
```

To get an overview of how a dataset is structured, use `str()`.  

```r
str(diamonds)
```

```
## tibble [53,940 x 10] (S3: tbl_df/tbl/data.frame)
##  $ carat  : num [1:53940] 0.23 0.21 0.23 0.29 0.31 0.24 0.24 0.26 0.22 0.23 ...
##  $ cut    : Ord.factor w/ 5 levels "Fair"<"Good"<..: 5 4 2 4 2 3 3 3 1 3 ...
##  $ color  : Ord.factor w/ 7 levels "D"<"E"<"F"<"G"<..: 2 2 2 6 7 7 6 5 2 5 ...
##  $ clarity: Ord.factor w/ 8 levels "I1"<"SI2"<"SI1"<..: 2 3 5 4 2 6 7 3 4 5 ...
##  $ depth  : num [1:53940] 61.5 59.8 56.9 62.4 63.3 62.8 62.3 61.9 65.1 59.4 ...
##  $ table  : num [1:53940] 55 61 65 58 58 57 57 55 61 61 ...
##  $ price  : int [1:53940] 326 326 327 334 335 336 336 337 337 338 ...
##  $ x      : num [1:53940] 3.95 3.89 4.05 4.2 4.34 3.94 3.95 4.07 3.87 4 ...
##  $ y      : num [1:53940] 3.98 3.84 4.07 4.23 4.35 3.96 3.98 4.11 3.78 4.05 ...
##  $ z      : num [1:53940] 2.43 2.31 2.31 2.63 2.75 2.48 2.47 2.53 2.49 2.39 ...
```


[Rundergrad-Github]: https://github.com/ucd-rundergrad-2020
[Kit]: Week1/sleeping_kit.jpg
