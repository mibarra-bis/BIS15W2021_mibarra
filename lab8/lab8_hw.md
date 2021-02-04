---
title: "Lab 8 Homework"
author: "Margarita I"
date: "2021-02-04"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
```

## Install `here`
The package `here` is a nice option for keeping directories clear when loading files. I will demonstrate below and let you decide if it is something you want to use.  


## Data
For this homework, we will use a data set compiled by the Office of Environment and Heritage in New South Whales, Australia. It contains the enterococci counts in water samples obtained from Sydney beaches as part of the Beachwatch Water Quality Program. Enterococci are bacteria common in the intestines of mammals; they are rarely present in clean water. So, enterococci values are a measurement of pollution. `cfu` stands for colony forming units and measures the number of viable bacteria in a sample [cfu](https://en.wikipedia.org/wiki/Colony-forming_unit).   

This homework loosely follows the tutorial of [R Ladies Sydney](https://rladiessydney.org/). If you get stuck, check it out!  

1. Start by loading the data `sydneybeaches`. Do some exploratory analysis to get an idea of the data structure.

```r
sydneybeaches <- readr::read_csv("data/sydneybeaches.csv") %>% 
  janitor::clean_names()
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   BeachId = col_double(),
##   Region = col_character(),
##   Council = col_character(),
##   Site = col_character(),
##   Longitude = col_double(),
##   Latitude = col_double(),
##   Date = col_character(),
##   `Enterococci (cfu/100ml)` = col_double()
## )
```

If you want to try `here`, first notice the output when you load the `here` library. It gives you information on the current working directory. You can then use it to easily and intuitively load files.

The quotes show the folder structure from the root directory.

2. Are these data "tidy" per the definitions of the tidyverse? How do you know? Are they in wide or long format?

Some of our columns are variables, so the data is not tidy. They are in long format. 

3. We are only interested in the variables site, date, and enterococci_cfu_100ml. Make a new object focused on these variables only. Name the object `sydneybeaches_long`


```r
sydneybeaches_long <- sydneybeaches %>% 
  select(site, date, enterococci_cfu_100ml)
```


4. Pivot the data such that the dates are column names and each beach only appears once. Name the object `sydneybeaches_wide`


```r
sydneybeaches_wide <- sydneybeaches_long %>% 
  pivot_wider(names_from = "date",
              values_from = "enterococci_cfu_100ml")
sydneybeaches_wide
```

```
## # A tibble: 11 x 345
##    site  `02/01/2013` `06/01/2013` `12/01/2013` `18/01/2013` `30/01/2013`
##    <chr>        <dbl>        <dbl>        <dbl>        <dbl>        <dbl>
##  1 Clov…           19            3            2           13            8
##  2 Coog…           15            4           17           18           22
##  3 Gord…           NA           NA           NA           NA           NA
##  4 Litt…            9            3           72            1           44
##  5 Mala…            2            4          390           15           13
##  6 Maro…            1            1           20            2           11
##  7 Sout…            1            0           33            2           13
##  8 Sout…           12            2          110           13          100
##  9 Bond…            3            1            2            1            6
## 10 Bron…            4            2           38            3           25
## 11 Tama…            1            0            7           22           23
## # … with 339 more variables: `05/02/2013` <dbl>, `11/02/2013` <dbl>,
## #   `23/02/2013` <dbl>, `07/03/2013` <dbl>, `25/03/2013` <dbl>,
## #   `02/04/2013` <dbl>, `12/04/2013` <dbl>, `18/04/2013` <dbl>,
## #   `24/04/2013` <dbl>, `01/05/2013` <dbl>, `20/05/2013` <dbl>,
## #   `31/05/2013` <dbl>, `06/06/2013` <dbl>, `12/06/2013` <dbl>,
## #   `24/06/2013` <dbl>, `06/07/2013` <dbl>, `18/07/2013` <dbl>,
## #   `24/07/2013` <dbl>, `08/08/2013` <dbl>, `22/08/2013` <dbl>,
## #   `29/08/2013` <dbl>, `24/01/2013` <dbl>, `17/02/2013` <dbl>,
## #   `01/03/2013` <dbl>, `13/03/2013` <dbl>, `19/03/2013` <dbl>,
## #   `06/04/2013` <dbl>, `07/05/2013` <dbl>, `14/05/2013` <dbl>,
## #   `25/05/2013` <dbl>, `17/06/2013` <dbl>, `30/06/2013` <dbl>,
## #   `12/07/2013` <dbl>, `30/07/2013` <dbl>, `14/08/2013` <dbl>,
## #   `16/08/2013` <dbl>, `02/09/2013` <dbl>, `28/09/2013` <dbl>,
## #   `04/10/2013` <dbl>, `12/10/2013` <dbl>, `28/10/2013` <dbl>,
## #   `05/11/2013` <dbl>, `29/11/2013` <dbl>, `07/12/2013` <dbl>,
## #   `10/09/2013` <dbl>, `16/09/2013` <dbl>, `22/09/2013` <dbl>,
## #   `20/10/2013` <dbl>, `13/11/2013` <dbl>, `21/11/2013` <dbl>,
## #   `23/12/2013` <dbl>, `13/12/2013` <dbl>, `31/12/2013` <dbl>,
## #   `08/10/2014` <dbl>, `16/10/2014` <dbl>, `25/10/2014` <dbl>,
## #   `02/11/2014` <dbl>, `10/11/2014` <dbl>, `18/11/2014` <dbl>,
## #   `13/12/2014` <dbl>, `19/12/2014` <dbl>, `16/01/2014` <dbl>,
## #   `24/01/2014` <dbl>, `09/02/2014` <dbl>, `25/02/2014` <dbl>,
## #   `05/03/2014` <dbl>, `06/04/2014` <dbl>, `06/05/2014` <dbl>,
## #   `16/05/2014` <dbl>, `22/05/2014` <dbl>, `10/06/2014` <dbl>,
## #   `26/06/2014` <dbl>, `08/07/2014` <dbl>, `14/07/2014` <dbl>,
## #   `24/07/2014` <dbl>, `05/08/2014` <dbl>, `21/08/2014` <dbl>,
## #   `21/10/2014` <dbl>, `26/11/2014` <dbl>, `04/12/2014` <dbl>,
## #   `12/09/2014` <dbl>, `18/09/2014` <dbl>, `24/09/2014` <dbl>,
## #   `28/12/2014` <dbl>, `08/01/2014` <dbl>, `01/02/2014` <dbl>,
## #   `17/02/2014` <dbl>, `13/03/2014` <dbl>, `21/03/2014` <dbl>,
## #   `29/03/2014` <dbl>, `22/04/2014` <dbl>, `14/04/2014` <dbl>,
## #   `30/04/2014` <dbl>, `12/05/2014` <dbl>, `28/05/2014` <dbl>,
## #   `03/06/2014` <dbl>, `19/06/2014` <dbl>, `03/07/2014` <dbl>,
## #   `18/07/2014` <dbl>, `01/08/2014` <dbl>, …
```


5. Pivot the data back so that the dates are data and not column names.


```r
sydneybeaches_wide %>% 
  pivot_longer(-site,
               names_to = "date",
               values_to = "enterococci_cfu_100ml")
