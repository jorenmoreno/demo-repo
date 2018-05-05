Study Guide - Final 2
================
Joren Moreno
May 4, 2018

``` r
knitr::opts_chunk$set(echo = TRUE, error = TRUE, comment = "", eval = TRUE)
```

### Rmd files

**Rmd** files are a special type of file, referred to as a *dynamic document*. It combines both the commands and the narrative of R code.

The structure of an `.Rmd` file can be divided in two parts: 1) a **YAML header**, and 2) the **body** of the document.

1.  *YAML header* consists of the first few lines at the top of the file. This header is established by a set of three dashes --- as delimiters (one starting set, and one ending set). This part of the file requires you to use YAML syntax (Yet Another Markup Language.) Within the delimiter sets of dashes, you specify settings (or metadata) that will apply to the entire document. Some of the common options are things like:

-   `title`
-   `author`
-   `date`
-   `output`

1.  The *body* of the document is everything below the YAML header. It consists of a mix of narrative and R code. All the text that is narrative is written in a markup syntax called **Markdown** (although you can also use LaTeX math notation). In turn, all the text that is code is written in R syntax inside *blocks of code.*

-   The header uses YAML syntax
-   The narrative in the body uses Markdown syntax.
-   The code and commands use R syntax.

### Markdown tutorial (heading)

-   *Italics* (italics)
-   **Bold** (bold)
-   Paragraphs:
    -   use two blank spaces at the end of the line or
    -   this is a line break
-   Headings: a hash `#` and a space makes a header. The more `#`, the smaller the header.

> Blockquotes: To create a blockquote, start a line with greater than `>` followed by an optional space. Blockquotes can be nested and can also contain other formatting. end of blockquote

-   Lists:
    -   unordered lists use asteriks `+`, or `-` as list markers
    -   ordered lists use numbers followed by a period `.` or right paren `)`
-   Links:
    -   links can either inline with the text, or placed at the bottom of the text as references. Link text is enclosed by square brackets `[]`, and for inline links, the link URL is enclosed by parens `()`.
-   Images:
    -   images are almost identical to links, but an image starts with an exclamation point `!`.
-   Code:
    -   `code`

    <!-- -->

        or use 3 backticks

-   Nested Lists
    -   Item
        1.  First subitem
        2.  Second subitem

### Data Types in R

-   Integer (whole numbers)
-   Double (real, decimal numbers)
-   Logical (boolean)
-   Character (strings)
-   Numeric (integer/real/double numbers)

### Coercion

If you mix different data values, R will **implicity coerce** them so they are ALL of the same type

``` r
#example 
a <- c(1,2,3,"four","five")
b <- c(TRUE,FALSE,3,4)
```

R provides a set of **explicit** coercion functions that allow you to "convert" one type of data into another:

-   as.character()
-   as.numeric()
-   as.integer()
-   as.logical()

### How does R coerce data types in vectors?

R follows two basic rules of implicit coercion

1.  If a character is present, R will coerce everything else to characters.
2.  If a vector contains logicals and numbers, R will convert the logicals to numbers (TRUE to 1, FALSE to 0)

Here is the general rule: - logical &lt; integer &lt; numeric &lt; complex &lt; character

### Special data values in R

-   `Null` = null object
-   `NA` = Not Available (missing value)
-   `Inf` = positive infinite
-   `-Inf` = negative infinite
-   `NaN` = Not a Number (different from NA)

### Subsetting

#### Numeric subsetting

``` r
x <- c(2,4,6,8)

# first 3 elements
x[1:3]
```

    [1] 2 4 6

``` r
# non-consecutive elements
x[c(1,3)]
```

    [1] 2 6

``` r
# different order
x[c(3,2,4,1)]
```

    [1] 6 4 8 2

**Logical subsetting** occurs when the vector of indices that you pass inside the brackets is a logical vector.

``` r
x <- c(2,4,6,8)
names(x) <- letters[1:4]
      
# first element
x[c(TRUE,FALSE,FALSE,FALSE)]
```

    a 
    2 

``` r
# elements equal to 2
x[x == 2]
```

    a 
    2 

``` r
# elements different to 2
x[x != 2]
```

    b c d 
    4 6 8 

``` r
# all elements
x[TRUE]
```

    a b c d 
    2 4 6 8 

``` r
# convert numbers as logicals 
x[as.logical(c(0,1,pi,-10))]
```

    b c d 
    4 6 8 

**Character subsetting** occurs with characters

``` r
# element names "a"
x["a"]
```

    a 
    2 

``` r
# "b" and "d"
x[c("b","d")]
```

    b d 
    4 8 

``` r
# "a" 5 times
x[rep("a",5)]
```

    a a a a a 
    2 2 2 2 2 

### Indexing

*Bracket notation for vectors*

-   To extract values from R object use brackets: \[\]
-   Inside the brackets specify vector(s) of indices
-   Use as many indices, separated by commas, as dimensions in the object
-   Vector(s) of indices can be *numbers, logicals*, and sometimes *characters*

``` r
# example
list <-  list(
  c(1,2,3),
  matrix(1:9, nrow = 3, ncol = 3),
  list(1:2, c(TRUE,FALSE), c("a","b"))
) 
```

##### access list elements

``` r
# list[elem]

list[1]
```

    [[1]]
    [1] 1 2 3

##### access object of list element

``` r
# list[[elem]]

list[[1]]
```

    [1] 1 2 3

##### access object's elemets, of list element

