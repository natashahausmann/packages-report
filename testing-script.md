---
title: "Untitled"
output:
   html_document:
       keep_md: yes
---


```r
# dplyr::na_if(x, y) replaces NA values in `x` with `y`
# it works when x is a data.frame _without_ Date objects, but fails when there is a Date in the df
# Can you use our debugging tools to figure out where and why it is failing?
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
test <- tibble(a = lubridate::today() + runif(5) * 30,
               b = c(1:4, ""), 
               c = c(runif(4), ""), 
               d = c(sample(letters, 4, replace = TRUE), ""))
test
```

```
## # A tibble: 5 x 4
##   a          b     c                 d    
##   <date>     <chr> <chr>             <chr>
## 1 2020-02-14 1     0.393750611692667 s    
## 2 2020-02-25 2     0.610832777805626 b    
## 3 2020-01-29 3     0.213927449425682 m    
## 4 2020-02-17 4     0.818773220526055 s    
## 5 2020-02-14 ""    ""                ""
```

```r
# test <-  na_if(test, "")

test <- test %>%
  mutate_if(is.character, ~na_if( ., "") )


# The traceback is easier to understand without the pipe involved

# Also useful to look at the implementation of `na_if()`
# Can you reproduce the error without using `na_if()`?

# What happens if you remove the date column from the tibble?
# How could you apply na_if only to non-date columns?
```


---
title: "testing-script.R"
author: "natasha.hausmann"
date: "2020-01-27"
---