```

```
## # A tibble: 3,784 x 3
##    site           date       enterococci_cfu_100ml
##    <chr>          <chr>                      <dbl>
##  1 Clovelly Beach 02/01/2013                    19
##  2 Clovelly Beach 06/01/2013                     3
##  3 Clovelly Beach 12/01/2013                     2
##  4 Clovelly Beach 18/01/2013                    13
##  5 Clovelly Beach 30/01/2013                     8
##  6 Clovelly Beach 05/02/2013                     7
##  7 Clovelly Beach 11/02/2013                    11
##  8 Clovelly Beach 23/02/2013                    97
##  9 Clovelly Beach 07/03/2013                     3
## 10 Clovelly Beach 25/03/2013                     0
## # … with 3,774 more rows
```

6. We haven't dealt much with dates yet, but separate the date into columns day, month, and year. Do this on the `sydneybeaches_long` data.


```r
sydneybeaches_long2 <- sydneybeaches_long %>% 
  separate(date, into = c("day", "month", "year"), sep = "/")
```


7. What is the average `enterococci_cfu_100ml` by year for each beach. Think about which data you will use- long or wide.


```r
sydneybeaches_avg <- sydneybeaches_long2 %>% 
  group_by(year, site) %>% 
  summarise(enterococci_mean = mean(enterococci_cfu_100ml, na.rm = T), .groups = "keep")
sydneybeaches_avg
```

```
## # A tibble: 66 x 3
## # Groups:   year, site [66]
##    year  site                    enterococci_mean
##    <chr> <chr>                              <dbl>
##  1 2013  Bondi Beach                        32.2 
##  2 2013  Bronte Beach                       26.8 
##  3 2013  Clovelly Beach                      9.28
##  4 2013  Coogee Beach                       39.7 
##  5 2013  Gordons Bay (East)                 24.8 
##  6 2013  Little Bay Beach                  122.  
##  7 2013  Malabar Beach                     101.  
##  8 2013  Maroubra Beach                     47.1 
##  9 2013  South Maroubra Beach               39.3 
## 10 2013  South Maroubra Rockpool            96.4 
## # … with 56 more rows
```


8. Make the output from question 7 easier to read by pivoting it to wide format.


```r
sydneybeaches_avg_wide <- sydneybeaches_avg %>% 
  pivot_wider(names_from = "year",
              values_from = enterococci_mean)
```


9. What was the most polluted beach in 2018?

```r
sydneybeaches_avg_wide %>% 
  select(site, "2018") %>% 
  arrange(desc(.))
```

```
## # A tibble: 11 x 2
## # Groups:   site [11]
##    site                    `2018`
##    <chr>                    <dbl>
##  1 Tamarama Beach           15.5 
##  2 South Maroubra Rockpool 112.  
##  3 South Maroubra Beach     12.5 
##  4 Maroubra Beach            9.21
##  5 Malabar Beach            38.0 
##  6 Little Bay Beach         59.1 
##  7 Gordons Bay (East)       17.6 
##  8 Coogee Beach             21.6 
##  9 Clovelly Beach           10.6 
## 10 Bronte Beach             43.4 
## 11 Bondi Beach              22.9
```

South Maroubra Rockpool Beach was the most polluted in 2018.

10. Please complete the class project survey at: [BIS 15L Group Project](https://forms.gle/H2j69Z3ZtbLH3efW6)


## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   