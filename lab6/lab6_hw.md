---
title: "Lab 6 Homework"
author: "Margarita I"
date: "2021-01-26"
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
library(skimr)
```

For this assignment we are going to work with a large data set from the [United Nations Food and Agriculture Organization](http://www.fao.org/about/en/) on world fisheries. These data are pretty wild, so we need to do some cleaning. First, load the data.  

Load the data `FAO_1950to2012_111914.csv` as a new object titled `fisheries`.

```r
fisheries <- readr::read_csv("data/FAO_1950to2012_111914.csv")
```

```
## 
## ── Column specification ────────────────────────────────────────────────────────
## cols(
##   .default = col_character(),
##   `ISSCAAP group#` = col_double(),
##   `FAO major fishing area` = col_double()
## )
## ℹ Use `spec()` for the full column specifications.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

```r
glimpse(fisheries)
```

```
## Rows: 17,692
## Columns: 71
## $ Country                   <chr> "Albania", "Albania", "Albania", "Albania",…
## $ `Common name`             <chr> "Angelsharks, sand devils nei", "Atlantic b…
## $ `ISSCAAP group#`          <dbl> 38, 36, 37, 45, 32, 37, 33, 45, 38, 57, 33,…
## $ `ISSCAAP taxonomic group` <chr> "Sharks, rays, chimaeras", "Tunas, bonitos,…
## $ `ASFIS species#`          <chr> "10903XXXXX", "1750100101", "17710001XX", "…
## $ `ASFIS species name`      <chr> "Squatinidae", "Sarda sarda", "Sphyraena sp…
## $ `FAO major fishing area`  <dbl> 37, 37, 37, 37, 37, 37, 37, 37, 37, 37, 37,…
## $ Measure                   <chr> "Quantity (tonnes)", "Quantity (tonnes)", "…
## $ `1950`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1951`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1952`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1953`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1954`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1955`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1956`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1957`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1958`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1959`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1960`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1961`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1962`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1963`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1964`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1965`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1966`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1967`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1968`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1969`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1970`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1971`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1972`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1973`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1974`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1975`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1976`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1977`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1978`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1979`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1980`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1981`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1982`                    <chr> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA,…
## $ `1983`                    <chr> NA, NA, NA, NA, NA, NA, "559", NA, NA, NA, …
## $ `1984`                    <chr> NA, NA, NA, NA, NA, NA, "392", NA, NA, NA, …
## $ `1985`                    <chr> NA, NA, NA, NA, NA, NA, "406", NA, NA, NA, …
## $ `1986`                    <chr> NA, NA, NA, NA, NA, NA, "499", NA, NA, NA, …
## $ `1987`                    <chr> NA, NA, NA, NA, NA, NA, "564", NA, NA, NA, …
## $ `1988`                    <chr> NA, NA, NA, NA, NA, NA, "724", NA, NA, NA, …
## $ `1989`                    <chr> NA, NA, NA, NA, NA, NA, "583", NA, NA, NA, …
## $ `1990`                    <chr> NA, NA, NA, NA, NA, NA, "754", NA, NA, NA, …
## $ `1991`                    <chr> NA, NA, NA, NA, NA, NA, "283", NA, NA, NA, …
## $ `1992`                    <chr> NA, NA, NA, NA, NA, NA, "196", NA, NA, NA, …
## $ `1993`                    <chr> NA, NA, NA, NA, NA, NA, "150 F", NA, NA, NA…
## $ `1994`                    <chr> NA, NA, NA, NA, NA, NA, "100 F", NA, NA, NA…
## $ `1995`                    <chr> "0 0", "1", NA, "0 0", "0 0", NA, "52", "30…
## $ `1996`                    <chr> "53", "2", NA, "3", "2", NA, "104", "8", NA…
## $ `1997`                    <chr> "20", "0 0", NA, "0 0", "0 0", NA, "65", "4…
## $ `1998`                    <chr> "31", "12", NA, NA, NA, NA, "220", "18", NA…
## $ `1999`                    <chr> "30", "30", NA, NA, NA, NA, "220", "18", NA…
## $ `2000`                    <chr> "30", "25", "2", NA, NA, NA, "220", "20", N…
## $ `2001`                    <chr> "16", "30", NA, NA, NA, NA, "120", "23", NA…
## $ `2002`                    <chr> "79", "24", NA, "34", "6", NA, "150", "84",…
## $ `2003`                    <chr> "1", "4", NA, "22", NA, NA, "84", "178", NA…
## $ `2004`                    <chr> "4", "2", "2", "15", "1", "2", "76", "285",…
## $ `2005`                    <chr> "68", "23", "4", "12", "5", "6", "68", "150…
## $ `2006`                    <chr> "55", "30", "7", "18", "8", "9", "86", "102…
## $ `2007`                    <chr> "12", "19", NA, NA, NA, NA, "132", "18", NA…
## $ `2008`                    <chr> "23", "27", NA, NA, NA, NA, "132", "23", NA…
## $ `2009`                    <chr> "14", "21", NA, NA, NA, NA, "154", "20", NA…
## $ `2010`                    <chr> "78", "23", "7", NA, NA, NA, "80", "228", N…
## $ `2011`                    <chr> "12", "12", NA, NA, NA, NA, "88", "9", NA, …
## $ `2012`                    <chr> "5", "5", NA, NA, NA, NA, "129", "290", NA,…
```

2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <- janitor::clean_names(fisheries)
names(fisheries)
```

