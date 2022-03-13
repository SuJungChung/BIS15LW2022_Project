---
title: "bis15L_final.project"
output: 
  html_document: 
    keep_md: yes
---



## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


```r
summary(cars)
```

```
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
```

## Including Plots

You can also embed plots, for example:

![](Untitled_files/figure-html/pressure-1.png)<!-- -->

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.

```r
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
```

```
## ✓ ggplot2 3.3.5     ✓ purrr   0.3.4
## ✓ tibble  3.1.6     ✓ dplyr   1.0.8
## ✓ tidyr   1.1.4     ✓ stringr 1.4.0
## ✓ readr   2.1.1     ✓ forcats 0.5.1
```

```
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(here)
```

```
## here() starts at /Users/julia/Documents/GitHub/BIS15W2022_jcook
```

```r
library(janitor)
```

```
## 
## Attaching package: 'janitor'
```

```
## The following objects are masked from 'package:stats':
## 
##     chisq.test, fisher.test
```

```r
library(lubridate)
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```


```r
nanno_1<-readr::read_csv("ph_nanno_1.csv")
```

```
## New names:
## * ph_7.6 -> ph_7.6...2
## * ph_8.2 -> ph_8.2...3
## * ph_7.6 -> ph_7.6...4
## * ph_8.2 -> ph_8.2...5
## * ph_8.2 -> ph_8.2...6
## * ...
```

```
## Warning: One or more parsing issues, see `problems()` for details
```

```
## Rows: 28787 Columns: 8
```

```
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (7): relative_time, ph_7.6...2, ph_8.2...3, ph_7.6...4, ph_8.2...5, ph_8...
## lgl (1): ...8
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
nanno_2<-readr::read_csv("ph_nanno_2.csv")
```

```
## New names:
## * ph_7.6 -> ph_7.6...2
## * ph_7.6 -> ph_7.6...3
## * ph_8.2 -> ph_8.2...4
## * ph_7.6 -> ph_7.6...5
## * ph_8.2 -> ph_8.2...6
## * ...
```

```
## Warning: One or more parsing issues, see `problems()` for details
```

```
## Rows: 28787 Columns: 8
```

```
## ── Column specification ────────────────────────────────────────────────────────
## Delimiter: ","
## dbl (7): relative_time, ph_7.6...2, ph_7.6...3, ph_8.2...4, ph_7.6...5, ph_8...
## lgl (1): ...8
## 
## ℹ Use `spec()` to retrieve the full column specification for this data.
## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

```r
nanno_1<-clean_names(nanno_1)
```


```r
glimpse(nanno_1)
```

```
## Rows: 28,787
## Columns: 8
## $ relative_time <dbl> 0.00000, 59.99988, 119.99976, 179.99964, 239.99952, 299.…
## $ ph_7_6_2      <dbl> 7.416141, 7.430027, 7.432163, 7.433231, 7.434299, 7.4353…
## $ ph_8_2_3      <dbl> 8.012955, 8.027909, 8.028977, 8.030045, 8.031113, 8.0311…
## $ ph_7_6_4      <dbl> 7.424657, 7.438542, 7.437474, 7.435338, 7.432134, 7.4310…
## $ ph_8_2_5      <dbl> 7.871005, 7.881686, 7.880618, 7.878481, 7.878481, 7.8774…
## $ ph_8_2_6      <dbl> 8.104071, 8.117957, 8.116888, 8.116888, 8.116888, 8.1158…
## $ ph_7_6_7      <dbl> 7.213557, 7.222102, 7.218898, 7.215693, 7.212489, 7.2103…
## $ x8            <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
```

```r
nanno_1%>%
  select(-c(x8))
