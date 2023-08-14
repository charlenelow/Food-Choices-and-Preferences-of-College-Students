Food Choices and Preference of College Students
================
Charlene
2023-08-09

## Loading readr package

Dataset used for this project was imported using readr package. To do
so, the tidyverse package which contains readr package was installed and
loaded.

## Importing CSV file

## Data cleaning

#### Preview dataset

Packages required in this step: Here, Skimr, Janitor, dply.

``` r
head(food_survey_respond_df)
```

    ## # A tibble: 6 × 61
    ##   GPA   Gender breakfast calories_chicken calories_day calories_scone coffee
    ##   <chr>  <dbl>     <dbl>            <dbl>        <dbl>          <dbl>  <dbl>
    ## 1 2.4        2         1              430          NaN            315      1
    ## 2 3.654      1         1              610            3            420      2
    ## 3 3.3        1         1              720            4            420      2
    ## 4 3.2        1         1              430            3            420      2
    ## 5 3.5        1         1              720            2            420      2
    ## 6 2.25       1         1              610            3            980      2
    ## # ℹ 54 more variables: comfort_food <chr>, comfort_food_reasons <chr>,
    ## #   comfort_food_reasons_coded...10 <dbl>, cook <dbl>,
    ## #   comfort_food_reasons_coded...12 <dbl>, cuisine <dbl>, diet_current <chr>,
    ## #   diet_current_coded <dbl>, drink <dbl>, eating_changes <chr>,
    ## #   eating_changes_coded <dbl>, eating_changes_coded1 <dbl>, eating_out <dbl>,
    ## #   employment <dbl>, ethnic_food <dbl>, exercise <dbl>,
    ## #   father_education <dbl>, father_profession <chr>, fav_cuisine <chr>, …