```
##  [1] "country"                 "common_name"            
##  [3] "isscaap_group_number"    "isscaap_taxonomic_group"
##  [5] "asfis_species_number"    "asfis_species_name"     
##  [7] "fao_major_fishing_area"  "measure"                
##  [9] "x1950"                   "x1951"                  
## [11] "x1952"                   "x1953"                  
## [13] "x1954"                   "x1955"                  
## [15] "x1956"                   "x1957"                  
## [17] "x1958"                   "x1959"                  
## [19] "x1960"                   "x1961"                  
## [21] "x1962"                   "x1963"                  
## [23] "x1964"                   "x1965"                  
## [25] "x1966"                   "x1967"                  
## [27] "x1968"                   "x1969"                  
## [29] "x1970"                   "x1971"                  
## [31] "x1972"                   "x1973"                  
## [33] "x1974"                   "x1975"                  
## [35] "x1976"                   "x1977"                  
## [37] "x1978"                   "x1979"                  
## [39] "x1980"                   "x1981"                  
## [41] "x1982"                   "x1983"                  
## [43] "x1984"                   "x1985"                  
## [45] "x1986"                   "x1987"                  
## [47] "x1988"                   "x1989"                  
## [49] "x1990"                   "x1991"                  
## [51] "x1992"                   "x1993"                  
## [53] "x1994"                   "x1995"                  
## [55] "x1996"                   "x1997"                  
## [57] "x1998"                   "x1999"                  
## [59] "x2000"                   "x2001"                  
## [61] "x2002"                   "x2003"                  
## [63] "x2004"                   "x2005"                  
## [65] "x2006"                   "x2007"                  
## [67] "x2008"                   "x2009"                  
## [69] "x2010"                   "x2011"                  
## [71] "x2012"
```


```r
fisheries$country <- as.factor(fisheries$country)
fisheries$isscaap_group_number <- as.factor(fisheries$isscaap_group_number)
fisheries$asfis_species_number <- as.factor(fisheries$asfis_species_number)
fisheries$fao_major_fishing_area <- as.factor(fisheries$fao_major_fishing_area)
```

We need to deal with the years because they are being treated as characters and start with an X. We also have the problem that the column names that are years actually represent data. We haven't discussed tidy data yet, so here is some help. You should run this ugly chunk to transform the data for the rest of the homework. It will only work if you have used janitor to rename the variables in question 2!

```r
fisheries_tidy <- fisheries %>% 
  pivot_longer(-c(country,common_name,isscaap_group_number,isscaap_taxonomic_group,asfis_species_number,asfis_species_name,fao_major_fishing_area,measure),
               names_to = "year",
               values_to = "catch",
               values_drop_na = TRUE) %>% 
  mutate(year= as.numeric(str_replace(year, 'x', ''))) %>% 
  mutate(catch= str_replace(catch, c(' F'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('...'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('-'), replacement = '')) %>% 
  mutate(catch= str_replace(catch, c('0 0'), replacement = ''))

fisheries_tidy$catch <- as.numeric(fisheries_tidy$catch)
```

3. How many countries are represented in the data? Provide a count and list their names.

```r
fisheries_tidy %>% 
  count(country, sort = T)
```

```
## # A tibble: 203 x 2
##    country                      n
##    <fct>                    <int>
##  1 United States of America 18080
##  2 Spain                    17482
##  3 Japan                    15429
##  4 Portugal                 11570
##  5 Korea, Republic of       10824
##  6 France                   10639
##  7 Taiwan Province of China  9927
##  8 Indonesia                 9274
##  9 Australia                 8183
## 10 Un. Sov. Soc. Rep.        7084
## # … with 193 more rows
```


```r
fisheries_tidy %>% 
  summarize(numcountries = n_distinct(country))
```

```
## # A tibble: 1 x 1
##   numcountries
##          <int>
## 1          203
```


4. Refocus the data only to include only: country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
```

```
## # A tibble: 376,771 x 6
##    country isscaap_taxonomic_g… asfis_species_na… asfis_species_num…  year catch
##    <fct>   <chr>                <chr>             <fct>              <dbl> <dbl>
##  1 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          1995    NA
##  2 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          1996    53
##  3 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          1997    20
##  4 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          1998    31
##  5 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          1999    30
##  6 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          2000    30
##  7 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          2001    16
##  8 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          2002    79
##  9 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          2003     1
## 10 Albania Sharks, rays, chima… Squatinidae       10903XXXXX          2004     4
## # … with 376,761 more rows
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

