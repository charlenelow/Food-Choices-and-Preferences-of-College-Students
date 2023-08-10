Food Choices and Preference of College Students
================
Charlene
2023-08-09

## Loading readr package & Import CSV file

Dataset used for this project was imported using readr package. To do
so, the tidyverse package which contains readr package was installed and
loaded.

Import CSV file using read_csv().

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
glimpse(food_survey_respond_df)
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

#### Remove missing values

Removed rows with missing values (NA) and saved it as a new dataframe
(new_responds_df).

``` r
library(tidyr)
food_survey_respond_df %>% 
  drop_na() -> new_respond_df
nrow(new_respond_df) # left 60 responses after dropping na
```

    ## [1] 60

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
weight_df<- new_respond_df %>% 
  select("Gender","exercise","weight")

weight_df %>% 
  count(weight) # to identify which responds needs cleaning / removing
```

    ## # A tibble: 31 × 2
    ##    weight     n
    ##    <chr>  <int>
    ##  1 110        1
    ##  2 115        1
    ##  3 116        1
    ##  4 120        2
    ##  5 123        1
    ##  6 125        2
    ##  7 130        2
    ##  8 135        4
    ##  9 137        1
    ## 10 140        5
    ## # ℹ 21 more rows

``` r
weight_df %>% 
  count(Gender) # should have 1 & 2 only. 1= Female, 2 = Male
```

    ## # A tibble: 2 × 2
    ##   Gender     n
    ##    <dbl> <int>
    ## 1      1    36
    ## 2      2    24

``` r
weight_df %>% 
  count(exercise)
```

    ## # A tibble: 3 × 2
    ##   exercise     n
    ##      <dbl> <int>
    ## 1        1    34
    ## 2        2    20
    ## 3        3     6

There are 4 rows in weight that needs cleaning before we can start
analysis.

``` r
library(stringr)
weight_df$weight <- str_replace_all(weight_df$weight, "^144 lbs$", "144")
weight_df$weight <- str_replace_all(weight_df$weight, "^Not sure, 240$", "240")

#Removing Row 2 & row 45
weight_df<- weight_df[-c(2,45),]

#Double checking the data within weight to make sure we have cleaned up properly
weight_df %>% 
  count(weight)
```

    ## # A tibble: 29 × 2
    ##    weight     n
    ##    <chr>  <int>
    ##  1 110        1
    ##  2 115        1
    ##  3 116        1
    ##  4 120        2
    ##  5 123        1
    ##  6 125        2
    ##  7 130        2
    ##  8 135        4
    ##  9 137        1
    ## 10 140        5
    ## # ℹ 19 more rows

#### Question 1: Replace Integer respond for Gender with String

``` r
weight_df <- weight_df %>% 
  mutate(Gender_Num = Gender) # create a duplicate column to preserve original data
weight_df$Gender <- str_replace_all(weight_df$Gender, "^1$", "Female")
weight_df$Gender <- str_replace_all(weight_df$Gender, "^2$", "Male")

weight_df %>% 
  count(Gender)
```

    ## # A tibble: 2 × 2
    ##   Gender     n
    ##   <chr>  <int>
    ## 1 Female    35
    ## 2 Male      23

#### Question 1: Replace Integer respond for exercise with String

``` r
weight_df <- weight_df %>% 
  mutate(exercise_Num = exercise) # create a duplicate column to preserve original data
weight_df$exercise <- str_replace_all(weight_df$exercise, "1", "Everyday")
weight_df$exercise <- str_replace_all(weight_df$exercise, "3", "once a week")
weight_df$exercise <- str_replace_all(weight_df$exercise, "2", "2-3 times a week")
weight_df$exercise <- str_replace_all(weight_df$exercise, "4", "Sometimes")
weight_df$exercise <- str_replace_all(weight_df$exercise, "5", "Never")

weight_df %>% 
  count(exercise)
```

    ## # A tibble: 3 × 2
    ##   exercise             n
    ##   <chr>            <int>
    ## 1 2-3 times a week    18
    ## 2 Everyday            34
    ## 3 once a week          6

#### Question 1: Replace Integer respond for weight with String

``` r
weight_df %>% 
  group_by (weight) %>% 
  summarize(count = sum(weight <129))
