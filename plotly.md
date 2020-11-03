plotly
================
Henry Stoddard
10/31/2020

``` r
library(tidyverse)
library(p8105.datasets)
library(plotly)

data("rest_inspec")
inspection_df =
  rest_inspec %>% 
  janitor::clean_names() %>% 
  select(boro, critical_flag, grade, inspection_date, score)%>%
  drop_na()

scatter_plot =
  inspection_df %>% 
  filter(boro == "MANHATTAN") %>% 
  plot_ly(x=~inspection_date, y=~score, alpha = .5, type = "scatter"
          , mode = "markers")
bar_plot = 
  inspection_df %>% 
  group_by(boro) %>% 
  mutate(avg_score = mean(score)) %>% 
  plot_ly(x=~boro, y=~avg_score, color=~boro, type = "bar")

box_plot =
  inspection_df %>% 
  group_by(boro) %>% 
  plot_ly(x=~boro, y=~score, color =~boro, type = "box")
```