``` r
dplyr::glimpse(food_survey_respond_df)
```

    ## Rows: 125
    ## Columns: 61
    ## $ GPA                             <chr> "2.4", "3.654", "3.3", "3.2", "3.5", "…
    ## $ Gender                          <dbl> 2, 1, 1, 1, 1, 1, 2, 1, 1, 1, 1, 1, 2,…
    ## $ breakfast                       <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    ## $ calories_chicken                <dbl> 430, 610, 720, 430, 720, 610, 610, 720…
    ## $ calories_day                    <dbl> NaN, 3, 4, 3, 2, 3, 3, 3, NaN, 3, 3, 4…
    ## $ calories_scone                  <dbl> 315, 420, 420, 420, 420, 980, 420, 420…
    ## $ coffee                          <dbl> 1, 2, 2, 2, 2, 2, 2, 1, 1, 2, 2, 2, 2,…
    ## $ comfort_food                    <chr> "none", "chocolate, chips, ice cream",…
    ## $ comfort_food_reasons            <chr> "we dont have comfort", "Stress, bored…
    ## $ comfort_food_reasons_coded...10 <dbl> 9, 1, 1, 2, 1, 4, 1, 1, 2, 1, 2, 3, 3,…
    ## $ cook                            <dbl> 2, 3, 1, 2, 1, 3, 2, 3, 3, 3, 1, 3, 5,…
    ## $ comfort_food_reasons_coded...12 <dbl> 9, 1, 1, 2, 1, 4, 1, 1, 2, 1, 2, 3, 3,…
    ## $ cuisine                         <dbl> NaN, 1, 3, 2, 2, NaN, 1, 1, 1, 1, 1, 1…
    ## $ diet_current                    <chr> "eat good and exercise", "I eat about …
    ## $ diet_current_coded              <dbl> 1, 2, 3, 2, 2, 2, 3, 1, 1, 1, 1, 1, 1,…
    ## $ drink                           <dbl> 1, 2, 1, 2, 2, 2, 1, 2, 1, 1, 2, 1, 2,…
    ## $ eating_changes                  <chr> "eat faster", "I eat out more than usu…
    ## $ eating_changes_coded            <dbl> 1, 1, 1, 1, 3, 1, 2, 2, 2, 1, 3, 4, 2,…
    ## $ eating_changes_coded1           <dbl> 1, 2, 3, 3, 4, 3, 5, 5, 8, 3, 4, 5, 5,…
    ## $ eating_out                      <dbl> 3, 2, 2, 2, 2, 1, 2, 2, 5, 3, 2, 1, 1,…
    ## $ employment                      <dbl> 3, 2, 3, 3, 2, 3, 3, 2, 2, 3, 1, 2, 3,…
    ## $ ethnic_food                     <dbl> 1, 4, 5, 5, 4, 4, 5, 2, 5, 5, 5, 5, 4,…
    ## $ exercise                        <dbl> 1, 1, 2, 3, 1, 2, 1, 2, NaN, 1, 1, 1, …
    ## $ father_education                <dbl> 5, 2, 2, 2, 4, 1, 4, 3, 5, 5, 2, 3, 3,…
    ## $ father_profession               <chr> "profesor", "Self employed", "owns bus…
    ## $ fav_cuisine                     <chr> "Arabic cuisine", "Italian", "italian"…
    ## $ fav_cuisine_coded               <dbl> 3, 1, 1, 3, 1, 6, 4, 5, 1, 1, 4, 1, 4,…
    ## $ fav_food                        <dbl> 1, 1, 3, 1, 3, 3, 1, 1, 3, 1, 1, 1, 3,…
    ## $ food_childhood                  <chr> "rice  and chicken", "chicken and bisc…
    ## $ fries                           <dbl> 2, 1, 1, 2, 1, 1, 1, 1, 1, 1, 1, 1, 1,…
    ## $ fruit_day                       <dbl> 5, 4, 5, 4, 4, 2, 4, 5, 4, 5, 5, 5, 4,…
    ## $ grade_level                     <dbl> 2, 4, 3, 4, 4, 2, 4, 2, 1, 1, 3, 2, 1,…
    ## $ greek_food                      <dbl> 5, 4, 5, 5, 4, 2, 5, 3, 5, 5, 1, 5, 3,…
    ## $ healthy_feeling                 <dbl> 2, 5, 6, 7, 6, 4, 4, 3, 7, 3, 9, 1, 9,…
    ## $ healthy_meal                    <chr> "looks not oily", "Grains, Veggies, (m…
    ## $ ideal_diet                      <chr> "being healthy", "Try to eat 5-6 small…
    ## $ ideal_diet_coded                <dbl> 8, 3, 6, 2, 2, 2, 2, 2, 6, 2, 7, 2, 1,…
    ## $ income                          <dbl> 5, 4, 6, 6, 6, 1, 4, 5, 5, 4, 3, 5, 5,…
    ## $ indian_food                     <dbl> 5, 4, 5, 5, 2, 5, 5, 1, 5, 4, 1, 5, 3,…
    ## $ italian_food                    <dbl> 5, 4, 5, 5, 5, 5, 5, 3, 5, 5, 5, 5, 4,…
    ## $ life_rewarding                  <dbl> 1, 1, 7, 2, 1, 4, 8, 3, 8, 3, 8, 1, 9,…
    ## $ marital_status                  <dbl> 1, 2, 2, 2, 1, 2, 1, 1, 2, 2, 1, 2, 2,…
    ## $ meals_dinner_friend             <chr> "rice, chicken,  soup", "Pasta, steak,…
    ## $ mother_education                <dbl> 1, 4, 2, 4, 5, 1, 4, 2, 5, 5, 4, 4, 4,…
    ## $ mother_profession               <chr> "unemployed", "Nurse RN", "owns busine…
    ## $ nutritional_check               <dbl> 5, 4, 4, 2, 3, 1, 4, 4, 2, 5, 2, 5, 2,…
    ## $ on_off_campus                   <dbl> 1, 1, 2, 1, 1, 1, 2, 1, 1, 1, 3, 1, 1,…
    ## $ parents_cook                    <dbl> 1, 1, 1, 1, 1, 2, 2, 1, 2, 3, 1, 1, 2,…
    ## $ pay_meal_out                    <dbl> 2, 4, 3, 2, 4, 5, 2, 5, 3, 3, 2, 3, 2,…
    ## $ persian_food                    <dbl> 5, 4, 5, 5, 2, 5, 5, 1, 5, 4, 2, 5, 3,…
    ## $ self_perception_weight          <dbl> 3, 3, 6, 5, 4, 5, 4, 3, 4, 3, 1, 2, 5,…
    ## $ soup                            <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 2,…
    ## $ sports                          <dbl> 1, 1, 2, 2, 1, 2, 1, 2, 2, 1, 1, 1, 1,…
    ## $ thai_food                       <dbl> 1, 2, 5, 5, 4, 4, 5, 1, 5, 4, 2, 5, 3,…
    ## $ tortilla_calories               <dbl> 1165, 725, 1165, 725, 940, 940, 940, 7…
    ## $ turkey_calories                 <dbl> 345, 690, 500, 690, 500, 345, 690, 500…
    ## $ type_sports                     <chr> "car racing", "Basketball", "none", "n…
    ## $ veggies_day                     <dbl> 5, 4, 5, 3, 4, 1, 4, 4, 3, 5, 5, 5, 3,…
    ## $ vitamins                        <dbl> 1, 2, 1, 1, 2, 2, 1, 2, 2, 1, 2, 1, 2,…
    ## $ waffle_calories                 <dbl> 1315, 900, 900, 1315, 760, 1315, 1315,…
    ## $ weight                          <chr> "187", "155", "I'm not answering this.…

