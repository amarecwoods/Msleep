# GitHub Documentation for R Data Analysis Workflow

## Introduction

This repository contains R code and documentation for a data analysis workflow using the `tidyverse` and other relevant packages. The analysis involves exploring and visualizing the sleep patterns and body weights of animals.

## Getting Started

To replicate the analysis, follow the steps below:

1. Install and load the `tidyverse` package:

   ```R
   install.packages('tidyverse')
   library(tidyverse)
   ```

2. Load the `msleep` dataset and explore its structure:

   ```R
   head(msleep)
   summarize(msleep)
   ```

   Identify and handle missing data:

   ```R
   missingdata <- !complete.cases(msleep)
   view(missingdata)
   msleep[missingdata,]
   ```

3. Subset relevant columns from the dataset:

   ```R
   RelevantMSLeep <- select(msleep, name, genus, vore, sleep_total, bodywt, awake)
   View(RelevantMSLeep)
   ```

   Filter out rows with incomplete data:

   ```R
   CompleteRevelantMsleep <- !complete.cases(RelevantMSLeep)
   RelevantMSLeep[CompleteRevelantMsleep,] %>%
     rename("Animal" = "name") %>%
     FinalMsleep <- select(Animal, vore, sleep_total, bodywt, awake)
   view(FinalMsleep)
   ```

4. Install and load the `googlesheets4` package:

   ```R
   install.packages("googlesheets4")
   library(googlesheets4)
   ```

   Read data from a Google Sheets document:

   ```R
   FinalMsleep <- read_sheet('https://docs.google.com/spreadsheets/d/1UyvrJ14oumkPtzYkDsh_lrbm1Z3Qrk5tsQ9tETVVK_s/edit?usp=sharing') %>%
     view()
   ```

   Check the class of the 'Weight(lbs)' column:

   ```R
   class(FinalMsleep$`Weight(lbs)`)
   ```

5. Explore and visualize the data:

   ```R
   # Scatterplot
   FinalMsleep %>%
     drop_na(vore) %>%
     ggplot(aes(`Sleep Total`, `Weight(lbs)`, color = vore)) +
     geom_point(size = 5, alpha = 0.5) +
     theme_bw() +
     labs(title = "Sleep Total by Diet")
   ```

6. Further exploration:

   ```R
   ?msleep
   ```

   Additional visualization:

   ```R
   FinalMsleep %>%
     drop_na(vore) %>%
     ggplot(aes(`Sleep Total`, `Weight(lbs)`, color = vore)) +
     geom_point(size = 5, alpha = 0.5) +
     theme_bw() +
     labs(title = "Sleep Total by Diet")
   ```

7. Install and load the `rmarkdown` package for report generation:

   ```R
   install.packages("rmarkdown")
   library(rmarkdown)
   ```

8. Perform data transformations and view the results:

   ```R
   RelevantMSLeep %>%
     mutate(BodyWeigthlbs = bodywt/2.20462 ) %>%
     mutate(round(BodyWeigthlbs, digits = 2)) %>%
     View()
   ```

## Conclusion

This GitHub repository provides a comprehensive analysis of sleep patterns and body weights in animals, utilizing the `tidyverse` and other relevant R packages. The workflow includes data cleaning, exploration, visualization, and report generation. Feel free to explore the code and adapt it to your specific needs.
