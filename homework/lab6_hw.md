---
title: "Lab 6 Homework"
author: "Sidney Parel"
date: "2022-01-25"
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
fisheries <- readr::read_csv(file = "../lab6/data/FAO_1950to2012_111914.csv")
```

```
## Rows: 17692 Columns: 71
```

```
## -- Column specification --------------------------------------------------------
## Delimiter: ","
## chr (69): Country, Common name, ISSCAAP taxonomic group, ASFIS species#, ASF...
## dbl  (2): ISSCAAP group#, FAO major fishing area
```

```
## 
## i Use `spec()` to retrieve the full column specification for this data.
## i Specify the column types or set `show_col_types = FALSE` to quiet this message.
```

1. Do an exploratory analysis of the data (your choice). What are the names of the variables, what are the dimensions, are there any NA's, what are the classes of the variables?  

The names of the variables, dimensions, and counts of NA's are reported in the summary below. The variables with NA's are characters.

```r
fisheries %>% skim()
```


Table: Data summary

|                         |           |
|:------------------------|:----------|
|Name                     |Piped data |
|Number of rows           |17692      |
|Number of columns        |71         |
|_______________________  |           |
|Column type frequency:   |           |
|character                |69         |
|numeric                  |2          |
|________________________ |           |
|Group variables          |None       |


**Variable type: character**

|skim_variable           | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-----------------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|Country                 |         0|          1.00|   4|  25|     0|      204|          0|
|Common name             |         0|          1.00|   3|  30|     0|     1553|          0|
|ISSCAAP taxonomic group |         0|          1.00|   5|  36|     0|       30|          0|
|ASFIS species#          |         0|          1.00|  10|  13|     0|     1553|          0|
|ASFIS species name      |         0|          1.00|   6|  32|     0|     1548|          0|
|Measure                 |         0|          1.00|  17|  17|     0|        1|          0|
|1950                    |     15561|          0.12|   1|   6|     0|      513|          0|
|1951                    |     15550|          0.12|   1|   7|     0|      536|          0|
|1952                    |     15501|          0.12|   1|   7|     0|      553|          0|
|1953                    |     15439|          0.13|   1|   6|     0|      570|          0|
|1954                    |     15417|          0.13|   1|   7|     0|      588|          0|
|1955                    |     15382|          0.13|   1|   7|     0|      589|          0|
|1956                    |     15331|          0.13|   1|   7|     0|      633|          0|
|1957                    |     15253|          0.14|   1|   7|     0|      627|          0|
|1958                    |     15138|          0.14|   1|   6|     0|      643|          0|
|1959                    |     15110|          0.15|   1|   7|     0|      641|          0|
|1960                    |     15016|          0.15|   1|   7|     0|      673|          0|
|1961                    |     14922|          0.16|   1|   8|     0|      713|          0|
|1962                    |     14801|          0.16|   1|   8|     0|      729|          0|
|1963                    |     14707|          0.17|   1|   8|     0|      760|          0|
|1964                    |     14349|          0.19|   1|   8|     0|      759|          0|
|1965                    |     14241|          0.20|   1|   8|     0|      798|          0|
|1966                    |     14187|          0.20|   1|   8|     0|      801|          0|
|1967                    |     14047|          0.21|   1|   8|     0|      815|          0|
|1968                    |     13963|          0.21|   1|   8|     0|      829|          0|
|1969                    |     13920|          0.21|   1|   8|     0|      853|          0|
|1970                    |     13113|          0.26|   1|   8|     0|     1225|          0|
|1971                    |     12925|          0.27|   1|   8|     0|     1326|          0|
|1972                    |     12749|          0.28|   1|   8|     0|     1372|          0|
|1973                    |     12673|          0.28|   1|   8|     0|     1432|          0|
|1974                    |     12583|          0.29|   1|   8|     0|     2601|          0|
|1975                    |     12333|          0.30|   1|   8|     0|     2767|          0|
|1976                    |     12177|          0.31|   1|   8|     0|     2804|          0|
|1977                    |     12014|          0.32|   1|   8|     0|     2867|          0|
|1978                    |     11847|          0.33|   1|   8|     0|     2901|          0|
|1979                    |     11820|          0.33|   1|   8|     0|     2932|          0|
|1980                    |     11747|          0.34|   1|   8|     0|     2956|          0|
|1981                    |     11713|          0.34|   1|   8|     0|     2996|          0|
|1982                    |     11558|          0.35|   1|   9|     0|     3030|          0|
|1983                    |     11453|          0.35|   1|   8|     0|     3031|          0|
|1984                    |     11309|          0.36|   1|   8|     0|     3076|          0|
|1985                    |     11212|          0.37|   1|   8|     0|     3161|          0|
|1986                    |     11086|          0.37|   1|   8|     0|     3242|          0|
|1987                    |     10930|          0.38|   1|   8|     0|     3255|          0|
|1988                    |     10493|          0.41|   1|   8|     0|     3435|          0|
|1989                    |     10435|          0.41|   1|   8|     0|     3425|          0|
|1990                    |     10293|          0.42|   1|   8|     0|     3446|          0|
|1991                    |     10364|          0.41|   1|   8|     0|     3420|          0|
|1992                    |     10435|          0.41|   1|   8|     0|     3322|          0|
|1993                    |     10522|          0.41|   1|   8|     0|     3313|          0|
|1994                    |     10400|          0.41|   1|   8|     0|     3313|          0|
|1995                    |     10148|          0.43|   1|   8|     0|     3329|          0|
|1996                    |      9990|          0.44|   1|   7|     0|     3358|          0|
|1997                    |      9773|          0.45|   1|   9|     0|     3393|          0|
|1998                    |      9579|          0.46|   1|   9|     0|     3399|          0|
|1999                    |      9265|          0.48|   1|   9|     0|     3428|          0|
|2000                    |      8899|          0.50|   1|   9|     0|     3481|          0|
|2001                    |      8646|          0.51|   1|   9|     0|     3490|          0|
|2002                    |      8590|          0.51|   1|   9|     0|     3507|          0|
|2003                    |      8383|          0.53|   1|   9|     0|     3482|          0|
|2004                    |      7977|          0.55|   1|   9|     0|     3505|          0|
|2005                    |      7822|          0.56|   1|   9|     0|     3532|          0|
|2006                    |      7699|          0.56|   1|   9|     0|     3565|          0|
|2007                    |      7589|          0.57|   1|   8|     0|     3551|          0|
|2008                    |      7667|          0.57|   1|   8|     0|     3537|          0|
|2009                    |      7573|          0.57|   1|   8|     0|     3572|          0|
|2010                    |      7499|          0.58|   1|   8|     0|     3590|          0|
|2011                    |      7371|          0.58|   1|   8|     0|     3618|          0|
|2012                    |      7336|          0.59|   1|   8|     0|     3609|          0|


**Variable type: numeric**

|skim_variable          | n_missing| complete_rate|  mean|    sd| p0| p25| p50| p75| p100|hist                                     |
|:----------------------|---------:|-------------:|-----:|-----:|--:|---:|---:|---:|----:|:----------------------------------------|
|ISSCAAP group#         |         0|             1| 37.38|  7.88| 11|  33|  36|  38|   77|▁▇▂▁▁ |
|FAO major fishing area |         0|             1| 45.34| 18.33| 18|  31|  37|  57|   88|▇▇▆▃▃ |


2. Use `janitor` to rename the columns and make them easier to use. As part of this cleaning step, change `country`, `isscaap_group_number`, `asfis_species_number`, and `fao_major_fishing_area` to data class factor. 

```r
fisheries <- fisheries %>% 
  clean_names() %>% 
  mutate(across(c(country, isscaap_group_number, asfis_species_number, fao_major_fishing_area), as.factor))
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