``` r
colnames(food_survey_respond_df)
```

    ##  [1] "GPA"                             "Gender"                         
    ##  [3] "breakfast"                       "calories_chicken"               
    ##  [5] "calories_day"                    "calories_scone"                 
    ##  [7] "coffee"                          "comfort_food"                   
    ##  [9] "comfort_food_reasons"            "comfort_food_reasons_coded...10"
    ## [11] "cook"                            "comfort_food_reasons_coded...12"
    ## [13] "cuisine"                         "diet_current"                   
    ## [15] "diet_current_coded"              "drink"                          
    ## [17] "eating_changes"                  "eating_changes_coded"           
    ## [19] "eating_changes_coded1"           "eating_out"                     
    ## [21] "employment"                      "ethnic_food"                    
    ## [23] "exercise"                        "father_education"               
    ## [25] "father_profession"               "fav_cuisine"                    
    ## [27] "fav_cuisine_coded"               "fav_food"                       
    ## [29] "food_childhood"                  "fries"                          
    ## [31] "fruit_day"                       "grade_level"                    
    ## [33] "greek_food"                      "healthy_feeling"                
    ## [35] "healthy_meal"                    "ideal_diet"                     
    ## [37] "ideal_diet_coded"                "income"                         
    ## [39] "indian_food"                     "italian_food"                   
    ## [41] "life_rewarding"                  "marital_status"                 
    ## [43] "meals_dinner_friend"             "mother_education"               
    ## [45] "mother_profession"               "nutritional_check"              
    ## [47] "on_off_campus"                   "parents_cook"                   
    ## [49] "pay_meal_out"                    "persian_food"                   
    ## [51] "self_perception_weight"          "soup"                           
    ## [53] "sports"                          "thai_food"                      
    ## [55] "tortilla_calories"               "turkey_calories"                
    ## [57] "type_sports"                     "veggies_day"                    
    ## [59] "vitamins"                        "waffle_calories"                
    ## [61] "weight"

## Data Transformation

In this part of the analysis, 3 new dataframes will be created with
variables of interest that were required to answer the following
questions:

- Question 1: Does exercising regularly affects weight of an individual?

- Question 2: Does factors such as: Employment, Income, and Living on or
  off campus affect the frequency of eating out for college students?

- Question 3: Does students who exercise regularly more likely to make
  better food choices?

#### Question 1: Creating new dataframe with variables of interest

In the preview of the food_survey_respond_df, there are 61 variables in
this dataset. Not all the variables will be needed in our analysis,
therefore, only the variables of interest will be selected and stored in
a new dataframe for easy access later.

