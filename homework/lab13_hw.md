---
title: "Lab 13 Homework"
author: "Sidney Parel"
date: "2022-02-25"
output:
  html_document: 
    theme: spacelab
    keep_md: yes
---



## Instructions
Answer the following questions and complete the exercises in RMarkdown. Please embed all of your code and push your final work to your repository. Your final lab report should be organized, clean, and run free from errors. Remember, you must remove the `#` for the included code chunks to run. Be sure to add your name to the author header above. For any included plots, make sure they are clearly labeled. You are free to use any plot type that you feel best communicates the results of your analysis.  

Make sure to use the formatting conventions of RMarkdown to make your report neat and clean!  

## Libraries

```r
library(tidyverse)
library(shiny)
library(shinydashboard)
library(dashboardthemes)
library(janitor)
library(skimr)
```

## Choose Your Adventure!
For this homework assignment, you have two choices of data. You only need to build an app for one of them. The first dataset is focused on UC Admissions and the second build on the Gabon data that we used for midterm 1.  

## Option 1
The data for this assignment come from the [University of California Information Center](https://www.universityofcalifornia.edu/infocenter). Admissions data were collected for the years 2010-2019 for each UC campus. Admissions are broken down into three categories: applications, admits, and enrollees. The number of individuals in each category are presented by demographic.  

**1. Load the `UC_admit.csv` data and use the function(s) of your choice to get an idea of the overall structure of the data frame, including its dimensions, column names, variable classes, etc. As part of this, determine if there are NA's and how they are treated.**  


**2. The president of UC has asked you to build a shiny app that shows admissions by ethnicity across all UC campuses. Your app should allow users to explore year, campus, and admit category as interactive variables. Use shiny dashboard and try to incorporate the aesthetics you have learned in ggplot to make the app neat and clean.**


**3. Make alternate version of your app above by tracking enrollment at a campus over all of the represented years while allowing users to interact with campus, category, and ethnicity.**  


## Option 2
We will use data from a study on vertebrate community composition and impacts from defaunation in Gabon, Africa. Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition and diversity declines along a defaunation gradient radiating from rural villages in Gabon. _Journal of Applied Ecology_. 2016.   

**1. Load the `IvindoData_DryadVersion.csv` data and use the function(s) of your choice to get an idea of the overall structure, including its dimensions, column names, variable classes, etc. As part of this, determine if NA's are present and how they are treated.** 

A summary of the structure of the data is reported below. The data does not contain any NA's.

```r
gabon <- read_csv("../lab13/data/gabon_data/IvindoData_DryadVersion.csv") %>% 
  clean_names()

gabon %>% 
  skim()
```


Table: Data summary

|                         |           |
|:------------------------|:----------|
|Name                     |Piped data |
|Number of rows           |24         |
|Number of columns        |26         |
|_______________________  |           |
|Column type frequency:   |           |
|character                |2          |
|numeric                  |24         |
|________________________ |           |
|Group variables          |None       |


**Variable type: character**

|skim_variable | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|hunt_cat      |         0|             1|   4|   8|     0|        3|          0|
|land_use      |         0|             1|   4|   7|     0|        3|          0|


**Variable type: numeric**

|skim_variable            | n_missing| complete_rate|  mean|    sd|    p0|   p25|   p50|   p75|  p100|hist                                     |
|:------------------------|---------:|-------------:|-----:|-----:|-----:|-----:|-----:|-----:|-----:|:----------------------------------------|
|transect_id              |         0|             1| 13.50|  8.51|  1.00|  5.75| 14.50| 20.25| 27.00|▇▃▅▆▆ |
|distance                 |         0|             1| 11.88|  7.28|  2.70|  5.67|  9.72| 17.68| 26.76|▇▂▂▅▂ |
|num_households           |         0|             1| 37.88| 17.80| 13.00| 24.75| 29.00| 54.00| 73.00|▇▇▂▇▂ |
|veg_rich                 |         0|             1| 14.83|  2.07| 10.88| 13.10| 14.94| 16.54| 18.75|▃▂▃▇▁ |
|veg_stems                |         0|             1| 32.80|  5.96| 23.44| 28.69| 32.44| 37.08| 47.56|▆▇▆▃▁ |
|veg_liana                |         0|             1| 11.04|  3.29|  4.75|  9.03| 11.94| 13.25| 16.38|▃▂▃▇▃ |
|veg_dbh                  |         0|             1| 46.09| 10.67| 28.45| 40.65| 43.90| 50.57| 76.48|▂▇▃▁▁ |
|veg_canopy               |         0|             1|  3.47|  0.35|  2.50|  3.25|  3.43|  3.75|  4.00|▁▁▇▅▇ |
|veg_understory           |         0|             1|  3.02|  0.34|  2.38|  2.88|  3.00|  3.17|  3.88|▂▆▇▂▁ |
|ra_apes                  |         0|             1|  2.04|  3.03|  0.00|  0.00|  0.48|  3.82| 12.93|▇▂▁▁▁ |
|ra_birds                 |         0|             1| 58.64| 14.71| 31.56| 52.51| 57.89| 68.18| 85.03|▅▅▇▇▃ |
|ra_elephant              |         0|             1|  0.54|  0.67|  0.00|  0.00|  0.36|  0.89|  2.30|▇▂▂▁▁ |
|ra_monkeys               |         0|             1| 31.30| 12.38|  5.84| 22.70| 31.74| 39.88| 54.12|▂▅▃▇▂ |
|ra_rodent                |         0|             1|  3.28|  1.47|  1.06|  2.05|  3.23|  4.09|  6.31|▇▅▇▃▃ |
|ra_ungulate              |         0|             1|  4.17|  4.31|  0.00|  1.23|  2.54|  5.16| 13.86|▇▂▁▁▂ |
|rich_all_species         |         0|             1| 20.21|  2.06| 15.00| 19.00| 20.00| 22.00| 24.00|▁▁▇▅▁ |
|evenness_all_species     |         0|             1|  0.77|  0.05|  0.67|  0.75|  0.78|  0.81|  0.83|▃▁▅▇▇ |
|diversity_all_species    |         0|             1|  2.31|  0.15|  1.97|  2.25|  2.32|  2.43|  2.57|▂▃▇▆▅ |
|rich_bird_species        |         0|             1| 10.33|  1.24|  8.00| 10.00| 11.00| 11.00| 13.00|▃▅▇▁▁ |
|evenness_bird_species    |         0|             1|  0.71|  0.08|  0.56|  0.68|  0.72|  0.77|  0.82|▅▁▇▆▇ |
|diversity_bird_species   |         0|             1|  1.66|  0.20|  1.16|  1.60|  1.68|  1.78|  2.01|▂▂▅▇▃ |
|rich_mammal_species      |         0|             1|  9.88|  1.68|  6.00|  9.00| 10.00| 11.00| 12.00|▂▂▃▅▇ |
|evenness_mammal_species  |         0|             1|  0.75|  0.06|  0.62|  0.71|  0.74|  0.78|  0.86|▂▃▇▂▅ |
|diversity_mammal_species |         0|             1|  1.70|  0.17|  1.38|  1.57|  1.70|  1.81|  2.06|▅▇▇▇▃ |

**2. Build an app that re-creates the plots shown on page 810 of this paper. The paper is included in the folder. It compares the relative abundance % to the distance from villages in rural Gabon. Use shiny dashboard and add aesthetics to the plot.  **  

```r
# Extract the relative abundance and distance data:
all_ra <- gabon %>% 
  select(c(transect_id, starts_with("ra"), distance)) %>% 
  # Pivot longer to create taxon and relative abundance columns.
  pivot_longer(-c(transect_id, distance), 
               names_to = "taxon",
               names_prefix = "ra_",
               values_to = "ra") %>%
  # Change taxon column to factor and rename levels to match taxon names in the paper.
  mutate(taxon = str_to_title(taxon),
         taxon = factor(taxon),
         taxon = recode(taxon,
                          Elephant = "Elephants",
                          Rodent = "Rodents",
                          Ungulate = "Ungulates"))


# Create a reference plot for the shiny dashboard:
# ggplot(data = all_ra %>% 
#         filter(taxon == "birds")) +
# geom_point(aes(x = distance, y = ra), size = 2) +
# geom_smooth(aes(x = distance, y = ra), method = lm, color = "black") 
```


```r
# Create the shiny dashboard:
ui <- dashboardPage(
  dashboardHeader(title = "Rural Gabon"),
  dashboardSidebar(disable = T),
  dashboardBody(
    shinyDashboardThemes(
      theme = "poor_mans_flatly"),
    fluidRow(
      box(title = "Taxon", width = 4,
          selectInput("taxon", "Select a taxon of interest:", choices = unique(all_ra$taxon),
                      selected = "birds"),
          helpText("Reference: Koerner SE, Poulsen JR, Blanchard EJ, Okouyi J, Clark CJ. Vertebrate community composition
                   and diversity declines along a defaunation gradient radiating from rural villages in Gabon. Journal
                   of Applied Ecology. 2016.")),
      box(title = "Relative abundance of taxonomic guilds with distance from the nearest village in the Ivindo
                   landscape",
          plotOutput("plot"))
    )
  )
)
  
server <- function(input, output, session){
  session$onSessionEnded(stopApp)
  
  output$plot <- renderPlot({
    all_ra %>% 
      filter(taxon == input$taxon) %>% 
      ggplot() +
        geom_point(aes_string(x = "distance", y = "ra"), color = "darkorange", alpha = 0.5, size = 2) +
        geom_smooth(aes_string(x = "distance", y = "ra"), color = "darkorange", method = lm) +
        labs(x = "Distance to nearest village (km)",
             y = "Relative abundance (%)",
             color = NULL) +
        theme_minimal()
  })
}  

shinyApp(ui, server)
```

`<div style="width: 100% ; height: 400px ; text-align: center; box-sizing: border-box; -moz-box-sizing: border-box; -webkit-box-sizing: border-box;" class="muted well">Shiny applications not supported in static R Markdown documents</div>`{=html}

## Push your final code to GitHub!
Please be sure that you check the `keep md` file in the knit preferences. 