203 countries are represented in the data. A list of the countries represented and the number of observations associated with each country is reported below.


```r
fisheries_tidy %>% 
  count(country)
```

```
## # A tibble: 203 x 2
##    country                 n
##    <fct>               <int>
##  1 Albania               934
##  2 Algeria              1561
##  3 American Samoa        556
##  4 Angola               2119
##  5 Anguilla              129
##  6 Antigua and Barbuda   356
##  7 Argentina            3403
##  8 Aruba                 172
##  9 Australia            8183
## 10 Bahamas               423
## # ... with 193 more rows
```

4. Refocus the data only to include country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch.

```r
fisheries_tidy2 <- fisheries_tidy %>% 
  select(country, isscaap_taxonomic_group, asfis_species_name, asfis_species_number, year, catch)
```

5. Based on the asfis_species_number, how many distinct fish species were caught as part of these data?

Based on the asfis_species_number, 1551 distinct fish species were caught.

```r
fisheries_tidy2 %>% 
  summarize(distinct_species = n_distinct(asfis_species_number))
```

```
## # A tibble: 1 x 1
##   distinct_species
##              <int>
## 1             1551
```

6. Which country had the largest overall catch in the year 2000?

China had the largest overall catch of a single species in the year 2000.

```r
fisheries_tidy2 %>% 
  group_by(country) %>% 
  filter(!is.na(catch), year == "2000") %>% 
  summarize(largest_overall_catch = max(catch)) %>% 
  arrange(desc(largest_overall_catch))
```