``` r
library(tidyr)
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
weight_df<- food_survey_respond_df %>% 
  select("Gender","exercise","weight") %>% 
  drop_na()

weight_df %>% 
  count(weight) # to identify which responds needs cleaning / removing
```

    ## # A tibble: 42 × 2
    ##    weight     n
    ##    <chr>  <int>
    ##  1 110        1
    ##  2 112        1
    ##  3 115        1
    ##  4 116        1
    ##  5 118        1
    ##  6 120        3
    ##  7 123        1
    ##  8 125        4
    ##  9 128        2
    ## 10 129        2
    ## # ℹ 32 more rows

``` r
weight_df %>% 
  count(Gender) # should have 1 & 2 only. 1= Female, 2 = Male
```

    ## # A tibble: 2 × 2
    ##   Gender     n
    ##    <dbl> <int>
    ## 1      1    65
    ## 2      2    47

``` r
weight_df %>% 
  count(exercise)
```

    ## # A tibble: 3 × 2
    ##   exercise     n
    ##      <dbl> <int>
    ## 1        1    57
    ## 2        2    44
    ## 3        3    11

There are 4 rows in weight that needs cleaning before we can start
analysis.

``` r
library(stringr)
weight_df$weight <- str_replace_all(weight_df$weight, "^144 lbs$", "144")
weight_df$weight <- str_replace_all(weight_df$weight, "^Not sure, 240$", "240")

#Removing Row 3 & row 66
weight_df<- weight_df[-c(3,66),]

#Double checking the data within weight to make sure we have cleaned up properly
weight_df %>% 
  count(weight)
```

    ## # A tibble: 40 × 2
    ##    weight     n
    ##    <chr>  <int>
    ##  1 110        1
    ##  2 112        1
    ##  3 115        1
    ##  4 116        1
    ##  5 118        1
    ##  6 120        3
    ##  7 123        1
    ##  8 125        4
    ##  9 128        2
    ## 10 129        2
    ## # ℹ 30 more rows

#### Question 1: Replace Integer respond for Gender with String

``` r
weight_df <- weight_df %>% 
  mutate(Gender_new=case_match(
           Gender,
           1~'Female',
           2~'Male'
         )
         )

weight_df %>% 
  count(Gender, Gender_new)
```

    ## # A tibble: 2 × 3
    ##   Gender Gender_new     n
    ##    <dbl> <chr>      <int>
    ## 1      1 Female        64
    ## 2      2 Male          46

#### Question 1: Replace Integer respond for exercise with String

``` r
weight_df <- weight_df %>% 
  mutate(exercise_new=case_match(
           exercise,
           1~"Everyday",
           2~"2-3 times a week",
           3~"Once a week",
           4~"Sometimes",
           5~"Never"
         ) 
         )

weight_df %>% 
  count(exercise_new, exercise)  
```

    ## # A tibble: 3 × 3
    ##   exercise_new     exercise     n
    ##   <chr>               <dbl> <int>
    ## 1 2-3 times a week        2    42
    ## 2 Everyday                1    57
    ## 3 Once a week             3    11

#### Question 1: Replace Integer respond for weight with String

``` r
weight_df <- weight_df %>% 
   mutate(weight_range = case_when(
     weight <130 ~'110 - 129 lbs',
     weight <160 ~ '130 - 159 lbs',
     weight < 190 ~'160 - 189 lbs',
     TRUE ~ '>=190 lbs'
     )
     )
weight_df %>% 
  count(weight_range, weight)
```

    ## # A tibble: 40 × 3
    ##    weight_range  weight     n
    ##    <chr>         <chr>  <int>
    ##  1 110 - 129 lbs 110        1
    ##  2 110 - 129 lbs 112        1
    ##  3 110 - 129 lbs 115        1
    ##  4 110 - 129 lbs 116        1
    ##  5 110 - 129 lbs 118        1
    ##  6 110 - 129 lbs 120        3
    ##  7 110 - 129 lbs 123        1
    ##  8 110 - 129 lbs 125        4
    ##  9 110 - 129 lbs 128        2
    ## 10 110 - 129 lbs 129        2
    ## # ℹ 30 more rows