```

    ## # A tibble: 29 × 2
    ##    weight count
    ##    <chr>  <int>
    ##  1 110        1
    ##  2 115        1
    ##  3 116        1
    ##  4 120        2
    ##  5 123        1
    ##  6 125        2
    ##  7 130        0
    ##  8 135        0
    ##  9 137        0
    ## 10 140        0
    ## # ℹ 19 more rows

``` r
weight_df %>% 
  group_by (weight) %>% 
  summarize(count= sum(weight >129 & weight <159))
```

    ## # A tibble: 29 × 2
    ##    weight count
    ##    <chr>  <int>
    ##  1 110        0
    ##  2 115        0
    ##  3 116        0
    ##  4 120        0
    ##  5 123        0
    ##  6 125        0
    ##  7 130        2
    ##  8 135        4
    ##  9 137        1
    ## 10 140        5
    ## # ℹ 19 more rows

``` r
weight_df %>% 
  group_by (weight) %>% 
  summarize(count= sum(weight >159 & weight <189))
```

    ## # A tibble: 29 × 2
    ##    weight count
    ##    <chr>  <int>
    ##  1 110        0
    ##  2 115        0
    ##  3 116        0
    ##  4 120        0
    ##  5 123        0
    ##  6 125        0
    ##  7 130        0
    ##  8 135        0
    ##  9 137        0
    ## 10 140        0
    ## # ℹ 19 more rows

``` r
weight_df %>% 
  group_by (weight) %>% 
  summarize(count= sum(weight >=190))
```

    ## # A tibble: 29 × 2
    ##    weight count
    ##    <chr>  <int>
    ##  1 110        0
    ##  2 115        0
    ##  3 116        0
    ##  4 120        0
    ##  5 123        0
    ##  6 125        0
    ##  7 130        0
    ##  8 135        0
    ##  9 137        0
    ## 10 140        0
    ## # ℹ 19 more rows

``` r
#creating new column in weight_df
weight_df<- weight_df %>% 
  mutate(weight_df, weight_range=weight)

#Rename 110 - 129 lbs:
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^110$", "110-129")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^115$", "110-129")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^116$", "110-129")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^120$", "110-129")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^123$", "110-129")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^125$", "110-129")

#Rename 130 - 159 lbs:
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^130$", "130-159")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^135$", "130-159")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^137$", "130-159")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^140$", "130-159")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^144$", "130-159")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^145$", "130-159")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^150$", "130-159")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^155$", "130-159")

#Rename 160 -189 lbs:
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^160$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^165$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^167$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^168$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^169$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^170$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^175$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^180$", "160-189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^185$", "160-189")

#Rename >190 lbs:
weight_df$weight_range <-
str_replace_all(weight_df$weight_range, "^190$", ">189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^200$", ">189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^205$", ">189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^210$", ">189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^240$", ">189")
weight_df$weight_range <- str_replace_all(weight_df$weight_range, "^264$", ">189")
```

#### Question 2: Creating new dataframe with variables of interest

``` r
frequency_df <- new_respond_df %>% 
  select ("eating_out","employment","income","on_off_campus")

glimpse(frequency_df)
```

    ## Rows: 60
    ## Columns: 4
    ## $ eating_out    <dbl> 2, 2, 2, 2, 2, 2, 3, 2, 1, 1, 4, 2, 2, 3, 4, 1, 2, 2, 2,…
    ## $ employment    <dbl> 2, 3, 3, 2, 3, 2, 3, 1, 2, 3, 2, 3, 3, 2, 2, 2, 2, 3, 2,…
    ## $ income        <dbl> 4, 6, 6, 6, 4, 5, 4, 3, 5, 5, 5, 5, 6, 5, 6, 6, 4, 6, 5,…
    ## $ on_off_campus <dbl> 1, 2, 1, 1, 2, 1, 1, 3, 1, 1, 2, 2, 1, 1, 1, 1, 1, 1, 1,…

#### Question 2: Replace Integer respond for eating_out with String

``` r
frequency_df <- frequency_df %>% 
  mutate(eating_out_Num = eating_out) # create a duplicate column to preserve original data
frequency_df$eating_out <- str_replace_all(frequency_df$eating_out, "^1$", "Never")
frequency_df$eating_out <- str_replace_all(frequency_df$eating_out, "^2$", "1-2 times")
frequency_df$eating_out <- str_replace_all(frequency_df$eating_out, "^3$", "2-3 times")
frequency_df$eating_out <- str_replace_all(frequency_df$eating_out, "^5$", "Everyday")
frequency_df$eating_out <- str_replace_all(frequency_df$eating_out, "^4$", "3-5 times")