```

```
## # A tibble: 28,787 × 7
##    relative_time ph_7_6_2 ph_8_2_3 ph_7_6_4 ph_8_2_5 ph_8_2_6 ph_7_6_7
##            <dbl>    <dbl>    <dbl>    <dbl>    <dbl>    <dbl>    <dbl>
##  1           0       7.42     8.01     7.42     7.87     8.10     7.21
##  2          60.0     7.43     8.03     7.44     7.88     8.12     7.22
##  3         120.      7.43     8.03     7.44     7.88     8.12     7.22
##  4         180.      7.43     8.03     7.44     7.88     8.12     7.22
##  5         240.      7.43     8.03     7.43     7.88     8.12     7.21
##  6         300.      7.44     8.03     7.43     7.88     8.12     7.21
##  7         360.      7.44     8.03     7.43     7.88     8.12     7.21
##  8         420.      7.44     8.03     7.43     7.88     8.11     7.21
##  9         480.      7.44     8.03     7.43     7.88     8.11     7.20
## 10         540.      7.44     8.01     7.43     7.87     8.11     7.20
## # … with 28,777 more rows
```

```r
nanno_1<-nanno_1 %>% 
rename(ph1_7_6 = ph_7_6_2,
       ph1_8_2 = ph_8_2_3,
       ph2_7_6 = ph_7_6_4,
       ph2_8_2 = ph_8_2_5,
       ph3_8_2 = ph_8_2_6, 
       ph3_7_6 = ph_7_6_7)
```

```r
nanno_1
```

```
## # A tibble: 28,787 × 8
##    relative_time ph1_7_6 ph1_8_2 ph2_7_6 ph2_8_2 ph3_8_2 ph3_7_6 x8   
##            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl> <lgl>
##  1           0      7.42    8.01    7.42    7.87    8.10    7.21 NA   
##  2          60.0    7.43    8.03    7.44    7.88    8.12    7.22 NA   
##  3         120.     7.43    8.03    7.44    7.88    8.12    7.22 NA   
##  4         180.     7.43    8.03    7.44    7.88    8.12    7.22 NA   
##  5         240.     7.43    8.03    7.43    7.88    8.12    7.21 NA   
##  6         300.     7.44    8.03    7.43    7.88    8.12    7.21 NA   
##  7         360.     7.44    8.03    7.43    7.88    8.12    7.21 NA   
##  8         420.     7.44    8.03    7.43    7.88    8.11    7.21 NA   
##  9         480.     7.44    8.03    7.43    7.88    8.11    7.20 NA   
## 10         540.     7.44    8.01    7.43    7.87    8.11    7.20 NA   
## # … with 28,777 more rows
```

```r
glimpse(nanno_1)
```

```
## Rows: 28,787
## Columns: 8
## $ relative_time <dbl> 0.00000, 59.99988, 119.99976, 179.99964, 239.99952, 299.…
## $ ph1_7_6       <dbl> 7.416141, 7.430027, 7.432163, 7.433231, 7.434299, 7.4353…
## $ ph1_8_2       <dbl> 8.012955, 8.027909, 8.028977, 8.030045, 8.031113, 8.0311…
## $ ph2_7_6       <dbl> 7.424657, 7.438542, 7.437474, 7.435338, 7.432134, 7.4310…
## $ ph2_8_2       <dbl> 7.871005, 7.881686, 7.880618, 7.878481, 7.878481, 7.8774…
## $ ph3_8_2       <dbl> 8.104071, 8.117957, 8.116888, 8.116888, 8.116888, 8.1158…
## $ ph3_7_6       <dbl> 7.213557, 7.222102, 7.218898, 7.215693, 7.212489, 7.2103…
## $ x8            <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, …
```


```r
nanno_1
```

```
## # A tibble: 28,787 × 8
##    relative_time ph1_7_6 ph1_8_2 ph2_7_6 ph2_8_2 ph3_8_2 ph3_7_6 x8   
##            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl> <lgl>
##  1           0      7.42    8.01    7.42    7.87    8.10    7.21 NA   
##  2          60.0    7.43    8.03    7.44    7.88    8.12    7.22 NA   
##  3         120.     7.43    8.03    7.44    7.88    8.12    7.22 NA   
##  4         180.     7.43    8.03    7.44    7.88    8.12    7.22 NA   
##  5         240.     7.43    8.03    7.43    7.88    8.12    7.21 NA   
##  6         300.     7.44    8.03    7.43    7.88    8.12    7.21 NA   
##  7         360.     7.44    8.03    7.43    7.88    8.12    7.21 NA   
##  8         420.     7.44    8.03    7.43    7.88    8.11    7.21 NA   
##  9         480.     7.44    8.03    7.43    7.88    8.11    7.20 NA   
## 10         540.     7.44    8.01    7.43    7.87    8.11    7.20 NA   
## # … with 28,777 more rows
```
`