#### Question 2: Creating new dataframe with variables of interest

``` r
frequency_df <- food_survey_respond_df %>% 
  select ("eating_out","employment","income","on_off_campus") %>% 
  drop_na()

glimpse(frequency_df)
```

    ## Rows: 115
    ## Columns: 4
    ## $ eating_out    <dbl> 3, 2, 2, 2, 2, 1, 2, 2, 5, 3, 2, 1, 1, 4, 2, 4, 1, 2, 3,…
    ## $ employment    <dbl> 3, 2, 3, 3, 2, 3, 3, 2, 2, 3, 1, 2, 3, 2, 3, 3, 2, 3, 2,…
    ## $ income        <dbl> 5, 4, 6, 6, 6, 1, 4, 5, 5, 4, 3, 5, 5, 5, 5, 4, 1, 6, 5,…
    ## $ on_off_campus <dbl> 1, 1, 2, 1, 1, 1, 2, 1, 1, 1, 3, 1, 1, 2, 2, 1, 1, 1, 1,…

#### Question 2: Replace Integer respond for eating_out with String

``` r
frequency_df <- frequency_df %>% 
  mutate(eating_out_new= case_match(
    eating_out,
    1 ~ "Never",
    2 ~ "1-2 times",
    3 ~ "2-3 times",
    4 ~ "3-4 times",
    5 ~ "Everyday"
  )
  )
frequency_df %>% 
  count(eating_out_new, eating_out) # checking if above code has been run correctly
```

    ## # A tibble: 5 × 3
    ##   eating_out_new eating_out     n
    ##   <chr>               <dbl> <int>
    ## 1 1-2 times               2    56
    ## 2 2-3 times               3    21
    ## 3 3-4 times               4    13
    ## 4 Everyday                5    10
    ## 5 Never                   1    15

#### Question 2: Replace Integer respond for employment with String

``` r
frequency_df <- frequency_df %>% 
  mutate(employment_new = case_match(
    employment,
    1 ~ "Full time",
    2 ~ "Part time",
    3 ~ "Unemployed"
  )
  )
frequency_df %>% 
  count(employment_new, employment)
```

    ## # A tibble: 3 × 3
    ##   employment_new employment     n
    ##   <chr>               <dbl> <int>
    ## 1 Full time               1     2
    ## 2 Part time               2    60
    ## 3 Unemployed              3    53

#### Question 2: Replace Integer respond for income with String

``` r
frequency_df <- frequency_df %>% 
  mutate(income_range = case_match(
    income,
    1 ~ "less than $15K",
    2 ~ ">$15K - $30K",
    3 ~ ">$30K - $50K",
    4 ~ ">$50K - $70K",
    5 ~ ">$70K - $100K",
    6 ~ "more than $100K"
  )
  )

frequency_df %>% 
  count(income, income_range)
```

    ## # A tibble: 6 × 3
    ##   income income_range        n
    ##    <dbl> <chr>           <int>
    ## 1      1 less than $15K      4
    ## 2      2 >$15K - $30K        7
    ## 3      3 >$30K - $50K       14
    ## 4      4 >$50K - $70K       19
    ## 5      5 >$70K - $100K      32
    ## 6      6 more than $100K    39

#### Question 2: Replace Integer respond for living on and off campus with String

``` r
frequency_df <- frequency_df %>% 
  mutate(living_on_off_campus = case_when(
    on_off_campus == 1 ~ "On campus",
    TRUE ~ "Off campus"
  )
  ) 

frequency_df %>% 
  count(on_off_campus, living_on_off_campus)
```

    ## # A tibble: 4 × 3
    ##   on_off_campus living_on_off_campus     n
    ##           <dbl> <chr>                <int>
    ## 1             1 On campus               90
    ## 2             2 Off campus              15
    ## 3             3 Off campus               8
    ## 4             4 Off campus               2

#### Question 3: Creating new dataframe with variables of interest

