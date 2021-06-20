---
title: Graduate Student Satisfaction Exit Surveys
author: ''
date: '2021-06-19'
slug: graduate-student-satisfaction-exit-surveys
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-04-30T20:40:15-07:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

This post was originally designed because I was interested in working on student experience exit survey data from my department to see if there was a change from 2012 to 2015. These questions are given to every student that graduates from a graduate program at the University of Oregon (UO). This also applies for doctoral students that complete the requirements for a master's degree on their way to their final PhD program. This data is open to any UO student, staff, or faculty member that has login information for this data. 

This data ended up becoming a real time commitment as there was no efficient way to collect data from the pdf files for each College at the UO. An example can be seen [here](https://github.com/jpedroza1228/exitsurveys/blob/main/pdf_data/exit_surveys/student_experience_survey/2015/2015-AAA-Grad-Experience-Survey-Report.pdf). One great resource for collecting data from pdfs was to use the [*pdftools*](https://cran.r-project.org/web/packages/pdftools/pdftools.pdf) package, but if you look at the example link provided above the UO Graduate School decided to color code cells in the table, which threw off any function to extract all the values in an efficient manner. Anyway...

The [data](https://github.com/jpedroza1228/exitsurveys/blob/main/data/student_experience.csv) and other existing data files can be found [here](https://github.com/jpedroza1228/exitsurveys/tree/main/pdf_data/exit_surveys). When I have some more free time, I may decide to join the other datasets to the student experience data to examine some more interesting questions regarding this data. But for now, lets look at the student experience data.


```r
library(tidyverse)
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.1.1     v dplyr   1.0.5
## v tidyr   1.1.3     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.1
```

```
## Warning: package 'ggplot2' was built under R version 4.0.4
```

```
## Warning: package 'tibble' was built under R version 4.0.5
```

```
## Warning: package 'tidyr' was built under R version 4.0.5
```

```
## Warning: package 'dplyr' was built under R version 4.0.5
```

```
## Warning: package 'forcats' was built under R version 4.0.5
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
theme_set(theme_minimal())

exit <- read_csv("https://raw.githubusercontent.com/jpedroza1228/exitsurveys/main/data/student_experience.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_double(),
##   program = col_character()
## )
## i Use `spec()` for the full column specifications.
```


```r
exit %>% 
  pivot_longer(cols = tidyselect::vars_select(names(exit), starts_with("fac_qual")),
               names_to = "fac_qual", values_to = "fac_values") %>% 
  mutate(fac_qual = recode(fac_qual, "fac_qual_ex" = "Faculty Quality-Ex",
                           "fac_qual_ex_good" = "Faculty Quality-Ex/Good",
                           "fac_qual_fair_poor" = "Faculty Quality-Fair/Poor")) %>% 
  filter(fac_qual != "Faculty Quality-Ex") %>%
  ggplot(aes(fct_reorder(program, fac_values), fac_values)) +
  geom_col(aes(fill = as.factor(year)), position = "dodge2") +
  labs(title = "Student Experiences by Academic Program",
       x = "",
       y = "Specific Student Experience",
       caption = "Ex = Excellent") +
  coord_flip() +
  facet_wrap(~fac_qual) +
  theme(legend.position = "bottom",
        legend.title = element_blank())
```

```
## Warning: Removed 20 rows containing missing values (geom_col).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-1.png" width="672" />

```r
exit %>% 
  pivot_longer(cols = tidyselect::vars_select(names(exit), starts_with("fac_qual")),
               names_to = "fac_qual", values_to = "fac_values") %>% 
  mutate(fac_qual = recode(fac_qual, "fac_qual_ex" = "Faculty Quality-Ex",
                           "fac_qual_ex_good" = "Faculty Quality-Ex/Good",
                           "fac_qual_fair_poor" = "Faculty Quality-Fair/Poor")) %>% 
    filter(fac_qual != "Faculty Quality-Ex") %>%
  ggplot(aes(fct_reorder(program, fac_values), fac_values)) +
  geom_point(aes(color = as.factor(year), shape = as.factor(year)), size = 2) +
  labs(title = "Student Experiences by Academic Program",
       x = "",
       y = "Specific Student Experience",
       caption = "Ex = Excellent") +
  coord_flip() +
  facet_wrap(~fac_qual) +
  scale_color_manual(values = c("#d74122","#669b3e")) +
  theme(legend.position = "bottom",
        legend.title = element_blank())
```

```
## Warning: Removed 20 rows containing missing values (geom_point).
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-1-2.png" width="672" />


```r
program_year_diff <- function(data, x){

    data %>% 
    filter(program == {{name}}) %>% 
  ggplot(data = data, aes(year, student_n)) +
    geom_point(aes(color = program)) +
    geom_line(aes(color = program)) +
    theme_minimal() +
    labs(title = "Comparison of Variable ")
    theme(legend.position = "none")
}

program_year_diff(exit, intel_open_agree)
```





