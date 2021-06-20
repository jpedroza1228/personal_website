---
title: Tidy Tuesday - Coffee Rating
author: Jonathan Pedroza
date: '2021-05-13'
slug: tidy-tuesday-coffee-rating
categories: []
tags: []
subtitle: ''
summary: ''
authors: []
lastmod: '2021-05-13T13:54:15-07:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---


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
coffee <- read_csv('https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2020/2020-07-07/coffee_ratings.csv') %>% 
  mutate(species = as.factor(species))
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   .default = col_character(),
##   total_cup_points = col_double(),
##   number_of_bags = col_double(),
##   aroma = col_double(),
##   flavor = col_double(),
##   aftertaste = col_double(),
##   acidity = col_double(),
##   body = col_double(),
##   balance = col_double(),
##   uniformity = col_double(),
##   clean_cup = col_double(),
##   sweetness = col_double(),
##   cupper_points = col_double(),
##   moisture = col_double(),
##   category_one_defects = col_double(),
##   quakers = col_double(),
##   category_two_defects = col_double(),
##   altitude_low_meters = col_double(),
##   altitude_high_meters = col_double(),
##   altitude_mean_meters = col_double()
## )
## i Use `spec()` for the full column specifications.
```


```r
psych::describe(coffee, na.rm = TRUE)[c("n", "mean", "sd", "min", "max", "skew", "kurtosis")]
```

```
##                           n    mean      sd min       max   skew kurtosis
## total_cup_points       1339   82.09    3.50   0     90.58 -10.42   226.88
## species*               1339    1.02    0.14   1      2.00   6.69    42.77
## owner*                 1332  147.41   83.74   1    315.00   0.12    -1.00
## country_of_origin*     1338   14.89   10.31   1     36.00   0.33    -1.17
## farm_name*              980  296.54  167.74   1    571.00  -0.01    -1.28
## lot_number*             276  103.05   67.38   1    227.00   0.21    -1.27
## mill*                  1024  218.82  134.22   1    460.00   0.23    -1.27
## ico_number*            1188  401.58  271.04   1    847.00   0.09    -1.27
## company*               1130  148.29   82.06   1    281.00  -0.06    -1.25
## altitude*              1113  173.87  110.54   1    396.00   0.32    -1.03
## region*                1280  188.66   96.37   1    356.00  -0.04    -1.10
## producer*              1108  348.55  194.03   1    691.00  -0.02    -1.14
## number_of_bags         1339  154.18  129.99   0   1062.00   0.31     0.21
## bag_weight*            1339   31.14   20.00   1     56.00  -0.35    -1.64
## in_country_partner*    1339   11.03    8.02   1     27.00   0.27    -1.50
## harvest_year*          1292   15.24    4.79   1     46.00   2.32    10.07
## grading_date*          1339  276.93  164.90   1    567.00   0.10    -1.20
## owner_1*               1332  149.87   85.05   1    319.00   0.11    -1.01
## variety*               1113   12.65    9.78   1     29.00   0.62    -1.25
## processing_method*     1169    3.98    1.67   1      5.00  -1.13    -0.62
## aroma                  1339    7.57    0.38   0      8.75  -6.23   120.77
## flavor                 1339    7.52    0.40   0      8.83  -5.18    94.25
## aftertaste             1339    7.40    0.40   0      8.67  -4.78    83.11
## acidity                1339    7.54    0.38   0      8.75  -5.93   115.52
## body                   1339    7.52    0.37   0      8.58  -6.78   129.25
## balance                1339    7.52    0.41   0      8.75  -4.77    85.18
## uniformity             1339    9.83    0.55   0     10.00  -6.95    84.91
## clean_cup              1339    9.84    0.76   0     10.00  -7.43    70.14
## sweetness              1339    9.86    0.62   0     10.00  -7.54    84.88
## cupper_points          1339    7.50    0.47   0     10.00  -2.81    49.44
## moisture               1339    0.09    0.05   0      0.28  -0.99    -0.18
## category_one_defects   1339    0.48    2.55   0     63.00  15.03   307.10
## quakers                1338    0.17    0.83   0     11.00   6.92    58.02
## color*                 1121    2.79    0.64   1      4.00  -1.53     2.52
## category_two_defects   1339    3.56    5.31   0     55.00   3.66    19.97
## expiration*            1339  275.83  164.50   1    566.00   0.11    -1.20
## certification_body*    1339   10.70    7.63   1     26.00   0.24    -1.50
## certification_address* 1339   17.56    8.34   1     32.00   0.03    -1.16
## certification_contact* 1339   11.19    8.06   1     29.00   0.28    -1.12
## unit_of_measurement*   1339    1.86    0.34   1      2.00  -2.12     2.51
## altitude_low_meters    1109 1750.71 8669.44   1 190164.00  20.27   421.25
## altitude_high_meters   1109 1799.35 8668.81   1 190164.00  20.26   420.92
## altitude_mean_meters   1109 1775.03 8668.63   1 190164.00  20.27   421.18
```

```r
summary(coffee)
```

```
##  total_cup_points    species        owner           country_of_origin 
##  Min.   : 0.00    Arabica:1311   Length:1339        Length:1339       
##  1st Qu.:81.08    Robusta:  28   Class :character   Class :character  
##  Median :82.50                   Mode  :character   Mode  :character  
##  Mean   :82.09                                                        
##  3rd Qu.:83.67                                                        
##  Max.   :90.58                                                        
##                                                                       
##   farm_name          lot_number            mill            ico_number       
##  Length:1339        Length:1339        Length:1339        Length:1339       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##    company            altitude            region            producer        
##  Length:1339        Length:1339        Length:1339        Length:1339       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##  number_of_bags    bag_weight        in_country_partner harvest_year      
##  Min.   :   0.0   Length:1339        Length:1339        Length:1339       
##  1st Qu.:  14.0   Class :character   Class :character   Class :character  
##  Median : 175.0   Mode  :character   Mode  :character   Mode  :character  
##  Mean   : 154.2                                                           
##  3rd Qu.: 275.0                                                           
##  Max.   :1062.0                                                           
##                                                                           
##  grading_date         owner_1            variety          processing_method 
##  Length:1339        Length:1339        Length:1339        Length:1339       
##  Class :character   Class :character   Class :character   Class :character  
##  Mode  :character   Mode  :character   Mode  :character   Mode  :character  
##                                                                             
##                                                                             
##                                                                             
##                                                                             
##      aroma           flavor       aftertaste       acidity           body      
##  Min.   :0.000   Min.   :0.00   Min.   :0.000   Min.   :0.000   Min.   :0.000  
##  1st Qu.:7.420   1st Qu.:7.33   1st Qu.:7.250   1st Qu.:7.330   1st Qu.:7.330  
##  Median :7.580   Median :7.58   Median :7.420   Median :7.580   Median :7.500  
##  Mean   :7.567   Mean   :7.52   Mean   :7.401   Mean   :7.536   Mean   :7.517  
##  3rd Qu.:7.750   3rd Qu.:7.75   3rd Qu.:7.580   3rd Qu.:7.750   3rd Qu.:7.670  
##  Max.   :8.750   Max.   :8.83   Max.   :8.670   Max.   :8.750   Max.   :8.580  
##                                                                                
##     balance        uniformity       clean_cup        sweetness     
##  Min.   :0.000   Min.   : 0.000   Min.   : 0.000   Min.   : 0.000  
##  1st Qu.:7.330   1st Qu.:10.000   1st Qu.:10.000   1st Qu.:10.000  
##  Median :7.500   Median :10.000   Median :10.000   Median :10.000  
##  Mean   :7.518   Mean   : 9.835   Mean   : 9.835   Mean   : 9.857  
##  3rd Qu.:7.750   3rd Qu.:10.000   3rd Qu.:10.000   3rd Qu.:10.000  
##  Max.   :8.750   Max.   :10.000   Max.   :10.000   Max.   :10.000  
##                                                                    
##  cupper_points       moisture       category_one_defects    quakers       
##  Min.   : 0.000   Min.   :0.00000   Min.   : 0.0000      Min.   : 0.0000  
##  1st Qu.: 7.250   1st Qu.:0.09000   1st Qu.: 0.0000      1st Qu.: 0.0000  
##  Median : 7.500   Median :0.11000   Median : 0.0000      Median : 0.0000  
##  Mean   : 7.503   Mean   :0.08838   Mean   : 0.4795      Mean   : 0.1734  
##  3rd Qu.: 7.750   3rd Qu.:0.12000   3rd Qu.: 0.0000      3rd Qu.: 0.0000  
##  Max.   :10.000   Max.   :0.28000   Max.   :63.0000      Max.   :11.0000  
##                                                          NA's   :1        
##     color           category_two_defects  expiration        certification_body
##  Length:1339        Min.   : 0.000       Length:1339        Length:1339       
##  Class :character   1st Qu.: 0.000       Class :character   Class :character  
##  Mode  :character   Median : 2.000       Mode  :character   Mode  :character  
##                     Mean   : 3.556                                            
##                     3rd Qu.: 4.000                                            
##                     Max.   :55.000                                            
##                                                                               
##  certification_address certification_contact unit_of_measurement
##  Length:1339           Length:1339           Length:1339        
##  Class :character      Class :character      Class :character   
##  Mode  :character      Mode  :character      Mode  :character   
##                                                                 
##                                                                 
##                                                                 
##                                                                 
##  altitude_low_meters altitude_high_meters altitude_mean_meters
##  Min.   :     1      Min.   :     1       Min.   :     1      
##  1st Qu.:  1100      1st Qu.:  1100       1st Qu.:  1100      
##  Median :  1311      Median :  1350       Median :  1311      
##  Mean   :  1751      Mean   :  1799       Mean   :  1775      
##  3rd Qu.:  1600      3rd Qu.:  1650       3rd Qu.:  1600      
##  Max.   :190164      Max.   :190164       Max.   :190164      
##  NA's   :230         NA's   :230          NA's   :230
```

```r
coffee %>% 
  group_by(species) %>% 
  summarize(n = n(),
            prop = n/1339)