``` r
exercise_df <- food_survey_respond_df %>% 
  select ("exercise","nutritional_check","veggies_day","fruit_day") %>% 
  drop_na()

glimpse(exercise_df)
```

    ## Rows: 112
    ## Columns: 4
    ## $ exercise          <dbl> 1, 1, 2, 3, 1, 2, 1, 2, 1, 1, 1, 3, 2, 2, 1, 2, 1, 3…
    ## $ nutritional_check <dbl> 5, 4, 4, 2, 3, 1, 4, 4, 5, 2, 5, 2, 2, 2, 1, 4, 4, 2…
    ## $ veggies_day       <dbl> 5, 4, 5, 3, 4, 1, 4, 4, 5, 5, 5, 3, 5, 5, 1, 5, 4, 5…
    ## $ fruit_day         <dbl> 5, 4, 5, 4, 4, 2, 4, 5, 5, 5, 5, 4, 5, 5, 3, 5, 3, 5…

#### Question 3: Replace Integer respond for exercise with String

``` r
exercise_df <- exercise_df %>% 
  mutate(exercise_new = case_match(
    exercise,
    1 ~ "Everyday",
    2 ~ "2-3 times a week",
    3 ~ "Once a week",
    4 ~ "Sometimes",
    5 ~ "Never"
  )
  ) 

exercise_df %>% 
  count(exercise, exercise_new)
```

    ## # A tibble: 3 × 3
    ##   exercise exercise_new         n
    ##      <dbl> <chr>            <int>
    ## 1        1 Everyday            57
    ## 2        2 2-3 times a week    44
    ## 3        3 Once a week         11

#### Question 3: Replace Integer respond for Nutritional check with String

``` r
exercise_df <- exercise_df %>% 
  mutate(nutritional_check_new = case_match(
    nutritional_check,
    1 ~ "Never",
    2 ~ "On certain products",
    3 ~ "Very rarely",
    4 ~ "On most products",
    5 ~ "On everything"
  )
  )

exercise_df %>% 
  count(nutritional_check,nutritional_check_new)
```

    ## # A tibble: 5 × 3
    ##   nutritional_check nutritional_check_new     n
    ##               <dbl> <chr>                 <int>
    ## 1                 1 Never                     8
    ## 2                 2 On certain products      30
    ## 3                 3 Very rarely              18
    ## 4                 4 On most products         40
    ## 5                 5 On everything            16

#### Question 3: Replace Integer respond for veggie consumption with String

``` r
exercise_df <- rename(exercise_df,"veggie_consumption" = "veggies_day") %>%
  mutate(veggie_consumption_new = case_match(
    veggie_consumption,
    1 ~ "Very unlikely",
    2 ~ "Unlikely",
    3 ~ "Neutral",
    4 ~ "Likely",
    5 ~ "Very likely"
  )
  )

exercise_df %>% 
  count(veggie_consumption, veggie_consumption_new)
```

    ## # A tibble: 5 × 3
    ##   veggie_consumption veggie_consumption_new     n
    ##                <dbl> <chr>                  <int>
    ## 1                  1 Very unlikely              3
    ## 2                  2 Unlikely                  11
    ## 3                  3 Neutral                   19
    ## 4                  4 Likely                    31
    ## 5                  5 Very likely               48

#### Question 3: Replace Integer respond for fruit consumption with String

``` r
exercise_df <- rename(exercise_df,"fruit_consumption"= "fruit_day") %>% 
  mutate(fruit_consumption_new = case_match(
    fruit_consumption,
    1 ~ "Very unlikely",
    2 ~ "Unlikely",
    3 ~ "Neutral",
    4 ~ "Likely",
    5 ~ "Very likely"
  )
  )

exercise_df %>% 
  count(fruit_consumption, fruit_consumption_new)
```

    ## # A tibble: 5 × 3
    ##   fruit_consumption fruit_consumption_new     n
    ##               <dbl> <chr>                 <int>
    ## 1                 1 Very unlikely             1
    ## 2                 2 Unlikely                  4
    ## 3                 3 Neutral                  23
    ## 4                 4 Likely                   26
    ## 5                 5 Very likely              58

## Data Vizualization

#### Question 1:Does exercising regularly affects weight of an individual?

