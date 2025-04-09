---
title: "02-qmd-figures-chunks"
author: "Your Name"
date: today
format: 
  html:
    keep-md: true
    fig-height: 10
    fig-align: center
    fig-asp: 1.5
    fig-format: png
    fig-dpi: 300
---


::: {.cell}

```{.r .cell-code}
library(tidyverse)
```

::: {.cell-output .cell-output-stderr}

```
── Attaching core tidyverse packages ──────────────────────── tidyverse 2.0.0 ──
✔ dplyr     1.1.4     ✔ readr     2.1.5
✔ forcats   1.0.0     ✔ stringr   1.5.1
✔ ggplot2   3.5.1     ✔ tibble    3.2.1
✔ lubridate 1.9.3     ✔ tidyr     1.3.1
✔ purrr     1.0.2     
── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
✖ dplyr::filter() masks stats::filter()
✖ dplyr::lag()    masks stats::lag()
ℹ Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```


:::

```{.r .cell-code}
library(skimr)
```
:::

::: {.cell}

```{.r .cell-code}
gap <- read_csv(here::here("data", "gapminder.csv"))
```

::: {.cell-output .cell-output-stderr}

```
Rows: 1704 Columns: 6
── Column specification ────────────────────────────────────────────────────────
Delimiter: ","
chr (2): country, continent
dbl (4): year, lifeExp, pop, gdpPercap

ℹ Use `spec()` to retrieve the full column specification for this data.
ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.
```


:::

```{.r .cell-code}
gap
```

::: {.cell-output .cell-output-stdout}

```
# A tibble: 1,704 × 6
   country     continent  year lifeExp      pop gdpPercap
   <chr>       <chr>     <dbl>   <dbl>    <dbl>     <dbl>
 1 Afghanistan Asia       1952    28.8  8425333      779.
 2 Afghanistan Asia       1957    30.3  9240934      821.
 3 Afghanistan Asia       1962    32.0 10267083      853.
 4 Afghanistan Asia       1967    34.0 11537966      836.
 5 Afghanistan Asia       1972    36.1 13079460      740.
 6 Afghanistan Asia       1977    38.4 14880372      786.
 7 Afghanistan Asia       1982    39.9 12881816      978.
 8 Afghanistan Asia       1987    40.8 13867957      852.
 9 Afghanistan Asia       1992    41.7 16317921      649.
10 Afghanistan Asia       1997    41.8 22227415      635.
# ℹ 1,694 more rows
```


:::
:::



Using the “02-qmd-figures-chunks.qmd”
Create a summary of your gapminder data, put it into a table.
Add a caption to this table.
Set the number of decimals to 2.



::: {.cell}

```{.r .cell-code}
summary_gap <- summary(gap)
knitr::kable(summary_gap,
             caption = "A table of the summary of gapminder",
             digits = 2)
```

::: {.cell-output-display}


Table: A table of the summary of gapminder

|   |  country        | continent       |     year    |   lifeExp    |     pop          |  gdpPercap      |
|:--|:----------------|:----------------|:------------|:-------------|:-----------------|:----------------|
|   |Length:1704      |Length:1704      |Min.   :1952 |Min.   :23.60 |Min.   :6.001e+04 |Min.   :   241.2 |
|   |Class :character |Class :character |1st Qu.:1966 |1st Qu.:48.20 |1st Qu.:2.794e+06 |1st Qu.:  1202.1 |
|   |Mode  :character |Mode  :character |Median :1980 |Median :60.71 |Median :7.024e+06 |Median :  3531.8 |
|   |NA               |NA               |Mean   :1980 |Mean   :59.47 |Mean   :2.960e+07 |Mean   :  7215.3 |
|   |NA               |NA               |3rd Qu.:1993 |3rd Qu.:70.85 |3rd Qu.:1.959e+07 |3rd Qu.:  9325.5 |
|   |NA               |NA               |Max.   :2007 |Max.   :82.60 |Max.   :1.319e+09 |Max.   :113523.1 |


:::
:::

::: {.cell}

```{.r .cell-code}
skim(gap)
```

::: {.cell-output-display}

Table: Data summary

|                         |     |
|:------------------------|:----|
|Name                     |gap  |
|Number of rows           |1704 |
|Number of columns        |6    |
|_______________________  |     |
|Column type frequency:   |     |
|character                |2    |
|numeric                  |4    |
|________________________ |     |
|Group variables          |None |


**Variable type: character**

|skim_variable | n_missing| complete_rate| min| max| empty| n_unique| whitespace|
|:-------------|---------:|-------------:|---:|---:|-----:|--------:|----------:|
|country       |         0|             1|   4|  24|     0|      142|          0|
|continent     |         0|             1|   4|   8|     0|        5|          0|


**Variable type: numeric**