```

```
## # A tibble: 2 x 3
##   species     n   prop
##   <fct>   <int>  <dbl>
## 1 Arabica  1311 0.979 
## 2 Robusta    28 0.0209
```


```r
library(tidymodels)
```

```
## -- Attaching packages -------------------------------------- tidymodels 0.1.1 --
```

```
## v broom     0.7.6      v recipes   0.1.14
## v dials     0.0.9      v rsample   0.0.8 
## v infer     0.5.3      v tune      0.1.1 
## v modeldata 0.1.0      v workflows 0.2.1 
## v parsnip   0.1.4      v yardstick 0.0.7
```

```
## Warning: package 'broom' was built under R version 4.0.5
```

```
## -- Conflicts ----------------------------------------- tidymodels_conflicts() --
## x scales::discard() masks purrr::discard()
## x dplyr::filter()   masks stats::filter()
## x recipes::fixed()  masks stringr::fixed()
## x dplyr::lag()      masks stats::lag()
## x yardstick::spec() masks readr::spec()
## x recipes::step()   masks stats::step()
```

```r
set.seed(05132021)

coffee_split <- initial_split(coffee, strata = "total_cup_points")

coffee_train <- training(coffee_split)
coffee_test <- training(coffee_split)
```


```r
set.seed(05132021)

