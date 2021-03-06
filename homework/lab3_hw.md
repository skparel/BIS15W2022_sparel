---
title: "Lab 3 Homework"
author: "Sidney Parel"
date: "2022-01-10"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---

## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the tidyverse

```r
library(tidyverse)
```

## Mammals Sleep
1. For this assignment, we are going to use built-in data on mammal sleep patterns. From which publication are these data taken from? Since the data are built-in you can use the help function in R.

The built-in data on mammal sleep patterns is taken from V. M. Savage and G. B. West. A quantitative, theoretical framework for understanding mammalian sleep. Proceedings of the National Academy of Sciences, 104 (3):1051-1056, 2007.

```r
help(msleep)
```

```
## starting httpd help server ... done
```

2. Store these data into a new data frame `sleep`.

```r
sleep <- msleep
```

3. What are the dimensions of this data frame (variables and observations)? How do you know? Please show the *code* that you used to determine this below. 

This data frame has 83 observations and 11 variables.

```r
sleep %>% dim()
```

```
## [1] 83 11
```

4. Are there any NAs in the data? How did you determine this? Please show your code.  

The data contains 136 NAs.

```r
sleep %>% is.na() %>% sum()
```

```
## [1] 136
```

5. Show a list of the column names is this data frame.

```r
sleep %>% names()
```

```
##  [1] "name"         "genus"        "vore"         "order"        "conservation"
##  [6] "sleep_total"  "sleep_rem"    "sleep_cycle"  "awake"        "brainwt"     
## [11] "bodywt"
```

6. How many herbivores are represented in the data?  

32 herbivores are represented in the data.

```r
sleep %>% filter(vore == "herbi") %>% nrow()
```

```
## [1] 32
```

7. We are interested in two groups; small and large mammals. Let's define small as less than or equal to 1kg body weight and large as greater than or equal to 200kg body weight. Make two new dataframes (large and small) based on these parameters.

```r
small_m <- sleep %>% subset(bodywt <= 1)
large_m <- sleep %>% subset(bodywt >= 200)
```

8. What is the mean weight for both the small and large mammals?

The mean weight for small mammals is 0.2596667.

```r
small_m$bodywt %>% mean()
```

```
## [1] 0.2596667
```

The mean weight for large mammals is 1747.071

```r
large_m$bodywt %>% mean()
```

```
## [1] 1747.071
```

9. Using a similar approach as above, do large or small animals sleep longer on average?  

Small animals sleep longer on average than large animals.

```r
small_m$sleep_total %>% mean() > large_m$sleep_total %>% mean()
```

```
## [1] TRUE
```

10. Which animal is the sleepiest among the entire dataframe?

The little brown bat is the sleepiest among the entire dataframe.

```r
sleep %>% arrange(desc(sleep_total)) %>% head(1)
```

```
## # A tibble: 1 x 11
##   name  genus vore  order conservation sleep_total sleep_rem sleep_cycle awake
##   <chr> <chr> <chr> <chr> <chr>              <dbl>     <dbl>       <dbl> <dbl>
## 1 Litt~ Myot~ inse~ Chir~ <NA>                19.9         2         0.2   4.1
## # ... with 2 more variables: brainwt <dbl>, bodywt <dbl>
```


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