|skim_variable | n_missing| complete_rate|        mean|           sd|       p0|        p25|        p50|         p75|         p100|hist  |
|:-------------|---------:|-------------:|-----------:|------------:|--------:|----------:|----------:|-----------:|------------:|:-----|
|year          |         0|             1|     1979.50|        17.27|  1952.00|    1965.75|    1979.50|     1993.25|       2007.0|▇▅▅▅▇ |
|lifeExp       |         0|             1|       59.47|        12.92|    23.60|      48.20|      60.71|       70.85|         82.6|▁▆▇▇▇ |
|pop           |         0|             1| 29601212.32| 106157896.74| 60011.00| 2793664.00| 7023595.50| 19585221.75| 1318683096.0|▇▁▁▁▁ |
|gdpPercap     |         0|             1|     7215.33|      9857.45|   241.17|    1202.06|    3531.85|     9325.46|     113523.1|▇▁▁▁▁ |


:::
:::

::: {.cell}

```{.r .cell-code}
do.call(cbind, lapply(gap, summary))
```

::: {.cell-output .cell-output-stdout}

```
        country     continent   year      lifeExp            pop               
Min.    "1704"      "1704"      "1952"    "23.599"           "60011"           
1st Qu. "character" "character" "1965.75" "48.198"           "2793664"         
Median  "character" "character" "1979.5"  "60.7125"          "7023595.5"       
Mean    "1704"      "1704"      "1979.5"  "59.4744393661972" "29601212.3245306"
3rd Qu. "character" "character" "1993.25" "70.8455"          "19585221.75"     
Max.    "character" "character" "2007"    "82.603"           "1318683096"      
        gdpPercap         
Min.    "241.1658765"     
1st Qu. "1202.06030925"   
Median  "3531.8469885"    
Mean    "7215.32708121215"
3rd Qu. "9325.462346"     
Max.    "113523.1329"     
```


:::
:::



## Adding a figure of gapminder



::: {.cell}

```{.r .cell-code}
ggplot(gap,
       aes(x = year,
           y = lifeExp,
           group = country)) +
  geom_line() + 
  facet_wrap(~continent,
             ncol = 1) + 
  theme_minimal()
```

::: {.cell-output-display}
![A visual summary of the gapminder data. We learn that overall, life expectancy has (on average) increased over time, but there are some countries where life expectancy has dropped and had large fluctuations.](02-qmd-figures-chunks_files/figure-html/fig-gg-gap-1.jpeg){#fig-gg-gap}
:::
:::

::: {.cell}

```{.r .cell-code}
ggplot(gap,
       aes(x = year,
           y = gdpPercap,
           group = country)) +
  geom_line() + 
  facet_wrap(~continent,
             ncol = 1) + 
  theme_minimal()
```

::: {.cell-output-display}
![](02-qmd-figures-chunks_files/figure-html/unnamed-chunk-7-1.png)
:::
:::



As we can see in @fig-gg-gap.

# Tasks

- Change the fig-width, fig-height, and fig-format of the figure in plot-1
  - (hint: use tab-complete on the `#|`)
- Add an option to keep the markdown source code 
- Print the code for one of the figures, but not the other (hint: use `echo = `)

# Introduction

This is a simple analysis of the New York Air Quality Measurements using the R statistical programming language. As stated in the helpfile `?airquality`, this dataset contains:

> Daily air quality measurements in New York, May to September 1973.

And the dataset is sourced from:

> ... the New York State Department of Conservation (ozone data) and the National Weather Service (meteorological data).

It contains the following variables

- Ozone: Mean ozone in parts per billion from 1300 to 1500 hours at Roosevelt Island.
- Solar.R: Solar radiation in Langleys in the frequency band 4000–7700 Angstroms from 0800 to 1200 hours at Central Park.
- Wind: Average wind speed in miles per hour at 0700 and 1000 hours at LaGuardia Airport.
- Temp: Maximum daily temperature in degrees Fahrenheit at La Guardia Airport.
- Month: Month (1--12)
- Day: Day of month (1--31)

We are going to explore the relationship between solar radiation and other selected variables, solar radiation, wind, and temperature.

# Results

We can see that there is an interesting relationship between ozone and solar radiation in figure 1 below, plotted using ggplot2.



::: {.cell layout-align="center"}

```{.r .cell-code}
library(ggplot2)
ggplot(airquality,
       aes(x = Ozone,
           y = Solar.R)) + 
  geom_point()
```

::: {.cell-output .cell-output-stderr}

```
Warning: Removed 42 rows containing missing values or values outside the scale range
(`geom_point()`).
```


:::

::: {.cell-output-display}
![](02-qmd-figures-chunks_files/figure-html/figure-1-1.png){fig-align='center'}
:::
:::



We can also see that there is an interesting relationship between Ozone and temperature.



::: {.cell}

```{.r .cell-code}
ggplot(airquality,
       aes(x = Ozone,
           y = Temp)) + 
  geom_point()
```

::: {.cell-output .cell-output-stderr}

```
Warning: Removed 37 rows containing missing values or values outside the scale range
(`geom_point()`).
```


:::

::: {.cell-output-display}
![](02-qmd-figures-chunks_files/figure-html/figure-2-1.png)
:::
:::