```r
nanno_1<-nanno_1[,c(1,2,4,7,3,5,6)]
```

```r
nanno_1
```

```
## # A tibble: 28,787 × 7
##    relative_time ph1_7_6 ph2_7_6 ph3_7_6 ph1_8_2 ph2_8_2 ph3_8_2
##            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1           0      7.42    7.42    7.21    8.01    7.87    8.10
##  2          60.0    7.43    7.44    7.22    8.03    7.88    8.12
##  3         120.     7.43    7.44    7.22    8.03    7.88    8.12
##  4         180.     7.43    7.44    7.22    8.03    7.88    8.12
##  5         240.     7.43    7.43    7.21    8.03    7.88    8.12
##  6         300.     7.44    7.43    7.21    8.03    7.88    8.12
##  7         360.     7.44    7.43    7.21    8.03    7.88    8.12
##  8         420.     7.44    7.43    7.21    8.03    7.88    8.11
##  9         480.     7.44    7.43    7.20    8.03    7.88    8.11
## 10         540.     7.44    7.43    7.20    8.01    7.87    8.11
## # … with 28,777 more rows
```

```r
nanno_1_long<- nanno_1 %>% 
  pivot_longer( 
    ph1_7_6:ph3_8_2,
    names_to = c("ph_set"),
    values_to = "ph_values")
nanno_1_long
```

```
## # A tibble: 172,722 × 3
##    relative_time ph_set  ph_values
##            <dbl> <chr>       <dbl>
##  1           0   ph1_7_6      7.42
##  2           0   ph2_7_6      7.42
##  3           0   ph3_7_6      7.21
##  4           0   ph1_8_2      8.01
##  5           0   ph2_8_2      7.87
##  6           0   ph3_8_2      8.10
##  7          60.0 ph1_7_6      7.43
##  8          60.0 ph2_7_6      7.44
##  9          60.0 ph3_7_6      7.22
## 10          60.0 ph1_8_2      8.03
## # … with 172,712 more rows
```

```r
nanno_1_long %>% 
  ggplot(aes(x=relative_time,y=ph_values,color=ph_set))+
  geom_point()+
  geom_line()+
  facet_grid()+
  labs(x="Time",y="pH")
```

![](Untitled_files/figure-html/unnamed-chunk-14-1.png)<!-- -->



```r
nanno_2
```

```
## # A tibble: 28,787 × 8
##    relative_time ph_7.6...2 ph_7.6...3 ph_8.2...4 ph_7.6...5 ph_8.2...6
##            <dbl>      <dbl>      <dbl>      <dbl>      <dbl>      <dbl>
##  1           0         6.10       6.23       7.82       6.24       7.95
##  2          60.0       6.11       6.24       7.84       6.25       7.98
##  3         120.        6.12       6.25       7.84       6.26       7.97
##  4         180.        6.13       6.25       7.84       6.26       7.97
##  5         240.        6.13       6.26       7.84       6.26       7.97
##  6         300.        6.14       6.26       7.84       6.26       7.97
##  7         360.        6.15       6.26       7.84       6.27       7.97
##  8         420.        6.15       6.27       7.84       6.27       7.97
##  9         480.        6.16       6.27       7.84       6.27       7.97
## 10         540.        6.16       6.28       7.84       6.27       7.97
## # … with 28,777 more rows, and 2 more variables: ph_8.2...7 <dbl>, ...8 <lgl>
```

```r
nanno_2<-clean_names(nanno_2)
```

```r
nanno_2<-nanno_2 %>% 
rename(ph1_7_6 = ph_7_6_2,
       ph1_8_2 = ph_8_2_4,
       ph2_7_6 = ph_7_6_3,
       ph2_8_2 = ph_8_2_6,
       ph3_8_2 = ph_8_2_7, 
       ph3_7_6 = ph_7_6_5)
```

```r
nanno_2
```

