Star Wars fisher logbooks - data wrangling
================
Gavin Fay <br> Acknowledgements: Mine Çetinkaya-Rundel

``` r
library(tidyverse)
library(skimr)
```

``` r
logbook <- read_csv("sw_fdd_logbook.csv")
```

## Exercises

### Exercise 1.

Warm up! Take a look at an overview of the data with the `skim()`
function.

**Note:** I already gave you the answer to this exercise. You just need
to knit the document and view the output. A definition of all variables
is given in the \[Data dictionary\] section at the end, though you don’t
need to familiarize yourself with all variables in order to work through
these exercises.

``` r
skim(logbook)
```

|                                                  |         |
|:-------------------------------------------------|:--------|
| Name                                             | logbook |
| Number of rows                                   | 152000  |
| Number of columns                                | 7       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_   |         |
| Column type frequency:                           |         |
| character                                        | 2       |
| numeric                                          | 5       |
| \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ |         |
| Group variables                                  | None    |

Data summary

**Variable type: character**

| skim\_variable | n\_missing | complete\_rate | min | max | empty | n\_unique | whitespace |
|:---------------|-----------:|---------------:|----:|----:|------:|----------:|-----------:|
| vessel         |          0 |              1 |   4 |  18 |     0 |        20 |          0 |
| world          |          0 |              1 |   6 |  12 |     0 |        10 |          0 |

**Variable type: numeric**

| skim\_variable | n\_missing | complete\_rate |    mean |    sd |      p0 |     p25 |     p50 |     p75 |    p100 | hist  |
|:---------------|-----------:|---------------:|--------:|------:|--------:|--------:|--------:|--------:|--------:|:------|
| year           |          0 |              1 | 1986.00 |  5.48 | 1977.00 | 1981.00 | 1986.00 | 1991.00 | 1995.00 | ▇▇▆▇▇ |
| quarter        |          0 |              1 |    2.50 |  1.12 |    1.00 |    1.75 |    2.50 |    3.25 |    4.00 | ▇▇▁▇▇ |
| towmin         |          0 |              1 |   45.92 |  9.32 |   18.41 |   39.30 |   45.01 |   51.51 |  110.65 | ▂▇▂▁▁ |
| depth          |          0 |              1 |  102.05 | 20.63 |   41.49 |   87.37 |  100.05 |  114.49 |  240.51 | ▂▇▂▁▁ |
| kept           |          0 |              1 |   12.83 |  6.17 |    2.09 |    8.46 |   11.53 |   15.75 |  101.66 | ▇▁▁▁▁ |

### Exercise 2.

What is the duration of fishing tows? Let’s see…

Fill in the blanks for filtering for fishing tows where the world was
**not** Kashyyyk (`world` code `"Kashyyyk"`) and the `towmin` is less
than 40 minutes in duration.

**Note:** You will need to set `eval=TRUE` when you have an answer you
want to try out.

``` r
logbook %>%
  filter(
    country ____ "Kashyyyk", 
    lead_time ____ ____
    )
```

### Exercise 3.

How many tows were at least 55 minutes long **or** were at depths of at
least 120 m?

In the following chunk, replace

-   `[AT LEAST]` with the logical operator for “at least” (in two
    places)
-   `[OR]` with the logical operator for “or”

**Note:** You will need to set `eval=TRUE` when you have an answer you
want to try out.

``` r
logbook %>%
  filter(
    towmin [AT LEAST] 55 [OR] depth [AT LEAST] 120
    )
```

### Exercise 4.

Do you think the FV Lando Calrissian is more likely to fish deep (at
least 120m) or have a high catch (at least 7kg) than the FV Boba Fett?
Test your intuition. Using `filter()` determine the number of tows by
the FV Lando Calrissian that have a depth of at least 120m **or** that
caught at least 7kg. Then, do the same for the FV Boba Fett, and compare
the numbers of rows in the resulting filtered data frames.

``` r
# add code here
# pay attention to correctness and code style
```

``` r
# add code here
# pay attention to correctness and code style
```

### Exercise 5.

The logbook data do not contain information about the type of vessel
(‘starship’) or the species of the crew. This information is in our
permit table that contains the vessel characteristics for each year of
fishing, but not individual tow data.

Read in the permit data, and review it’s properties and dimensions
(number of rows and columns). Then create a single dataset for the tow
data that links the vessel information in the permit table to the
logbook data. Verify that this new data set has been created
successfully.

**Note:** You will need to set `eval=TRUE` when you have an answer you
want to try out.

``` r
permit <- ______("sw_fdd_permit.csv")

______(permit)

full_data <- logbook %>% 
   ________
```

### Exercise 6.

Create a frequency table of the `species` of crew in tows. Display the
results in descending order so the most common observation (species) is
on top. What is the most common species of crew in this dataset? Are
there any surprising results?

**Note:** Don’t forget to label your R chunk as well (where it says
`label-me-1`). Your label should be short, informative, and shouldn’t
include spaces. It also shouldn’t repeat a previous label, otherwise R
Markdown will give you an error about repeated R chunk labels.

``` r
# add code here
# pay attention to correctness and code style
```

### Exercise 7.

Repeat Exercise 6, once for Imperial shuttle vessels (`starship` is
“Imperial shuttle”) and once for all other vessel types (value in
`starship` is something else). What does this reveal about the
surprising results you spotted in the previous exercise?

**Note:** Don’t forget to label your R chunk as well (where it says
`label-me-2`).

``` r
# add code here
# pay attention to correctness and code style
```

### Exercise 8.

Calculate minimum, mean, median, and maximum average catch rate (kept
per hour) grouped by `vessel` so that you can get these statistics
separately for each of the FVs. Which fishing vessels have higher catch
rates on average?

``` r
# add code here
# pay attention to correctness and code style
```

### Exercise 9.

Create a visualization to show how the mean catch rate for each of the
fishing vessels (`vessel`) changes over time. **Stretch goal** extend
your graph to also show the effects of vessel type (`starship`) What
conclusions can you draw?

**Hint:** You may want to create a summary data frame containing the
information you want to plot before passing it to your `ggplot()` call.

**Super-stretch goal** add information to your graph to also reflect
fishing depths.

``` r
# add code here
# pay attention to correctness and code style
```

## Data dictionaries

Below is the full data dictionary.

### Logbook data

| variable | class     | description                                 |
|:---------|:----------|:--------------------------------------------|
| year     | double    | Year in which tow took place                |
| vessel   | character | Name of the fishing vessel                  |
| world    | character | Name of the world where the tow tool place  |
| quarter  | double    | quarter of the year when the tow took place |
| towmin   | double    | duration of the tow in minutes              |
| depth    | double    | depth (in m) of the tow                     |
| kept     | double    | weight of fish (in kg) kept from the tow    |

### Permit data

| variable | class     | description                  |
|:---------|:----------|:-----------------------------|
| year     | double    | Year in which tow took place |
| vessel   | character | Name of the fishing vessel   |
| height   | double    | height (in m) of the vessel  |
| mass     | double    | mass (in tons) of the vessel |
| species  | character | species of the crew          |
| starship | character | type of vessel               |