frequency_df %>% 
  count(eating_out) # checking if above code has been run correctly
```

    ## # A tibble: 5 × 2
    ##   eating_out     n
    ##   <chr>      <int>
    ## 1 1-2 times     32
    ## 2 2-3 times     13
    ## 3 3-5 times      5
    ## 4 Everyday       2
    ## 5 Never          8

#### Question 2: Replace Integer respond for employment with String

``` r
frequency_df <- frequency_df %>% 
  mutate(employment_Num = employment) # create a duplicate to preserve original data column
frequency_df$employment <- str_replace_all(frequency_df$employment, "1", "Full time")
frequency_df$employment <- str_replace_all(frequency_df$employment, "2", "Part time")
frequency_df$employment <- str_replace_all(frequency_df$employment, "3", "Unemployed")

frequency_df %>% 
  count(employment)
```

    ## # A tibble: 3 × 2
    ##   employment     n
    ##   <chr>      <int>
    ## 1 Full time      1
    ## 2 Part time     33
    ## 3 Unemployed    26

#### Question 2: Replace Integer respond for income with String

``` r
frequency_df <- frequency_df %>% 
  mutate(income_Num = income) # create a duplicate column to preserve original data
frequency_df$income <- str_replace_all(frequency_df$income, "^1$", "less than $15K")
frequency_df$income <- str_replace_all(frequency_df$income, "^2$", "$15.001K-$30K")
frequency_df$income <- str_replace_all(frequency_df$income, "^3$", "$30.001K-$50K")
frequency_df$income <- str_replace_all(frequency_df$income, "^4$", "$50.001K-$70K")
frequency_df$income <- str_replace_all(frequency_df$income, "^5$", "$70.001K-$100K")
frequency_df$income <- str_replace_all(frequency_df$income, "^6$", "more than $100K")

frequency_df %>% 
  count(income)
```

    ## # A tibble: 6 × 2
    ##   income              n
    ##   <chr>           <int>
    ## 1 $15.001K-$30K       1
    ## 2 $30.001K-$50K       6
    ## 3 $50.001K-$70K      10
    ## 4 $70.001K-$100K     18
    ## 5 less than $15K      1
    ## 6 more than $100K    24

#### Question 2: Replace Integer respond for living on and off campus with String

``` r
frequency_df <- frequency_df %>% 
  mutate(income_Num = on_off_campus) # create a duplicate column to preserve original data
frequency_df$on_off_campus <- str_replace_all(frequency_df$on_off_campus, "1", "On campus")
frequency_df$on_off_campus <- str_replace_all(frequency_df$on_off_campus, "2", "Off campus")
frequency_df$on_off_campus <- str_replace_all(frequency_df$on_off_campus, "3", "Off campus")
frequency_df$on_off_campus <- str_replace_all(frequency_df$on_off_campus, "4", "Off campus")

frequency_df %>% 
  count(on_off_campus)
```

    ## # A tibble: 2 × 2
    ##   on_off_campus     n
    ##   <chr>         <int>
    ## 1 Off campus       16
    ## 2 On campus        44

#### Question 3: Creating new dataframe with variables of interest

``` r
exercise_df <- new_respond_df %>% 
  select ("exercise","nutritional_check","veggies_day","fruit_day")

glimpse(exercise_df)
```

    ## Rows: 60
    ## Columns: 4
    ## $ exercise          <dbl> 1, 2, 3, 1, 1, 2, 1, 1, 1, 3, 2, 2, 1, 3, 1, 1, 3, 1…
    ## $ nutritional_check <dbl> 4, 4, 2, 3, 4, 4, 5, 2, 5, 2, 2, 2, 4, 2, 2, 3, 2, 4…
    ## $ veggies_day       <dbl> 4, 5, 3, 4, 4, 4, 5, 5, 5, 3, 5, 5, 4, 5, 3, 3, 4, 3…
    ## $ fruit_day         <dbl> 4, 5, 4, 4, 4, 5, 5, 5, 5, 4, 5, 5, 3, 5, 2, 4, 3, 4…

#### Question 3: Replace Integer respond for exercise with String

``` r
exercise_df <- exercise_df %>% 
  mutate(exercise_Num = exercise) # create a duplicate column to preserve original data