```
## # A tibble: 28,787 × 8
##    relative_time ph1_7_6 ph2_7_6 ph1_8_2 ph3_7_6 ph2_8_2 ph3_8_2 x8   
##            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl> <lgl>
##  1           0      6.10    6.23    7.82    6.24    7.95    7.84 NA   
##  2          60.0    6.11    6.24    7.84    6.25    7.98    7.86 NA   
##  3         120.     6.12    6.25    7.84    6.26    7.97    7.86 NA   
##  4         180.     6.13    6.25    7.84    6.26    7.97    7.86 NA   
##  5         240.     6.13    6.26    7.84    6.26    7.97    7.86 NA   
##  6         300.     6.14    6.26    7.84    6.26    7.97    7.86 NA   
##  7         360.     6.15    6.26    7.84    6.27    7.97    7.86 NA   
##  8         420.     6.15    6.27    7.84    6.27    7.97    7.86 NA   
##  9         480.     6.16    6.27    7.84    6.27    7.97    7.86 NA   
## 10         540.     6.16    6.28    7.84    6.27    7.97    7.86 NA   
## # … with 28,777 more rows
```

```r
nanno_2 %>% 
  select(-c(x8))
```

```
## # A tibble: 28,787 × 7
##    relative_time ph1_7_6 ph2_7_6 ph1_8_2 ph3_7_6 ph2_8_2 ph3_8_2
##            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1           0      6.10    6.23    7.82    6.24    7.95    7.84
##  2          60.0    6.11    6.24    7.84    6.25    7.98    7.86
##  3         120.     6.12    6.25    7.84    6.26    7.97    7.86
##  4         180.     6.13    6.25    7.84    6.26    7.97    7.86
##  5         240.     6.13    6.26    7.84    6.26    7.97    7.86
##  6         300.     6.14    6.26    7.84    6.26    7.97    7.86
##  7         360.     6.15    6.26    7.84    6.27    7.97    7.86
##  8         420.     6.15    6.27    7.84    6.27    7.97    7.86
##  9         480.     6.16    6.27    7.84    6.27    7.97    7.86
## 10         540.     6.16    6.28    7.84    6.27    7.97    7.86
## # … with 28,777 more rows
```

```r
nanno_2<-nanno_2[,c(1,2,3,5,4,6,7)]
```

```r
nanno_2
```

```
## # A tibble: 28,787 × 7
##    relative_time ph1_7_6 ph2_7_6 ph3_7_6 ph1_8_2 ph2_8_2 ph3_8_2
##            <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>   <dbl>
##  1           0      6.10    6.23    6.24    7.82    7.95    7.84
##  2          60.0    6.11    6.24    6.25    7.84    7.98    7.86
##  3         120.     6.12    6.25    6.26    7.84    7.97    7.86
##  4         180.     6.13    6.25    6.26    7.84    7.97    7.86
##  5         240.     6.13    6.26    6.26    7.84    7.97    7.86
##  6         300.     6.14    6.26    6.26    7.84    7.97    7.86
##  7         360.     6.15    6.26    6.27    7.84    7.97    7.86
##  8         420.     6.15    6.27    6.27    7.84    7.97    7.86
##  9         480.     6.16    6.27    6.27    7.84    7.97    7.86
## 10         540.     6.16    6.28    6.27    7.84    7.97    7.86
## # … with 28,777 more rows
```

```r
nanno_2_long<-nanno_2 %>% 
  pivot_longer( 
    ph1_7_6:ph3_8_2,
    names_to = c("ph_set"),
    values_to = "ph_values")
nanno_2_long
```

```
## # A tibble: 172,722 × 3
##    relative_time ph_set  ph_values
##            <dbl> <chr>       <dbl>
##  1           0   ph1_7_6      6.10
##  2           0   ph2_7_6      6.23
##  3           0   ph3_7_6      6.24
##  4           0   ph1_8_2      7.82
##  5           0   ph2_8_2      7.95
##  6           0   ph3_8_2      7.84
##  7          60.0 ph1_7_6      6.11
##  8          60.0 ph2_7_6      6.24
##  9          60.0 ph3_7_6      6.25
## 10          60.0 ph1_8_2      7.84
## # … with 172,712 more rows
```

```r
nanno_2_long %>% 
  ggplot(aes(x=relative_time,y=ph_values,color=ph_set))+
  geom_point()+
  geom_line()+
  facet_grid()+
  labs(x="Time",y="pH")
```

```
## Warning: Removed 17880 rows containing missing values (geom_point).
```

```
## Warning: Removed 17880 row(s) containing missing values (geom_path).
```

![](Untitled_files/figure-html/unnamed-chunk-23-1.png)<!-- -->