```
## # A tibble: 187 x 2
##    country                  largest_overall_catch
##    <fct>                                    <dbl>
##  1 China                                     9068
##  2 Peru                                      5717
##  3 Russian Federation                        5065
##  4 Viet Nam                                  4945
##  5 Chile                                     4299
##  6 United States of America                  2438
##  7 Philippines                                999
##  8 Japan                                      988
##  9 Bangladesh                                 977
## 10 Senegal                                    970
## # ... with 177 more rows
```
China also had the largest catch across all species in the year 2000.

```r
fisheries_tidy2 %>% 
  group_by(country) %>% 
  filter(!is.na(catch), year == "2000") %>% 
  summarize(largest_overall_catch = sum(catch)) %>% 
  arrange(desc(largest_overall_catch))
```

```
## # A tibble: 187 x 2
##    country                  largest_overall_catch
##    <fct>                                    <dbl>
##  1 China                                    25899
##  2 Russian Federation                       12181
##  3 United States of America                 11762
##  4 Japan                                     8510
##  5 Indonesia                                 8341
##  6 Peru                                      7443
##  7 Chile                                     6906
##  8 India                                     6351
##  9 Thailand                                  6243
## 10 Korea, Republic of                        6124
## # ... with 177 more rows
```

7. Which country caught the most sardines (_Sardina pilchardus_) between the years 1990-2000?

Morocco caught the most sardines between the years 1990 - 2000.

```r
fisheries_tidy2 %>% 
  group_by(country) %>% 
  filter(!is.na(catch), 
         between(year, "1990", "2000"), 
         asfis_species_name == "Sardina pilchardus") %>% 
  summarize(sardines_caught = sum(catch)) %>% 
  arrange(desc(sardines_caught))
```

```
## # A tibble: 37 x 2
##    country               sardines_caught
##    <fct>                           <dbl>
##  1 Morocco                          7470
##  2 Spain                            3507
##  3 Russian Federation               1639
##  4 Ukraine                          1030
##  5 France                            966
##  6 Portugal                          818
##  7 Greece                            528
##  8 Italy                             507
##  9 Serbia and Montenegro             478
## 10 Denmark                           477
## # ... with 27 more rows
```

8. Which five countries caught the most cephalopods between 2008-2012?

Cephalopods are recorded in `isscaap_taxonomic_group` as "Squids, cuttlefishes, octopuses".

```r
fisheries_tidy2$isscaap_taxonomic_group %>% unique()
```