exercise_df$exercise <- str_replace_all(exercise_df$exercise, "1", "Everyday")
exercise_df$exercise <- str_replace_all(exercise_df$exercise, "3", "once a week")
exercise_df$exercise <- str_replace_all(exercise_df$exercise, "2", "2-3 times a week")
exercise_df$exercise <- str_replace_all(exercise_df$exercise, "4", "Sometimes")
exercise_df$exercise <- str_replace_all(exercise_df$exercise, "5", "Never")

exercise_df %>% 
  count(exercise)
```

    ## # A tibble: 3 × 2
    ##   exercise             n
    ##   <chr>            <int>
    ## 1 2-3 times a week    20
    ## 2 Everyday            34
    ## 3 once a week          6

#### Question 3: Replace Integer respond for Nutritional check with String

``` r
exercise_df <- exercise_df %>% 
  mutate(nutritional_check_Num = nutritional_check) # create a duplicate column to preserve original data
exercise_df$nutritional_check <- str_replace_all(exercise_df$nutritional_check, "1", "Never")
exercise_df$nutritional_check <- str_replace_all(exercise_df$nutritional_check, "2", "On certain products")
exercise_df$nutritional_check <- str_replace_all(exercise_df$nutritional_check, "3", "Very rarely")
exercise_df$nutritional_check <- str_replace_all(exercise_df$nutritional_check, "4", "On most products")
exercise_df$nutritional_check <- str_replace_all(exercise_df$nutritional_check, "5", "On everything")

exercise_df %>% 
  count(nutritional_check)
```

    ## # A tibble: 5 × 2
    ##   nutritional_check       n
    ##   <chr>               <int>
    ## 1 Never                   1
    ## 2 On certain products    18
    ## 3 On everything           9
    ## 4 On most products       24
    ## 5 Very rarely             8

#### Question 3: Replace Integer respond for veggie consumption with String

``` r
exercise_df <- rename(exercise_df,"veggie_consumption" = "veggies_day") #rename column name for better representation of data

exercise_df <- exercise_df %>% 
  mutate(veggie_consumption_Num = veggie_consumption) # create a duplicate column to preserve original data

exercise_df$veggie_consumption <- str_replace_all(exercise_df$veggie_consumption, "1", "Very unlikely")
exercise_df$veggie_consumption <- str_replace_all(exercise_df$veggie_consumption, "2", "Unlikely")
exercise_df$veggie_consumption <- str_replace_all(exercise_df$veggie_consumption, "3", "Neutral")
exercise_df$veggie_consumption <- str_replace_all(exercise_df$veggie_consumption, "4", "Likely")
exercise_df$veggie_consumption <- str_replace_all(exercise_df$veggie_consumption, "5", "Very likely")

exercise_df %>% 
  count(veggie_consumption)
```

    ## # A tibble: 5 × 2
    ##   veggie_consumption     n
    ##   <chr>              <int>
    ## 1 Likely                21
    ## 2 Neutral                7
    ## 3 Unlikely               6
    ## 4 Very likely           25
    ## 5 Very unlikely          1

#### Question 3: Replace Integer respond for fruit consumption with String

``` r
exercise_df <- rename(exercise_df,"fruit_consumption"= "fruit_day") #rename column name for better representation of data

exercise_df<- exercise_df %>% 
  mutate(fruit_consumption_Num = fruit_consumption)

exercise_df$fruit_consumption <- str_replace_all(exercise_df$fruit_consumption, "1", "Very unlikely")
exercise_df$fruit_consumption <- str_replace_all(exercise_df$fruit_consumption, "2", "Unlikely")
exercise_df$fruit_consumption <- str_replace_all(exercise_df$fruit_consumption, "3", "Neutral")
exercise_df$fruit_consumption <- str_replace_all(exercise_df$fruit_consumption, "4", "Likely")
exercise_df$fruit_consumption <- str_replace_all(exercise_df$fruit_consumption, "5", "Very likely")

exercise_df %>% 
  count(fruit_consumption)
```

    ## # A tibble: 4 × 2
    ##   fruit_consumption     n
    ##   <chr>             <int>
    ## 1 Likely               16
    ## 2 Neutral              11
    ## 3 Unlikely              2
    ## 4 Very likely          31

## Data Vizualization

#### Question 1: Eating out VS Employment status

``` r
#filter Female:
library(ggplot2)
weight_female <- weight_df %>% 
  filter(Gender == "Female")