Female Students:

``` r
#filter Female:
library(ggplot2)
library(here)
```

    ## here() starts at /Users/charlenelow/Desktop/My Projects/Food Choices and Preference of College Students

``` r
exercise_levels <- c("Everyday", "2-3 times a week","Once a week")
weight_female <- weight_df %>% 
  filter(Gender_new == "Female")
ggplot(data=weight_female)+
  geom_bar(mapping= aes(x= factor(exercise_new,exercise_levels), fill=weight_range))+ labs(title="Exercise VS Weight (lbs)", x= "Exercise", y= "Frequency", subtitle= "Female")
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-15-1.png)<!-- -->

``` r
ggsave(here("Figures","Exercise VS Weight- Female.png"))
```

    ## Saving 7 x 5 in image

Male students:

``` r
#filter Male:
weight_male <- weight_df %>% 
  filter(Gender_new == "Male")
ggplot(data=weight_male)+
  geom_bar(mapping= aes(x=factor(exercise_new,exercise_levels), fill=weight_range))+ labs(title="Exercise VS Weight (lbs)", x= "Exercise", y= "Frequency", subtitle= "Male")
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-16-1.png)<!-- -->

``` r
ggsave(here("Figures","Exercise VS Weight- Male.png"))
```

    ## Saving 7 x 5 in image

#### Question 2: Eating out VS Employment status

``` r
eating_out_levels <- c("Everyday","3-4 times","2-3 times","1-2 times","Never")
ggplot(data=frequency_df)+
  geom_bar(mapping=aes (x=factor(eating_out_new,eating_out_levels), fill=employment_new)) + labs(title = "Frequency of Eating Out VS Employment", x ="Eating out", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-17-1.png)<!-- -->

``` r
ggsave(here("Figures","Eating out VS Employment.png"))
```

    ## Saving 7 x 5 in image

#### Question 2: Eating out VS Income

``` r
ggplot(data=frequency_df)+
  geom_bar(mapping=aes (x=factor(eating_out_new,eating_out_levels), fill=income_range)) + labs(title = "Frequency of Eating Out VS Income", x ="Eating out", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-18-1.png)<!-- -->

``` r
ggsave(here("Figures","Eating out VS Income.png"))
```

    ## Saving 7 x 5 in image

#### Question 2: Eating out VS Living on or off campus

``` r
ggplot(data=frequency_df)+
  geom_bar(mapping=aes (x=factor(eating_out_new,eating_out_levels), fill=living_on_off_campus)) + labs(title = "Frequency of Eating Out VS Living on or \noff Campus", x ="Eating out", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-19-1.png)<!-- -->

``` r
ggsave(here("Figures","Eating out VSLiving on or off campus.png"))
```

    ## Saving 7 x 5 in image

#### Question 3: Exercise VS Nutritional check

``` r
nutri_levels <- c("Never","Very rarely","On certain products", "On most products", "On everything")

ggplot(data=exercise_df)+
  geom_bar(mapping=aes(x= factor(nutritional_check_new, nutri_levels),fill= exercise_new)) + labs(title="Exercise VS Nutritional checks", x= "Nutritional checks", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-20-1.png)<!-- -->

``` r
ggsave(here("Figures","Exercise VS Nutritional checks.png"))
```

    ## Saving 7 x 5 in image

#### Question 3: Exercise VS Veggie consumption

``` r
Veggie_consumption_levels <- c("Very likely","Likely","Neutral","Unlikely","Very unlikely")
ggplot(data=exercise_df)+ 
  geom_bar(mapping=aes(x= factor(veggie_consumption_new,Veggie_consumption_levels),fill=exercise_new)) + labs(title="Exercise VS Veggie consumption", x= "Veggie consumption", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-21-1.png)<!-- -->

``` r
ggsave(here("Figures","Exercise VS Veggie consumption.png"))
```

    ## Saving 7 x 5 in image

#### Question 3: Exercise VS Fruit consumption

``` r
Fruit_consumption_levels <- c("Very likely","Likely","Neutral","Unlikely","Very unlikely")
ggplot(data=exercise_df)+
  geom_bar(mapping=aes(fill=exercise_new,x=factor(fruit_consumption_new,Fruit_consumption_levels))) +
  labs(title="Exercise VS Fruit consumption", x= "Fruit consumption", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](Food_Choices_Preference_of_College_Students-copy_files/figure-gfm/unnamed-chunk-22-1.png)<!-- -->