```r
fisheries_tidy %>% 
  summarize(distinctfish = n_distinct(asfis_species_name))
```

```
## # A tibble: 1 x 1
##   distinctfish
##          <int>
## 1         1546
```

6. Which country had the largest overall catch in the year 2000?
China had the biggest.

```r
fisheries_tidy %>% 
  filter(year == 2000)%>% 
  group_by(country) %>% 
  summarize(biggest_fish=max(catch, na.rm=T)) %>% 
  arrange(desc(biggest_fish))
```

```
## Warning in max(catch, na.rm = T): no non-missing arguments to max; returning -
## Inf

## Warning in max(catch, na.rm = T): no non-missing arguments to max; returning -
## Inf

## Warning in max(catch, na.rm = T): no non-missing arguments to max; returning -
## Inf

## Warning in max(catch, na.rm = T): no non-missing arguments to max; returning -
## Inf

## Warning in max(catch, na.rm = T): no non-missing arguments to max; returning -
## Inf

## Warning in max(catch, na.rm = T): no non-missing arguments to max; returning -
## Inf
```

```
## # A tibble: 193 x 2
##    country                  biggest_fish
##    <fct>                           <dbl>
##  1 China                            9068
##  2 Peru                             5717
##  3 Russian Federation               5065
##  4 Viet Nam                         4945
##  5 Chile                            4299
##  6 United States of America         2438
##  7 Philippines                       999
##  8 Japan                             988
##  9 Bangladesh                        977
## 10 Senegal                           970
## # … with 183 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?
Morocco caught the most sardines.


```r
fisheries_tidy %>% 
  filter(year >= 1990, year <= 2000) %>% 
  filter(asfis_species_name == "Sardina pilchardus") %>% 
  group_by(country) %>% 
  summarize(sardines=sum(catch, na.rm=T)) %>% 
  arrange(desc(sardines))
```

```
## # A tibble: 37 x 2
##    country               sardines
##    <fct>                    <dbl>
##  1 Morocco                   7470
##  2 Spain                     3507
##  3 Russian Federation        1639
##  4 Ukraine                   1030
##  5 France                     966
##  6 Portugal                   818
##  7 Greece                     528
##  8 Italy                      507
##  9 Serbia and Montenegro      478
## 10 Denmark                    477
## # … with 27 more rows
```

8. Which five countries caught the most cephalopods between 2008-2012?

India, China, Spain, Algeria and France caught the most.  

```r
fisheries_tidy %>% 
  filter(year >= 2008, year <= 2012) %>% 
  filter(asfis_species_name == "Cephalopoda") %>% 
  group_by(country) %>% 
  summarize(cephalopods=sum(catch, na.rm=T)) %>% 
  arrange(desc(cephalopods))
```

```
## # A tibble: 16 x 2
##    country                  cephalopods
##    <fct>                          <dbl>
##  1 India                            570
##  2 China                            257
##  3 Spain                            198
##  4 Algeria                          162
##  5 France                           101
##  6 Mauritania                        90
##  7 TimorLeste                        76
##  8 Italy                             66
##  9 Mozambique                        16
## 10 Cambodia                          15
## 11 Taiwan Province of China          13
## 12 Madagascar                        11
## 13 Croatia                            7
## 14 Israel                             0
## 15 Somalia                            0
## 16 Viet Nam                           0
```

9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)
Theragra chalcogramma had the highest catch total.


```r
fisheries_tidy %>% 
  filter(between(year, 2008, 2012)) %>% 
  group_by(asfis_species_name) %>% 
  summarize(totalcatch=sum(catch)) %>% 
  arrange(desc(totalcatch))
```

```
## # A tibble: 1,472 x 2
##    asfis_species_name    totalcatch
##    <chr>                      <dbl>
##  1 Theragra chalcogramma      41075
##  2 Engraulis ringens          35523
##  3 Cololabis saira             5733
##  4 Sardinella longiceps        3849
##  5 Sardinops caeruleus         3204
##  6 Brevoortia patronus         3179
##  7 Acetes japonicus            2915
##  8 Squillidae                  2884
##  9 Trachurus japonicus         2710
## 10 Ammodytes personatus        2611
## # … with 1,462 more rows
```

10. Use the data to do at least one analysis of your choice.

```r
fisheries_tidy %>% 
  filter(year == 2008) %>% 
  filter(asfis_species_name == "Squillidae") %>% 
  group_by(country) %>% 
  summarize(sq = sum(catch)) %>% 
  arrange(desc(sq))
```

```
## # A tibble: 2 x 2
##   country        sq
##   <fct>       <dbl>
## 1 China         873
## 2 Philippines     6
```

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   