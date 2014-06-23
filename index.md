---
title       : Text String Distance Explorer
subtitle    : A utility for comparing the number of required tranformations to match text strings
author      : Peter Davis 
job         : Coursera Developing Data products
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : []            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
---

## Text String Distance Explorer
This project is to allow us to interactively explore how different two text strings are by measuring their "distance."

String distance is a measure of the number of operations that it will take to transform one string to another. It is a way to compare of how far apart two strings are from each other as measured by operations.   

For example, if we wanted to transform "James" into "Janine" we might do the following steps:
- James
- Janes
- Janis
- Janin
- Janine

So we have changed 3 letters and added another letter for a total of 4 operations.  This transformation give us one measure of how closely James and Janine are related.


--- .class #id 

## Why explore string distances?

There are several motivators for looking at string distances:
- To better understand how string comparisons work.
- To explore a variety of algorithms and their outputs.
- To improve deduplication alorithms.

This project is motivated by improvements to existing deduplication algorithms that I have seen on Customer Relationship Management Systems.  They typically utilize a very simplistic model for finding duplicates. 

As an initial pass we used adist to give relative scores on comparisons of data.  


---
## Primary Algorithm

For this first build of the application, we are using the adist algorithm. The two primary parameters of adist are the strings to compare, other parameters are optional.

An example of the algorithm in action:


```r
adist("James", "Janine", partial = FALSE)
```

```
##      [,1]
## [1,]    4
```


The counts for each operation (insert, delete and substution) are:

```r
drop(attr(adist("James", "Janine", counts = TRUE), "counts"))
```

```
## ins del sub 
##   1   0   3
```




---
## Exploration Interface

The initial interface for the application is quite simple.  

One may enter a starting text string and an ending text string in the left hand panel.

Distances are calculated in real time and are shown to the right of the input area.  

The number of substitutions, deletions and modifications are shown to the end user.  

There are a number of improvements to be made to the simplified interface:
- Tabbed output for additional algorithms
- Better layouts
- Additional widgets for turning on/off counts or other elements
- Improved HTML output



---
## Future use and development

As development continues, I would like to add in additional algorithms and functionality for comparison.

For instance, the SQL Server SOUNDEX algorithm is good for checking non numeric strings.  For non numerics it would be interesting to directly compare this against the success of the adist implementation.

I would also add in more sophisticated handling of input strings.  E.g. an option to remove spaces to make strings more compact as well as breaking leading numerics off into their own comparison string.  This would result in better handling of address comparisons.  