coffee_fold <- vfold_cv(coffee_train, strata = "total_cup_points", v = 10)
```


```r
set.seed(05132021)

char_recipe <- recipe(total_cup_points ~ aroma + flavor + aftertaste + acidity + body + balance + uniformity + clean_cup + sweetness, data = coffee_train) %>% 
  step_zv(all_predictors()) %>% 
  step_nzv(all_predictors())
```


```r
set.seed(05132021)

lr_mod <- linear_reg()  %>%
  set_engine("glmnet") %>% 
  set_mode("regression") %>%  
  set_args(penalty = 0,
           mixture = 0)

lr_flo <- workflow() %>% 
  add_recipe(char_recipe) %>% 
  add_model(lr_mod)

lr_fit <- tune::fit_resamples(object = lr_flo,
                    resamples = coffee_fold,
                    control = control_resamples(verbose = TRUE,
                                                save_pred = TRUE))
```

```
## i Fold01: recipe
```

```
## v Fold01: recipe
```

```
## i Fold01: model
```

```
## v Fold01: model
```

```
## i Fold01: model (predictions)
```

```
## i Fold02: recipe
```

```
## v Fold02: recipe
```

```
## i Fold02: model
```

```
## v Fold02: model
```

```
## i Fold02: model (predictions)
```

```
## i Fold03: recipe
```

```
## v Fold03: recipe
```

```
## i Fold03: model
```

```
## v Fold03: model
```

```
## i Fold03: model (predictions)
```

```
## i Fold04: recipe
```

```
## v Fold04: recipe
```

```
## i Fold04: model
```

```
## v Fold04: model
```

```
## i Fold04: model (predictions)
```

```
## i Fold05: recipe
```

```
## v Fold05: recipe
```

```
## i Fold05: model
```

```
## v Fold05: model
```

```
## i Fold05: model (predictions)
```

```
## i Fold06: recipe
```

```
## v Fold06: recipe
```

```
## i Fold06: model
```

```
## v Fold06: model
```

```
## i Fold06: model (predictions)
```

```
## i Fold07: recipe
```

```
## v Fold07: recipe
```

```
## i Fold07: model
```

```
## v Fold07: model
```

```
## i Fold07: model (predictions)
```

```
## i Fold08: recipe
```

```
## v Fold08: recipe
```

```
## i Fold08: model
```

```
## v Fold08: model
```

```
## i Fold08: model (predictions)
```

```
## i Fold09: recipe
```

```
## v Fold09: recipe
```

```
## i Fold09: model
```

```
## v Fold09: model
```

```
## i Fold09: model (predictions)
```

```
## i Fold10: recipe
```

```
## v Fold10: recipe
```

```
## i Fold10: model
```

```
## v Fold10: model
```

```
## i Fold10: model (predictions)
```

```r
lr_fit %>% 
  collect_metrics()
