Homework 6
================
Vincent Tam
November 25, 2018

``` r
library(tidyverse)
```

    ## -- Attaching packages ----------------------------- tidyverse 1.2.1 --

    ## v ggplot2 3.0.0     v purrr   0.2.5
    ## v tibble  1.4.2     v dplyr   0.7.6
    ## v tidyr   0.8.1     v stringr 1.3.1
    ## v readr   1.1.1     v forcats 0.3.0

    ## -- Conflicts -------------------------------- tidyverse_conflicts() --
    ## x dplyr::filter() masks stats::filter()
    ## x dplyr::lag()    masks stats::lag()

``` r
library(janitor)
library(dplyr)
library(purrr)
hom_data <- read.csv(file = "./homicide-data.csv") 
hom_data = 
  hom_data %>%
  mutate(city_state = str_c(city, ",", state)) %>%
  filter(city_state != "Dallas,TX", city_state != "Phoenix,AZ", city_state != "Kansas City,MO", city_state != "Tulsa,AL") %>% 
  filter(victim_sex != "Unknown") %>%
  mutate(victim_sex = as.factor(victim_sex)) %>%
  mutate(victim_race = recode(victim_race, 'White' = "White", 'Hispanic' = "Non_white", 'Other' = "Non_white", 'Black' = "Non_white", 'Asian' = "Non_white", 'Unknown' = "Non_white")) %>% 
  mutate(solved = as.numeric(disposition == "Closed by arrest"),
         victim_age = as.numeric(victim_age),
         victim_race = fct_relevel(victim_race, "White", "Non_white")) %>% 
  mutate(victim_age = as.numeric(victim_age)) 
baltimore_data = 
  hom_data %>%
  filter(city_state == "Baltimore,MD")
baltimore_fit = 
  baltimore_data %>% 
  glm(solved ~ victim_age + victim_race + victim_sex, data = ., family = binomial()) %>% 
  broom::tidy() %>% 
  mutate(OR = boot::inv.logit(estimate)) %>%
  select(term, log_OR = estimate, OR, p.value) %>% 
  knitr::kable(digits = 3)
cities_glinmodel = 
  hom_data %>% 
  group_by(city_state) %>%
  select(city_state, solved, victim_age, victim_race, victim_sex) %>%
  nest() %>% 
  mutate(glinmodel = map(data, ~glm(solved ~ victim_age + victim_race + victim_sex, data = ., family = binomial()))) %>%
  mutate(glinmodel_tidy = map(glinmodel, ~broom::tidy(.))) %>%
  mutate(glinmodel_ci = map(glinmodel, ~broom::confint_tidy(.))) %>%
  select(city_state, glinmodel_tidy, glinmodel_ci) %>% 
  unnest() %>% 
  mutate(OR = exp(estimate)) %>%
  mutate(conf.low = exp(estimate - (1.96 * std.error)), conf.high = exp(estimate + (1.96 * std.error))) 
cities_plot =
  cities_glinmodel %>% 
  ggplot(aes(fct_reorder(city_state, OR), OR)) +
  geom_point() +
  geom_errorbar(aes(ymin = conf.low, ymax = conf.high)) +
  labs(
    title = "Estimates and CIs for All Cities",
    x = "City",
    y = "Estimates"
  )  +
  theme(axis.text.x = element_text(angle = 90))
cities_plot
```

![](hw6_files/figure-markdown_github/setup-1.png)