```
##  [1] "Sharks, rays, chimaeras"             
##  [2] "Tunas, bonitos, billfishes"          
##  [3] "Miscellaneous pelagic fishes"        
##  [4] "Shrimps, prawns"                     
##  [5] "Cods, hakes, haddocks"               
##  [6] "Miscellaneous coastal fishes"        
##  [7] "Squids, cuttlefishes, octopuses"     
##  [8] "Flounders, halibuts, soles"          
##  [9] "Lobsters, spinyrock lobsters"        
## [10] "Herrings, sardines, anchovies"       
## [11] "Miscellaneous demersal fishes"       
## [12] "Marine fishes not identified"        
## [13] "Mussels"                             
## [14] "Crabs, seaspiders"                   
## [15] "Seaurchins and other echinoderms"    
## [16] "Clams, cockles, arkshells"           
## [17] "Miscellaneous marine crustaceans"    
## [18] "Miscellaneous marine molluscs"       
## [19] "Shads"                               
## [20] "Abalones, winkles, conchs"           
## [21] "Scallops, pectens"                   
## [22] "King crabs, squatlobsters"           
## [23] "Miscellaneous aquatic invertebrates" 
## [24] "Miscellaneous diadromous fishes"     
## [25] "Oysters"                             
## [26] "Sturgeons, paddlefishes"             
## [27] "Salmons, trouts, smelts"             
## [28] "Carps, barbels and other cyprinids"  
## [29] "Tilapias and other cichlids"         
## [30] "Horseshoe crabs and other arachnoids"
```
The 5 countries which caught the most cephalopods between 2008 - 2012 are reported below.

```r
fisheries_tidy2 %>% 
  group_by(country) %>% 
  filter(!is.na(catch), 
         isscaap_taxonomic_group == "Squids, cuttlefishes, octopuses", 
         between(year, "2008", "2012")) %>% 
  summarize(cephalopods_caught = sum(catch)) %>% 
  arrange(desc(cephalopods_caught)) %>% 
  head(5)
```

```
## # A tibble: 5 x 2
##   country            cephalopods_caught
##   <fct>                           <dbl>
## 1 China                            8349
## 2 Korea, Republic of               3480
## 3 Peru                             3422
## 4 Japan                            3248
## 5 Chile                            2775
```

9. Which species had the highest catch total between 2008-2012? (hint: Osteichthyes is not a species)

_Theragra chalcogramma_ had the highest catch total between 2008 - 2012.

```r
fisheries_tidy2 %>% 
  group_by(asfis_species_name) %>% 
  filter(!is.na(catch), 
         between(year, "2008", "2012"), 
         asfis_species_name != "Osteichthyes") %>% 
  summarize(catch_total = sum(catch)) %>% 
  arrange(desc(catch_total))
```

```
## # A tibble: 1,352 x 2
##    asfis_species_name    catch_total
##    <chr>                       <dbl>
##  1 Theragra chalcogramma       41075
##  2 Engraulis ringens           35523
##  3 Katsuwonus pelamis          32153
##  4 Trichiurus lepturus         30400
##  5 Clupea harengus             28527
##  6 Thunnus albacares           20119
##  7 Scomber japonicus           14723
##  8 Gadus morhua                13253
##  9 Thunnus alalunga            12019
## 10 Natantia                    11984
## # ... with 1,342 more rows
```

10. Use the data to do at least one analysis of your choice.

Were more shrimps and prawns caught in the United States in 2000 or in 2010?

```r
# shrimps and prawns caught in 2000
fisheries_tidy2 %>% 
  filter(!is.na(catch), 
         year == 2000, 
         isscaap_taxonomic_group == "Shrimps, prawns",
         country == "United States of America") %>% 
  summarize(catch_total = sum(catch))
```

```
## # A tibble: 1 x 1
##   catch_total
##         <dbl>
## 1         282
```

```r
# shrimps and prawns caught in 2010
fisheries_tidy2 %>% 
  filter(!is.na(catch), 
         year == 2010, 
         isscaap_taxonomic_group == "Shrimps, prawns",
         country == "United States of America") %>% 
  summarize(catch_total = sum(catch))
```

```
## # A tibble: 1 x 1
##   catch_total
##         <dbl>
## 1         262
```
More shrimps and prawns were caught in 2000.

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences.   