```

```
## # A tibble: 2 x 5
##   .metric .estimator  mean     n std_err
##   <chr>   <chr>      <dbl> <int>   <dbl>
## 1 rmse    standard   0.936    10  0.133 
## 2 rsq     standard   0.899    10  0.0248
```

```r
lr_fit %>% 
  collect_metrics(summarize = FALSE)
```

```
## # A tibble: 20 x 4
##    id     .metric .estimator .estimate
##    <chr>  <chr>   <chr>          <dbl>
##  1 Fold01 rmse    standard       0.394
##  2 Fold01 rsq     standard       0.976
##  3 Fold02 rmse    standard       0.834
##  4 Fold02 rsq     standard       0.937
##  5 Fold03 rmse    standard       0.927
##  6 Fold03 rsq     standard       0.856
##  7 Fold04 rmse    standard       1.33 
##  8 Fold04 rsq     standard       0.987
##  9 Fold05 rmse    standard       1.22 
## 10 Fold05 rsq     standard       0.822
## 11 Fold06 rmse    standard       1.73 
## 12 Fold06 rsq     standard       0.779
## 13 Fold07 rmse    standard       1.15 
## 14 Fold07 rsq     standard       0.797
## 15 Fold08 rmse    standard       0.537
## 16 Fold08 rsq     standard       0.940
## 17 Fold09 rmse    standard       0.531
## 18 Fold09 rsq     standard       0.972
## 19 Fold10 rmse    standard       0.701
## 20 Fold10 rsq     standard       0.920
```


```r
set.seed(05132021)

