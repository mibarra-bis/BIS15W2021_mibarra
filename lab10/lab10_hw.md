---
title: "Lab 10 Homework"
author: "Margarita I"
date: "2021-02-14"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Load the libraries

```r
library(tidyverse)
library(janitor)
library(here)
library(naniar)
```

## Desert Ecology
For this assignment, we are going to use a modified data set on [desert ecology](http://esapubs.org/archive/ecol/E090/118/). The data are from: S. K. Morgan Ernest, Thomas J. Valone, and James H. Brown. 2009. Long-term monitoring and experimental manipulation of a Chihuahuan Desert ecosystem near Portal, Arizona, USA. Ecology 90:1708.

```r
deserts <- read_csv(here("lab10", "data", "surveys_complete.csv"))
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   record_id = col_double(),
##   month = col_double(),
##   day = col_double(),
##   year = col_double(),
##   plot_id = col_double(),
##   species_id = col_character(),
##   sex = col_character(),
##   hindfoot_length = col_double(),
##   weight = col_double(),
##   genus = col_character(),
##   species = col_character(),
##   taxa = col_character(),
##   plot_type = col_character()
## )
```

1. Use the function(s) of your choice to get an idea of its structure, including how NA's are treated. Are the data tidy?  


```r
glimpse(deserts)
```

```
## Rows: 34,786
## Columns: 13
## $ record_id       <dbl> 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, ...
## $ month           <dbl> 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, 7, ...
## $ day             <dbl> 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16,...
## $ year            <dbl> 1977, 1977, 1977, 1977, 1977, 1977, 1977, 1977, 197...
## $ plot_id         <dbl> 2, 3, 2, 7, 3, 1, 2, 1, 1, 6, 5, 7, 3, 8, 6, 4, 3, ...
## $ species_id      <chr> "NL", "NL", "DM", "DM", "DM", "PF", "PE", "DM", "DM...
## $ sex             <chr> "M", "M", "F", "M", "M", "M", "F", "M", "F", "F", "...
## $ hindfoot_length <dbl> 32, 33, 37, 36, 35, 14, NA, 37, 34, 20, 53, 38, 35,...
## $ weight          <dbl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,...
## $ genus           <chr> "Neotoma", "Neotoma", "Dipodomys", "Dipodomys", "Di...
## $ species         <chr> "albigula", "albigula", "merriami", "merriami", "me...
## $ taxa            <chr> "Rodent", "Rodent", "Rodent", "Rodent", "Rodent", "...
## $ plot_type       <chr> "Control", "Long-term Krat Exclosure", "Control", "...
```



```r
summary(deserts)
```

```
##    record_id         month             day            year         plot_id     
##  Min.   :    1   Min.   : 1.000   Min.   : 1.0   Min.   :1977   Min.   : 1.00  
##  1st Qu.: 8964   1st Qu.: 4.000   1st Qu.: 9.0   1st Qu.:1984   1st Qu.: 5.00  
##  Median :17762   Median : 6.000   Median :16.0   Median :1990   Median :11.00  
##  Mean   :17804   Mean   : 6.474   Mean   :16.1   Mean   :1990   Mean   :11.34  
##  3rd Qu.:26655   3rd Qu.:10.000   3rd Qu.:23.0   3rd Qu.:1997   3rd Qu.:17.00  
##  Max.   :35548   Max.   :12.000   Max.   :31.0   Max.   :2002   Max.   :24.00  
##                                                                                
##   species_id            sex            hindfoot_length     weight      
##  Length:34786       Length:34786       Min.   : 2.00   Min.   :  4.00  
##  Class :character   Class :character   1st Qu.:21.00   1st Qu.: 20.00  
##  Mode  :character   Mode  :character   Median :32.00   Median : 37.00  
##                                        Mean   :29.29   Mean   : 42.67  
##                                        3rd Qu.:36.00   3rd Qu.: 48.00  
##                                        Max.   :70.00   Max.   :280.00  
##                                        NA's   :3348    NA's   :2503    
##     genus             species              taxa            plot_type        
##  Length:34786       Length:34786       Length:34786       Length:34786      
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
## 
```


```r
naniar::miss_var_summary(deserts)
```

```
## # A tibble: 13 x 3
##    variable        n_miss pct_miss
##    <chr>            <int>    <dbl>
##  1 hindfoot_length   3348     9.62
##  2 weight            2503     7.20
##  3 sex               1748     5.03
##  4 record_id            0     0   
##  5 month                0     0   
##  6 day                  0     0   
##  7 year                 0     0   
##  8 plot_id              0     0   
##  9 species_id           0     0   
## 10 genus                0     0   
## 11 species              0     0   
## 12 taxa                 0     0   
## 13 plot_type            0     0
```

2. How many genera and species are represented in the data? What are the total number of observations? Which species is most/ least frequently sampled in the study?


There are 26 genera and 40 species represented in the data. There were a total of 34786 observations. Merriami is the most frequently sampled while clarki, scutalatus, tereticaudus, tigris, uniparens,and viridis were the least frequently sampled. 


```r
deserts %>% 
  summarize(n_genera = n_distinct(genus))
```

```
## # A tibble: 1 x 1
##   n_genera
##      <int>
## 1       26
```

```r
deserts %>% 
  summarize(n_genera = n_distinct(species))
```

```
## # A tibble: 1 x 1
##   n_genera
##      <int>
## 1       40
```


```r
deserts %>% 
  count()
```

```
## # A tibble: 1 x 1
##       n
##   <int>
## 1 34786
```


```r
deserts %>% 
  count(species) %>% 
  arrange(desc(n))
```

```
## # A tibble: 40 x 2
##    species          n
##    <chr>        <int>
##  1 merriami     10596
##  2 penicillatus  3123
##  3 ordii         3027
##  4 baileyi       2891
##  5 megalotis     2609
##  6 spectabilis   2504
##  7 torridus      2249
##  8 flavus        1597
##  9 eremicus      1299
## 10 albigula      1252
## # ... with 30 more rows
```

```r
deserts %>% 
  count(species) %>% 
  arrange(n)
```

```
## # A tibble: 40 x 2
##    species          n
##    <chr>        <int>
##  1 clarki           1
##  2 scutalatus       1
##  3 tereticaudus     1
##  4 tigris           1
##  5 uniparens        1
##  6 viridis          1
##  7 leucophrys       2
##  8 savannarum       2
##  9 fuscus           5
## 10 undulatus        5
## # ... with 30 more rows
```




3. What is the proportion of taxa included in this study? Show a table and plot that reflects this count.


```r
deserts %>%
  count(taxa)
```

```
## # A tibble: 4 x 2
##   taxa        n
## * <chr>   <int>
## 1 Bird      450
## 2 Rabbit     75
## 3 Reptile    14
## 4 Rodent  34247
```


```r
deserts %>% 
  filter(taxa != "NA") %>% 
  ggplot(aes(x = taxa))+
  geom_bar()+
  scale_y_log10()+
  coord_flip()+
  labs(title = "Taxa of the Chihuahan Desert", x = "Taxa", y = "Count")
```

![](lab10_hw_files/figure-html/unnamed-chunk-12-1.png)<!-- -->


4. For the taxa included in the study, use the fill option to show the proportion of individuals sampled by `plot_type.`

```r
deserts %>% 
  filter(taxa != "NA") %>% 
  ggplot(aes(x = taxa, fill = plot_type))+
  geom_bar()+
  scale_y_log10()+
  coord_flip()+
  labs(title = "Plot Type Proportions Among Chihuahuan Desert Taxa", x = "Taxa", y = "Count")
```

![](lab10_hw_files/figure-html/unnamed-chunk-13-1.png)<!-- -->

5. What is the range of weight for each species included in the study? Remove any observations of weight that are NA so they do not show up in the plot.


```r
deserts %>% 
  filter(weight != "NA") %>% 
  ggplot(aes(x = reorder(species, weight), y = weight, color = species)) +
  geom_boxplot()+
  coord_flip()+
  labs(title = "Weight Range of Species in the Chihuahuan Desert", x = "Species",  y = "Weight")
```

![](lab10_hw_files/figure-html/unnamed-chunk-14-1.png)<!-- -->


6. Add another layer to your answer from #4 using `geom_point` to get an idea of how many measurements were taken for each species.

```r
deserts %>% 
  filter(weight != "NA") %>% 
  ggplot(aes(x = reorder(species, weight), y = weight, color = species)) +
  geom_boxplot()+
  scale_y_log10()+
  geom_point(size = 0.5)+
  coord_flip()+
  labs(title = "Weight Range of Species in the Chihuahuan Desert", x = "Species",  y = "Weight (log10)")
```

![](lab10_hw_files/figure-html/unnamed-chunk-15-1.png)<!-- -->

7. [Dipodomys merriami](https://en.wikipedia.org/wiki/Merriam's_kangaroo_rat) is the most frequently sampled animal in the study. How have the number of observations of this species changed over the years included in the study?

```r
deserts %>% 
  filter(species_id == "DM") %>% 
  tabyl(year)
```

```
##  year   n    percent
##  1977 264 0.02491506
##  1978 389 0.03671197
##  1979 209 0.01972442
##  1980 493 0.04652699
##  1981 559 0.05275576
##  1982 609 0.05747452
##  1983 528 0.04983012
##  1984 396 0.03737259
##  1985 667 0.06294828
##  1986 406 0.03831635
##  1987 469 0.04426199
##  1988 365 0.03444696
##  1989 321 0.03029445
##  1990 462 0.04360136
##  1991 404 0.03812760
##  1992 307 0.02897320
##  1993 253 0.02387693
##  1994 293 0.02765194
##  1995 436 0.04114760
##  1996 492 0.04643262
##  1997 576 0.05436014
##  1998 503 0.04747074
##  1999 348 0.03284258
##  2000 233 0.02198943
##  2001 305 0.02878445
##  2002 309 0.02916195
```


```r
deserts %>% 
  filter(species_id == "DM") %>% 
  ggplot(aes(x = year)) +
  geom_bar() + 
  labs(title = "Dipodomys merriami Observation Count (1977-2002)", y = "Number of Observations", x = "Year")
```

![](lab10_hw_files/figure-html/unnamed-chunk-17-1.png)<!-- -->


8. What is the relationship between `weight` and `hindfoot` length? Consider whether or not over plotting is an issue.

The data is very scattered, therefore it is difficult to make any assumptions about their relationship, but it appears to be a positive one. It seems that over plotting is an issue with this data.


```r
deserts %>% 
  filter(weight != "NA") %>% 
  filter(hindfoot_length != "NA") %>% 
  ggplot(aes(x = weight, y = hindfoot_length))+
  geom_jitter(size = 0.25, na.rm = T)+
  geom_smooth(method = "lm")+
  labs(title = "Relationship Between Species Weight and Hindfoot Length", x = "Weight", y = "Hindfoot Length")
```

```
## `geom_smooth()` using formula 'y ~ x'
```

![](lab10_hw_files/figure-html/unnamed-chunk-18-1.png)<!-- -->


9. Which two species have, on average, the highest weight? Once you have identified them, make a new column that is a ratio of `weight` to `hindfoot_length`. Make a plot that shows the range of this new ratio and fill by sex.

Albigula and spectabilis have the highest average weight.


```r
deserts %>% 
  group_by(species) %>% 
  filter(weight != "NA") %>% 
  summarise(avg_weight = mean(weight)) %>% 
  arrange(desc(avg_weight))
```

```
## # A tibble: 22 x 2
##    species      avg_weight
##    <chr>             <dbl>
##  1 albigula          159. 
##  2 spectabilis       120. 
##  3 spilosoma          93.5
##  4 hispidus           65.6
##  5 fulviventer        58.9
##  6 ochrognathus       55.4
##  7 ordii              48.9
##  8 merriami           43.2
##  9 baileyi            31.7
## 10 leucogaster        31.6
## # ... with 12 more rows
```

```r
deserts %>% 
  filter(weight != "NA") %>% 
  filter(hindfoot_length != "NA") %>% 
  filter(sex != "NA") %>%
  filter(species == "albigula" | species == "spectabilis") %>% 
  group_by(species) %>% 
  mutate(wl_ratio = weight/hindfoot_length) %>% 
  ggplot(aes(x = species, y = wl_ratio, fill = sex))+
  geom_boxplot()+
  labs(title = "Weight-Hindfoot Length Ratio Comparison of Albigula and Spectabilis", x = "Species", y = "Weight : Hindfoot Length Ratio")
```

![](lab10_hw_files/figure-html/unnamed-chunk-20-1.png)<!-- -->


10. Make one plot of your choice! Make sure to include at least two of the aesthetics options you have learned.
look at the number of observations 


```r
deserts %>% 
  filter(species == "penicillatus") %>% 
  filter(sex != "NA") %>% 
  group_by(year, sex) %>% 
  summarise(obs_count = n(), .groups = "keep") %>% 
  ggplot(aes(x = year, y = obs_count, fill = sex))+
  geom_col()+
  labs(title = "Penicillatus Observation Count by Sex (1977-2002)", x = "Year", y = "Number of Observations")
```

![](lab10_hw_files/figure-html/unnamed-chunk-21-1.png)<!-- -->



## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