ggplot(data=weight_female)+
  geom_bar(mapping= aes(x=exercise, fill=weight_range))+ labs(title="Exercise VS Weight (lbs)", x= "Exercise", y= "Frequency", subtitle= "Female")
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-19-1.png)'<!-- -->

Among female students, individuals in the lowest weight range 110 - 129
lbs mostly exercise daily while a small group exercises at least 2 - 3
times a week. Individuals in the 2nd lowest weight range mostly exercise
daily or 2 to 3 times a week, while a small group exercises once a week.
Individuals in 160 - 189 lbs range either exercise daily or just once a
week and for individuals in >189 lbs range, most of them exercise
daily.

``` r
#filter Male:
weight_male <- weight_df %>% 
  filter(Gender == "Male")
ggplot(data=weight_male)+
  geom_bar(mapping= aes(x=exercise, fill=weight_range))+ labs(title="Exercise VS Weight (lbs)", x= "Exercise", y= "Frequency", subtitle= "Male")
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-20-1.png)<!-- -->

Among male students, individuals in the lowest weight range 130 - 159
lbs exercises daily. Most individuals in the 160 - 189 lbs range
exercises daily and \>189 lbs 2 - 3 times a week.

#### Question 2: Eating out VS Employment status

``` r
ggplot(data=frequency_df)+
  geom_bar(mapping=aes (x=eating_out, fill=employment)) + labs(title = "Frequency of Eating Out VS Employment", x ="Eating out", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-21-1.png)<!-- -->

Most college students regardless of their employment status tends to eat
out 1 - 2 times a week, and only very few eat out everyday.

#### Question 2: Eating out VS Income

``` r
ggplot(data=frequency_df)+
  geom_bar(mapping=aes (x=eating_out, fill=income)) + labs(title = "Frequency of Eating Out VS Income", x ="Eating out", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-22-1.png)<!-- -->

There is a similar trend observed here compared to Frequency of eating
out VS employment where most student regardless of income eats out 1 - 2
time a week, followed by 2 to 3 times, never, 3 to 5 times and least
number of students eat out everyday.

An additional observation made is, only students with income of more
than \$100K chooses to eat out everyday.

#### Question 2: Eating out VS Living on or off campus

``` r
ggplot(data=frequency_df)+
  geom_bar(mapping=aes (x=eating_out, fill=on_off_campus)) + labs(title = "Frequency of Eating Out VS Living on or off Campus", x ="Eating out", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-23-1.png)<!-- -->

There is a similar trend observed for the frequency of eating out VS
Living on or off campus as the other two factors (employment & income),
where most college students regardless of living situation tends to eat
out mostly 1-2 times a week and very small number of students eat out
everyday. Those who does eat out everyday tend to be living on campus.

#### Question 3: Exercise VS Nutritional check

``` r
ggplot(data=exercise_df)+
  geom_bar(mapping=aes(fill=exercise,x=nutritional_check)) +
  labs(title="Exercise VS Nutritional checks", x= "Nutritional checks", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-24-1.png)<!-- -->

Generally students who exercises more often tends to check nutritional
content of the food they consume. This would also make them more
conscious of the food choices they make and thus have higher chances of
making better food choices compared to students who do not.

#### Question 3: Exercise VS Veggie consumption

``` r
ggplot(data=exercise_df)+
  geom_bar(mapping=aes(fill=exercise,x=veggie_consumption)) +
  labs(title="Exercise VS Veggie consumption", x= "Veggie consumption", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-25-1.png)<!-- -->

The general observation of vegetables consumption in relation to
frequency of exercising is that students who exercise more regularly are
more likely to consume vegetables. However, it is also seen that a small
group of students who exercise daily or 2-3 times a week are unlikely to
consume vegetables. This group of students might have food aversion to
vegetables.

#### Question 3: Exercise VS Fruit consumption

``` r
ggplot(data=exercise_df)+
  geom_bar(mapping=aes(fill=exercise,x=fruit_consumption)) +
  labs(title="Exercise VS Fruit consumption", x= "Fruit consumption", y="Frequency") + theme(axis.text.x = element_text(angle = 45))
```

![](https://github.com/charlenelow/Food-Choices-and-Preferences-of-College-Students/blob/main/unnamed-chunk-26-1.png)<!-- -->

Similar to the observation made for vegetable consumption, students who
exercise more regularly are likely to consume fruits and there is also a
small group of students who exercise daily but is unlikely to consume
fruit. We should also keep in mind that this group of students might
have food aversion towards fruits.