lasso_mod <- linear_reg()  %>%
  set_engine("glmnet") %>% 
  set_mode("regression") %>% 
  set_args(penalty = 0,
           mixture = 1)

lasso_flo <- lr_flo %>% 
  update_model(lasso_mod) 

lasso_fit <- tune::fit_resamples(object = lasso_flo,
                    resamples = coffee_fold,
                    metrics = metric_set(rmse),
                    control = control_resamples(verbose = TRUE,
                                                save_pred = TRUE))
```

```
## i Fold01: recipe
```

```
## v Fold01: recipe
```

```
## i Fold01: model
```

```
## v Fold01: model
```

```
## i Fold01: model (predictions)
```

```
## i Fold02: recipe
```

```
## v Fold02: recipe
```

```
## i Fold02: model
```

```
## v Fold02: model
```

```
## i Fold02: model (predictions)
```

```
## i Fold03: recipe
```

```
## v Fold03: recipe
```

```
## i Fold03: model
```

```
## v Fold03: model
```

```
## i Fold03: model (predictions)
```

```
## i Fold04: recipe
```

```
## v Fold04: recipe
```

```
## i Fold04: model
```

```
## v Fold04: model
```

```
## i Fold04: model (predictions)
```

```
## i Fold05: recipe
```

```
## v Fold05: recipe
```

```
## i Fold05: model
```

```
## v Fold05: model
```

```
## i Fold05: model (predictions)
```

```
## i Fold06: recipe
```

```
## v Fold06: recipe
```

```
## i Fold06: model
```

```
## v Fold06: model
```

```
## i Fold06: model (predictions)
```

```
## i Fold07: recipe
```

```
## v Fold07: recipe
```

```
## i Fold07: model
```

```
## v Fold07: model
```

```
## i Fold07: model (predictions)
```

```
## i Fold08: recipe
```

```
## v Fold08: recipe
```

```
## i Fold08: model
```

```
## v Fold08: model
```

```
## i Fold08: model (predictions)
```

```
## i Fold09: recipe
```

```
## v Fold09: recipe
```

```
## i Fold09: model
```

```
## v Fold09: model
```

```
## i Fold09: model (predictions)
```

```
## i Fold10: recipe
```

```
## v Fold10: recipe
```

```
## i Fold10: model
```

```
## v Fold10: model
```

```
## i Fold10: model (predictions)
```

```r
lasso_fit %>% 
  collect_metrics()
```

```
## # A tibble: 1 x 5
##   .metric .estimator  mean     n std_err
##   <chr>   <chr>      <dbl> <int>   <dbl>
## 1 rmse    standard   0.935    10   0.125
```

```r
lasso_fit %>% 
  collect_metrics(summarize = FALSE)
```

```
## # A tibble: 10 x 4
##    id     .metric .estimator .estimate
##    <chr>  <chr>   <chr>          <dbl>
##  1 Fold01 rmse    standard       0.407
##  2 Fold02 rmse    standard       0.807
##  3 Fold03 rmse    standard       0.930
##  4 Fold04 rmse    standard       1.25 
##  5 Fold05 rmse    standard       1.21 
##  6 Fold06 rmse    standard       1.69 
##  7 Fold07 rmse    standard       1.18 
##  8 Fold08 rmse    standard       0.568
##  9 Fold09 rmse    standard       0.590
## 10 Fold10 rmse    standard       0.720
```


```r
set.seed(05132021)

elastic_tune_mod <- linear_reg()  %>%
  set_engine("glmnet") %>% 
  set_mode("regression") %>% 
  set_args(penalty = tune(),
           mixture = tune())

elastic_tune_flo <- lr_flo %>% 
  update_model(elastic_tune_mod) 

elastic_grid <- grid_regular(penalty(), mixture(), levels = 10)

elastic_fit <- tune_grid(elastic_tune_flo,
                          resamples = coffee_fold,
                          grid = elastic_grid,
                    metrics = metric_set(rmse),
                           control = tune::control_resamples(save_pred = TRUE))