``` r
ggsave(here("Figures","Exercise VS Fruit consumption.png"))
```

    ## Saving 7 x 5 in image

## Basic Statistic test

#### Question 1: Does exercising regularly affects weight of an individual?

Test of independence using Fisher’s extract test. alpha value = 0.05 H0:
exercise frequency and weight among female college students are
independent Since p = 0.6322 which is more than alpha value (0.05), we
accept H0 and can conclude that exercise frequency does not affect
weight of female college students in our study.

``` r
weight_female %>% 
  select("exercise_new","weight_range") %>% 
  table() %>% 
  fisher.test()
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.6039
    ## alternative hypothesis: two.sided

Since p = 0.7479 which is more than alpha value (0.05), we accept H0 and
can conclude that exercise frequency does not affect weight of male
college students in our study.

``` r
weight_male %>% 
  select("exercise_new","weight_range") %>% 
  table() %>% 
  fisher.test()
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.7479
    ## alternative hypothesis: two.sided

#### Question 2: Does factors such as: Employment, Income, and Living on or off campus affect the frequency of eating out for college students?

Test of independence using Fisher’s extract test. alpha value = 0.05 H0:
Factor(employment/income/living on or off campus) has no statistical
influence to the frequency of college student eating out. Since p =
0.6443 which is more than alpha value (0.05), we accept H0 and can
conclude that employment status of a college student does not affect the
frequency of eating out.

Employment:

``` r
frequency_df %>% 
  select("employment_new","eating_out_new") %>% 
  table() %>% 
  fisher.test()
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.6443
    ## alternative hypothesis: two.sided

Income: Since p = 0.6681 which is more than alpha value (0.05), we
accept H0 and can conclude that income of a college student does not
affect the frequency of eating out.

``` r
frequency_df %>% 
  select("income_range","eating_out_new") %>% 
  table() %>% 
  fisher.test(input_table, workspace = 1e7) #increase workspace due to error message
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.6681
    ## alternative hypothesis: two.sided

Living on and off campus: Since p = 0.2007 which is more than alpha
value (0.05), we accept H0 and can conclude that living on or off campus
does not affect the frequency of eating out.

``` r
frequency_df %>% 
  select("living_on_off_campus","eating_out_new") %>% 
  table() %>% 
  fisher.test() 
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.2007
    ## alternative hypothesis: two.sided

#### Question 3: Does students who exercise regularly more likely to make better food choices?

Test of independence using Fisher’s extract test. alpha value = 0.05 H0:
Students who exercise regularly are more likely to make better food
choices. Since p = 0.1133 which is more than alpha value (0.05), we
accept H0 and can conclude that students who exercise regularly does not
check nutritional labels of food more regularly.

``` r
exercise_df %>% 
  select("nutritional_check_new","exercise_new") %>% 
  table() %>% 
  fisher.test()
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.1133
    ## alternative hypothesis: two.sided

Since p = 0.1485 which is more than alpha value (0.05), we accept H0 and
can conclude that students who exercise regularly does always consumer
more vegetables.

``` r
exercise_df %>% 
  select("veggie_consumption_new","exercise_new") %>% 
  table() %>% 
  fisher.test()
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.1485
    ## alternative hypothesis: two.sided

Since p = 0.03453 which is less than alpha value (0.05), we reject H0
and can conclude that students who exercise regularly does consumer more
fruits.

``` r
exercise_df %>% 
  select("fruit_consumption_new","exercise_new") %>% 
  table() %>% 
  fisher.test()
```

    ## 
    ##  Fisher's Exact Test for Count Data
    ## 
    ## data:  .
    ## p-value = 0.03453
    ## alternative hypothesis: two.sided