``` r
# list[[elem]][obj]

list[[1]][2]
```

    [1] 2

``` r
list[[2]][1,1]
```

    [1] 1

``` r
list[[2]][,2]
```

    [1] 4 5 6

##### access object's elements, of list element

``` r
# list[[elem]][[obj]]

list[[3]][[1]]
```

    [1] 1 2

##### access element of object's elements, of list element

``` r
# list[[elem]][[obj]][ind]
  
list[[3]][[1]][1]
```

    [1] 1

``` r
list[[3]][[3]][c(1,2)]
```

    [1] "a" "b"

#### Dollar notation

##### access list named elements

``` r
lst <- list(
  vec = c(1,2,3),
  mat = matrix(1:9, nrow = 3, ncol = 3),
  lis = list(1:2, c(TRUE,FALSE), c("a","b"))
)

lst$vec
```

    [1] 1 2 3

##### access list named elements

``` r
lst$vec[2]
```

    [1] 2

``` r
lst$lis[[1]]
```

    [1] 1 2

### Recycling Rule & Vectorization

#### Recycling Example

``` r
x <- c(2,4,6,7)
x + 3
```

    [1]  5  7  9 10

-   Most functions that operate with vectors in R are vectorized functions. This means that an action is applied to all elements of the vector without the need to explicitly type commands to traverse all the elements.

### Object Names

There are certain rules you have to follow when creating objects and variables. Object names cannot start with a digit and cannot contain certain other characters such as a comma or a space. You will be wise to adopt a convention for demarcating words in names.

### Factors

Vectors, matrices, and arrays are atomic structures (they can only store one type of data)

-   A factor is a data structure designed to handle **categorical data**.
-   Use factor().
-   Factors are **internally stored as vectors of integers**.
-   Factors generally convert strings or characters, (i.e. "yes" to yes)
-   Under the hood, a factor is internally stored using two arrays (R vectors): one is an integer array containing the values of the categories, the other array is the "levels" which has the names of categories which are mapped to the integers.
-   `table()` is a function to get a table with the frequencies (i.e. counts) of the factor categories or *levels*
-   use `as.factor()` to force a vector to have a factor data structure

### Lists

-   A list is the most general data structure in r
-   Lists can contain any other type of data structure
-   Lists can even contain other lists
-   Lists are a special type of vector
-   Lists are vectors in the sense of being a one-dimensional object.
-   Lists are NOT atomic structures.

### Inspecting the data objects

-   `typeof()` type of storage of any object
-   `class()` gives you the class of the object
-   `str()` displays the structure of an object in a compact way
-   `mode()` gives the data type (as used in R)
-   `object.size()` gives an estimate of the memory space used by an object
-   `length()` gives the length (i.e. number of elements)
-   `head()` take a peek at the first elements
-   `tail()` take a peek at the last elements
-   `summary()` shows a summary of a given object

### Main Unix Concepts

-   At any given time we are inside a directory.
-   The current directory is the working directory
-   When a new R session is started, a working directory will be associated to the session.
-   When a terminal is started the working directory is the home directory.

### Paths

-   Each file and directory has a unique name in the filesystem called a path.
-   Absolute Paths: an absolute pathname begins with the root directory and follows the tree branch by branch.
-   Relative Paths: a relative pathname begins at some working directory, moving either up or down the tree.

### Creating files

3 main ways to create files:

-   Using a text editor
-   Direct output (from command) to a file
-   Using the command `touch`

Note: text editor =/ word processor

### Spreadsheet inconveniences

-   Excel files (.xls) are NOT text files
-   They are enriched files with added format elements.
-   Cannot be opened with a text editior.
-   You depend on proprietary software.

### Character Delimited Text

-   A common way to store data in tabular form is via text files.
-   To store the data we need a way to separate data values
-   Each line represents a "row"
-   The idea of columns is conveyed with delimiters.

### Plain Text Formats

-   There are 2 main subtypes of plain text format, depending on how the separated values are identified in a row.

1.  Delimited formats
2.  Fixed-width formats

### Advantages

-   Simplicity
-   Common formats (csv,tsv,txt,dat,etc...)
-   Can be opened and modified with a text editor.
-   Can also be opened in spreadsheet software.
-   Easy to understand for most users.
-   Can be read in data analysis software.

### R data frames

-   R data frames are special kinds of lists
-   Stored in R as a list of vectors (or factors)
-   Columns are typically atomic structures.
-   But since a data frame is a list, you can mix different types of columns.

### dplyr Functions

-   `filter`: filter by some specific value.
-   `select`: select certain columns
-   `slice`: select certain rows
-   `group_by`: group by team
-   `summarise`: summarise info
-   `aggregate`: aggregate info
-   `arrange`: sort by something

### ggplot functions

-   `aes` = aesthetic
-   ggplot() + geom\_point + geom\_text
-   faceting by position

### gitbash commands

-   `wc`: count lines, words, and bytes
-   `wc -l`: count number of lines
-   `head -n 10`: inspect first 10 rows
-   `tail -n 10`: inspect last 10 rows
-   `less`: see contents with a paginator
-   `cut`: select columns
-   `pwd`: print working directory
-   `cd`: change directory (move to another directly)
-   `mv`: rename file(s)
-   `cp`: copy file(s)
-   `touch`: create a new (empty) file
-   `rm`: delete file(s)
-   `mkdir`: create a new directory
-   `ls`: list files and directories
-   `curl -O`: download files
-   `cat`: output the contents of a file
-   `grep`: output all occurrences of "text" inside a file