elastic_fit %>% 
  collect_metrics(summarize = FALSE)
```

```
## # A tibble: 1,000 x 7
##    id           penalty mixture .metric .estimator .estimate .config 
##    <chr>          <dbl>   <dbl> <chr>   <chr>          <dbl> <chr>   
##  1 Fold01 0.0000000001        0 rmse    standard       0.394 Model001
##  2 Fold01 0.00000000129       0 rmse    standard       0.394 Model002
##  3 Fold01 0.0000000167        0 rmse    standard       0.394 Model003
##  4 Fold01 0.000000215         0 rmse    standard       0.394 Model004
##  5 Fold01 0.00000278          0 rmse    standard       0.394 Model005
##  6 Fold01 0.0000359           0 rmse    standard       0.394 Model006
##  7 Fold01 0.000464            0 rmse    standard       0.394 Model007
##  8 Fold01 0.00599             0 rmse    standard       0.394 Model008
##  9 Fold01 0.0774              0 rmse    standard       0.394 Model009
## 10 Fold01 1                   0 rmse    standard       0.401 Model010
## # ... with 990 more rows
```

```r
elastic_fit %>% 
  show_best(metric = "rmse", n = 5)
```

```
## # A tibble: 5 x 8
##         penalty mixture .metric .estimator  mean     n std_err .config 
##           <dbl>   <dbl> <chr>   <chr>      <dbl> <int>   <dbl> <chr>   
## 1 0.0000000001    0.111 rmse    standard   0.933    10   0.125 Model011
## 2 0.00000000129   0.111 rmse    standard   0.933    10   0.125 Model012
## 3 0.0000000167    0.111 rmse    standard   0.933    10   0.125 Model013
## 4 0.000000215     0.111 rmse    standard   0.933    10   0.125 Model014
## 5 0.00000278      0.111 rmse    standard   0.933    10   0.125 Model015
```

```r
elastic_fit %>% 
  select_best(metric = "rmse")
```

```
## # A tibble: 1 x 3
##        penalty mixture .config 
##          <dbl>   <dbl> <chr>   
## 1 0.0000000001   0.111 Model011
```

```r
elastic_fit %>% 
  collect_metrics() %>% 
  ggplot(aes(penalty, mean, color = .metric)) +
  geom_errorbar(aes(ymin = mean - std_err,
                    ymax = mean + std_err),
                alpha = .5) +
  geom_line(size = 1.25) 
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-1.png" width="672" />

```r
autoplot(elastic_fit, metric = "rmse") + geom_smooth(se = FALSE)
```

```
## `geom_smooth()` using method = 'loess' and formula 'y ~ x'
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-2.png" width="672" />

```r
library(vip)
```

```
## 
## Attaching package: 'vip'
```

```
## The following object is masked from 'package:utils':
## 
##     vi
```

```r
elastic_train_best_fit <- elastic_fit %>%
  select_best(metric = "rmse")

final_workflow <- finalize_workflow(elastic_tune_flo, elastic_train_best_fit)

final_workflow %>%
  fit(coffee_train) %>%
  pull_workflow_fit() %>%
  vi(lambda = elastic_train_best_fit$penalty) %>%
  mutate(
    importance = abs(Importance),
    variable = fct_reorder(Variable, importance)
  ) %>%
  ggplot(aes(x = importance, y = variable, fill = Sign)) +
  geom_col() +
  scale_x_continuous(expand = c(0, 0)) +
  labs(y = NULL)
```

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-8-3.png" width="672" />


```r
set.seed(05132021)

test_set_model_results <- last_fit(final_workflow,
                                   split = coffee_split)

test_set_model_results %>%
  collect_metrics()
```

```
## # A tibble: 2 x 3
##   .metric .estimator .estimate
##   <chr>   <chr>          <dbl>
## 1 rmse    standard       0.920
## 2 rsq     standard       0.877
```



