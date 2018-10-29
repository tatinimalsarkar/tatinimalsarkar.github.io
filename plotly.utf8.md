---
title: "Some plots about NYC restaurants"
output: 
  flexdashboard::flex_dashboard:
    orientation: columns
    vertical_layout: fill
---

I like to eat! Let's investigate some restaurants in the Big Apple.

Chart A depicts American restaurants in NYC, separated by borough. Chart B shows NYC Department of Health scores for Korean restaurants in Manhattan by year of inspection. Chart C shows DOH scores for Chinese restaurants by borough.

Whew! All those charts are making me hungry. Time for a snack!



Column {data-width = 650}
-----------------------------------------------------------------------

### Chart A

```r
nyrest_a = read_csv("./data/DOHMH_New_York_City_Restaurant_Inspection_Results.csv.gz") %>% 
  janitor::clean_names() %>% 
  filter(cuisine_description == "American")
```

```
## Parsed with column specification:
## cols(
##   action = col_character(),
##   boro = col_character(),
##   building = col_integer(),
##   camis = col_integer(),
##   critical_flag = col_character(),
##   cuisine_description = col_character(),
##   dba = col_character(),
##   inspection_date = col_datetime(format = ""),
##   inspection_type = col_character(),
##   phone = col_character(),
##   record_date = col_datetime(format = ""),
##   score = col_integer(),
##   street = col_character(),
##   violation_code = col_character(),
##   violation_description = col_character(),
##   zipcode = col_integer(),
##   grade = col_character(),
##   grade_date = col_datetime(format = "")
## )
```

```
## Warning in rbind(names(probs), probs_f): number of columns of result is not
## a multiple of vector length (arg 1)
```

```
## Warning: 9380 parsing failures.
## row # A tibble: 5 x 5 col     row col     expected  actual file                                      expected   <int> <chr>   <chr>     <chr>  <chr>                                     actual 1  2292 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… file 2  3268 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… row 3  5321 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… col 4  5689 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… expected 5  6364 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I…
## ... ................. ... .......................................................................... ........ .......................................................................... ...... .......................................................................... .... .......................................................................... ... .......................................................................... ... .......................................................................... ........ ..........................................................................
## See problems(...) for more details.
```

```r
nyrest_a %>% 
  count(boro) %>% 
  mutate(boro = fct_reorder(boro, n)) %>% 
  plot_ly(x = ~boro, y = ~n, color = ~boro, type = "bar")
```

preserveada5079dd989e403


Column {data-width=350}
-----------------------------------------------------------------------

### Chart B


```r
nyrest_b = read_csv("./data/DOHMH_New_York_City_Restaurant_Inspection_Results.csv.gz") %>% 
  janitor::clean_names() %>% 
  filter(!is.na(grade),
         boro == "MANHATTAN",
         cuisine_description == "Korean") 
```

```
## Parsed with column specification:
## cols(
##   action = col_character(),
##   boro = col_character(),
##   building = col_integer(),
##   camis = col_integer(),
##   critical_flag = col_character(),
##   cuisine_description = col_character(),
##   dba = col_character(),
##   inspection_date = col_datetime(format = ""),
##   inspection_type = col_character(),
##   phone = col_character(),
##   record_date = col_datetime(format = ""),
##   score = col_integer(),
##   street = col_character(),
##   violation_code = col_character(),
##   violation_description = col_character(),
##   zipcode = col_integer(),
##   grade = col_character(),
##   grade_date = col_datetime(format = "")
## )
```

```
## Warning in rbind(names(probs), probs_f): number of columns of result is not
## a multiple of vector length (arg 1)
```

```
## Warning: 9380 parsing failures.
## row # A tibble: 5 x 5 col     row col     expected  actual file                                      expected   <int> <chr>   <chr>     <chr>  <chr>                                     actual 1  2292 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… file 2  3268 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… row 3  5321 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… col 4  5689 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… expected 5  6364 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I…
## ... ................. ... .......................................................................... ........ .......................................................................... ...... .......................................................................... .... .......................................................................... ... .......................................................................... ... .......................................................................... ........ ..........................................................................
## See problems(...) for more details.
```

```r
nyrest_b %>% 
  mutate(text_label = str_c("Type of warning: ", critical_flag, "\nScore: ", score),
         year = lubridate::year(inspection_date)) %>% 
  plot_ly(x = ~year, y = ~score, type = "scatter", mode = "markers",
          alpha = 0.5,
          color = ~critical_flag,
          text = ~text_label)
```

preserve6aea3a488c295b1b

### Chart C


```r
nyrest_c = read_csv("./data/DOHMH_New_York_City_Restaurant_Inspection_Results.csv.gz") %>% 
  janitor::clean_names() %>% 
  filter(cuisine_description == "Chinese")
```

```
## Parsed with column specification:
## cols(
##   action = col_character(),
##   boro = col_character(),
##   building = col_integer(),
##   camis = col_integer(),
##   critical_flag = col_character(),
##   cuisine_description = col_character(),
##   dba = col_character(),
##   inspection_date = col_datetime(format = ""),
##   inspection_type = col_character(),
##   phone = col_character(),
##   record_date = col_datetime(format = ""),
##   score = col_integer(),
##   street = col_character(),
##   violation_code = col_character(),
##   violation_description = col_character(),
##   zipcode = col_integer(),
##   grade = col_character(),
##   grade_date = col_datetime(format = "")
## )
```

```
## Warning in rbind(names(probs), probs_f): number of columns of result is not
## a multiple of vector length (arg 1)
```

```
## Warning: 9380 parsing failures.
## row # A tibble: 5 x 5 col     row col     expected  actual file                                      expected   <int> <chr>   <chr>     <chr>  <chr>                                     actual 1  2292 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… file 2  3268 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… row 3  5321 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… col 4  5689 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I… expected 5  6364 buildi… an integ… NKA    './data/DOHMH_New_York_City_Restaurant_I…
## ... ................. ... .......................................................................... ........ .......................................................................... ...... .......................................................................... .... .......................................................................... ... .......................................................................... ... .......................................................................... ........ ..........................................................................
## See problems(...) for more details.
```

```r
nyrest_c %>% 
  mutate(boro = fct_reorder(boro, score)) %>% 
  plot_ly(y = ~score, color = ~boro, type = "box", colors = "Set2")
```

```
## Warning: Ignoring 1555 observations
```

preservef4f10d330e02b945

