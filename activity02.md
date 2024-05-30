activity02
================
Cyril Owuor

### The data

The data we’re working with is from the OpenIntro site:
`https://www.openintro.org/data/csv/hfi.csv`. Here is the “about” page:
<https://www.openintro.org/data/index.php?data=hfi>.

In the R code chunk below titled `load-data`, you will type the code
that reads in the above linked CSV file by doing the following:

- Rather than downloading this file, uploading to RStudio, then reading
  it in, explore how to load this file directly from the provided URL
  with `readr::read_csv` (`{readr}` is part of `{tidyverse}`).
- Assign this data set into a data frame named `hfi` (short for “Human
  Freedom Index”).

``` r
hfi <- read_csv("hfi.csv")
```

    ## Rows: 1458 Columns: 123
    ## ── Column specification ────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (3): ISO_code, countries, region
    ## dbl (120): year, pf_rol_procedural, pf_rol_civil, pf_rol_criminal, pf_rol, p...
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

``` r
hfi
```

    ## # A tibble: 1,458 × 123
    ##     year ISO_code countries  region               pf_rol_procedural pf_rol_civil
    ##    <dbl> <chr>    <chr>      <chr>                            <dbl>        <dbl>
    ##  1  2016 ALB      Albania    Eastern Europe                    6.66         4.55
    ##  2  2016 DZA      Algeria    Middle East & North…             NA           NA   
    ##  3  2016 AGO      Angola     Sub-Saharan Africa               NA           NA   
    ##  4  2016 ARG      Argentina  Latin America & the…              7.10         5.79
    ##  5  2016 ARM      Armenia    Caucasus & Central …             NA           NA   
    ##  6  2016 AUS      Australia  Oceania                           8.44         7.53
    ##  7  2016 AUT      Austria    Western Europe                    8.97         7.87
    ##  8  2016 AZE      Azerbaijan Caucasus & Central …             NA           NA   
    ##  9  2016 BHS      Bahamas    Latin America & the…              6.93         6.01
    ## 10  2016 BHR      Bahrain    Middle East & North…             NA           NA   
    ## # ℹ 1,448 more rows
    ## # ℹ 117 more variables: pf_rol_criminal <dbl>, pf_rol <dbl>,
    ## #   pf_ss_homicide <dbl>, pf_ss_disappearances_disap <dbl>,
    ## #   pf_ss_disappearances_violent <dbl>, pf_ss_disappearances_organized <dbl>,
    ## #   pf_ss_disappearances_fatalities <dbl>, pf_ss_disappearances_injuries <dbl>,
    ## #   pf_ss_disappearances <dbl>, pf_ss_women_fgm <dbl>,
    ## #   pf_ss_women_missing <dbl>, pf_ss_women_inheritance_widows <dbl>, …

1.  What are the dimensions of the dataset? What does each row
    represent?

``` r
dimensions <- dim(hfi)
rows <- dimensions[1]
columns <- dimensions[2]

# Print the dimensions
cat("The dataset has", rows, "rows and", columns, "columns.\n")
```

    ## The dataset has 1458 rows and 123 columns.

The dataset spans a lot of years. We are only interested in data from
year 2016. In the R code chunk below titled `hfi-2016`, type the code
that does the following:

- Filter the data `hfi` data frame for year 2016, and
- Assigns the result to a data frame named `hfi_2016`.

``` r
library(dplyr)

# Filter the data for year 2016 and assign it to hfi_2016
hfi_2016 <- hfi |>
  filter(year == 2016)
hfi_2016
```

    ## # A tibble: 162 × 123
    ##     year ISO_code countries  region               pf_rol_procedural pf_rol_civil
    ##    <dbl> <chr>    <chr>      <chr>                            <dbl>        <dbl>
    ##  1  2016 ALB      Albania    Eastern Europe                    6.66         4.55
    ##  2  2016 DZA      Algeria    Middle East & North…             NA           NA   
    ##  3  2016 AGO      Angola     Sub-Saharan Africa               NA           NA   
    ##  4  2016 ARG      Argentina  Latin America & the…              7.10         5.79
    ##  5  2016 ARM      Armenia    Caucasus & Central …             NA           NA   
    ##  6  2016 AUS      Australia  Oceania                           8.44         7.53
    ##  7  2016 AUT      Austria    Western Europe                    8.97         7.87
    ##  8  2016 AZE      Azerbaijan Caucasus & Central …             NA           NA   
    ##  9  2016 BHS      Bahamas    Latin America & the…              6.93         6.01
    ## 10  2016 BHR      Bahrain    Middle East & North…             NA           NA   
    ## # ℹ 152 more rows
    ## # ℹ 117 more variables: pf_rol_criminal <dbl>, pf_rol <dbl>,
    ## #   pf_ss_homicide <dbl>, pf_ss_disappearances_disap <dbl>,
    ## #   pf_ss_disappearances_violent <dbl>, pf_ss_disappearances_organized <dbl>,
    ## #   pf_ss_disappearances_fatalities <dbl>, pf_ss_disappearances_injuries <dbl>,
    ## #   pf_ss_disappearances <dbl>, pf_ss_women_fgm <dbl>,
    ## #   pf_ss_women_missing <dbl>, pf_ss_women_inheritance_widows <dbl>, …

### 1. Identify our research question(s)

The research question is often defined by you (or your company, boss,
etc.). Today’s research question/goal is to predict a country’s personal
freedom score in 2016.

For this activity we want to explore the relationship between the
personal freedom score, `pf_score`, and the political pressures and
controls on media content index,`pf_expression_control`. Specifically,
we are going to use the political pressures and controls on media
content index to predict a country’s personal freedom score in 2016.

### 2. Explore the variables of interest

Answer the following questions (use your markdown skills) and complete
the following tasks.

2.  What type of plot would you use to display the distribution of the
    personal freedom scores, `pf_score`? Would this be the same type of
    plot to display the distribution of the political pressures and
    controls on media content index, `pf_expression_control`?

**A histogram would be an effective choice. A histogram allows us to see
the frequency distribution of pf_score across different ranges, helping
us understand its central tendency, spread, and the presence of any
skewness or outliers.**

- In the R code chunk below titled `univariable-plots`, type the R code
  that displays this plot for `pf_score`.
- In the R code chunk below titled `univariable-plots`, type the R code
  that displays this plot for `pf_expression_control`.

``` r
# Histogram for pf_score
ggplot(hfi_2016, aes(x = pf_score)) +
  geom_histogram(binwidth = 1, fill = "blue", color = "black") +
  labs(title = "Distribution of Personal Freedom Scores",
       x = "Personal Freedom Score",
       y = "Frequency") +
  theme_minimal()
```

![](activity02_files/figure-gfm/distribution-plots-1.png)<!-- -->

``` r
# Histogram for pf_expression_control
ggplot(hfi_2016, aes(x = pf_expression_control)) +
  geom_histogram(binwidth = 1, fill = "green", color = "black") +
  labs(title = "Distribution of Political Pressures and Controls on Media Content Index",
       x = "Political Pressures and Controls on Media Content Index",
       y = "Frequency") +
  theme_minimal()
```

![](activity02_files/figure-gfm/distribution-plots-2.png)<!-- --> 4.
Comment on each of these two distributions. Be sure to describe their
centers, spread, shape, and any potential outliers. **The pf_score is
left skewed and does not have an outlier. The pf_expression_control is a
bimodal and does not have an outlier.**

**The distribution of personal freedom score`pf_score` is left skewed
with a mean of 6.98 and a standard deviation of 1.49. This means that is
a small variance between personal freedom score and most people tend to
have a higher score with a few outliers.**

**The distribution for political pressures and controls is almost normal
with a mean of 4.98 and a standard deviation of 2.32. This means that
there is a greater variance between the index of political pressures and
controls on media. **

5.  What type of plot would you use to display the relationship between
    the personal freedom score, `pf_score`, and the political pressures
    and controls on media content index,`pf_expression_control`?

**To display the relationship between the personal freedom score
(pf_score) and the political pressures and controls on media content
index (pf_expression_control), a scatter plot would be an appropriate
choice. Scatter plots allow us to visualize the relationship between two
continuous variables and can help identify patterns, correlations, and
potential outliers.**

- In the R code chunk below titled `relationship-plot`, plot this
  relationship using the variable `pf_expression_control` as the
  predictor/explanatory variable.

``` r
# Scatter plot to display the relationship between pf_score and pf_expression_control
ggplot(hfi_2016, aes(x = pf_expression_control, y = pf_score)) +
  geom_point(color = "blue") +
  labs(title = "Relationship between Personal Freedom Score and Political Pressures and Controls on Media Content Index",
       x = "Political Pressures and Controls on Media Content Index",
       y = "Personal Freedom Score") +
  theme_minimal()
```

![](activity02_files/figure-gfm/relationship-plot-1.png)<!-- -->

4.  Does the relationship look linear? If you knew a country’s
    `pf_expression_control`, or its score out of 10, with 0 being the
    most, of political pressures and controls on media content, would
    you be comfortable using a linear model to predict the personal
    freedom score?

**Yes the relationship between `pf_score` and `pf_expression_control` is
linear with an increasing trend, this means that an increase
`pf_expression control` causes an increase in `pf_score`.**

#### Challenge

For each plot and using your `{dplyr}` skills, obtain the appropriate
numerical summary statistics and provide more detailed descriptions of
these plots. For example, in (4) you were asked to comment on the
center, spread, shape, and potential outliers. What measures
could/should be used to describe these? You might not know of one for
each of those terms.

What numerical summary would you use to describe the relationship
between two numerical variables? (hint: explore the `cor` function from
Base R)

``` r
# Compute the correlation coefficient between pf_expression_control and pf_score
correlation <- cor(hfi_2016$pf_expression_control, hfi_2016$pf_score)

# Print the correlation coeficient

print(correlation)
```

    ## [1] 0.8450646

## 3. Fit a simple linear regression model

Regardless of your response to (4), we will continue fitting a simple
linear regression (SLR) model to these data. The code that we will be
using to fit statistical models in this course use `{tidymodels}` - an
opinionated way to fit models in R - and this is likely new to most of
you. I will provide you with example code when I do not think you should
know what to do - i.e., anything `{tidymodels}` related.

To begin, we will create a `{parsnip}` specification for a linear model.

- In the code chunk below titled `parsnip-spec`, replace “verbatim” with
  “r” just before the code chunk title.

``` r
lm_spec <- linear_reg() %>%
  set_mode("regression") %>%
  set_engine("lm")

lm_spec
```

    ## Linear Regression Model Specification (regression)
    ## 
    ## Computational engine: lm

Note that the `set_mode("regression")` is really unnecessary/redundant
as linear models (`"lm"`) can only be regression models. It is better to
be explicit as we get comfortable with this new process. Remember that
you can type `?function_name` in the R **Console** to explore a
function’s help documentation.

The above code also outputs the `lm_spec` output. This code does not do
any calculations by itself, but rather specifies what we plan to do.

Using this specification, we can now fit our model:
$\texttt{pf\\_score} = \beta_0 + \beta_1 \times \texttt{pf\\_expression\\_control} + \varepsilon$.
Note, the “\$” portion in the previous sentence is LaTeX snytex which is
a math scripting (and other scripting) language. I do not expect you to
know this, but you will become more comfortable with this. Look at your
knitted document to see how this syntax appears.

- In the code chunk below titled `fit-lm`, replace “verbatim” with “r”
  just before the code chunk title.

``` r
slr_mod <- lm_spec %>% 
  fit(pf_score ~ pf_expression_control, data = hfi_2016)

tidy(slr_mod)
```

    ## # A tibble: 2 × 5
    ##   term                  estimate std.error statistic  p.value
    ##   <chr>                    <dbl>     <dbl>     <dbl>    <dbl>
    ## 1 (Intercept)              4.28     0.149       28.8 4.23e-65
    ## 2 pf_expression_control    0.542    0.0271      20.0 2.31e-45

The above code fits our SLR model, then provides a `tidy` parameter
estimates table.

5.  Using the `tidy` output, update the below formula with the estimated
    parameters. That is, replace “intercept” and “slope” with the
    appropriate values

$\widehat{\texttt{pf\\_score}} = 4.284 + 0.542 \times \texttt{pf\\_expression\\_control}$

6.  Interpret each of the estimated parameters from (5) in the context
    of this research question. That is, what do these values represent?

## Day 2

Hopefully, you were able to interpret the SLR model parameter estimates
(i.e., the *y*-intercept and slope) as follows:

> For countries with a `pf_expression_control` of 0 (those with the
> largest amount of political pressure on media content), we expect
> their mean personal freedom score to be 4.28.

> For every 1 unit increase in `pf_expression_control` (political
> pressure on media content index), we expect a country’s mean personal
> freedom score to increase 0.542 units.

### 4. Assessing

#### 4.A: Assess with your Day 1 model

To assess our model fit, we can use $R^2$ (the coefficient of
determination), the proportion of variability in the response variable
that is explained by the explanatory variable. We use `glance` from
`{broom}` (which is automatically loaded with `{tidymodels}` - `{broom}`
is also where `tidy` is from) to access this information.

- In the code chunk below titled `glance-lm`, replace “verbatim” with
  “r” just before the code chunk title.

``` r
glance(slr_mod)
```

    ## # A tibble: 1 × 12
    ##   r.squared adj.r.squared sigma statistic  p.value    df logLik   AIC   BIC
    ##       <dbl>         <dbl> <dbl>     <dbl>    <dbl> <dbl>  <dbl> <dbl> <dbl>
    ## 1     0.714         0.712 0.799      400. 2.31e-45     1  -193.  391.  400.
    ## # ℹ 3 more variables: deviance <dbl>, df.residual <int>, nobs <int>

After doing this and running the code, answer the following questions:

7.  What is the value of $R^2$ for this model? The $R^2$ of this model
    is 0.714.

8.  What does this value mean in the context of this model? Think about
    what would a “good” value of $R^2$ would be? Can/should this value
    be “perfect”?

**71% of the variance in `pf_score` can be explained by
`pf_expression_control`. This means that the model fits the data fairly
well.**

#### 4.B: Assess with test/train

You previously fit a model and evaluated it using the exact same data.
This is a bit of circular reasoning and does not provide much
information about the model’s performance. Now we will work through the
test/train process of fitting and assessing a simple linear regression
model.

Using the `diamonds` example provided to you in the Day 2 `README`, do
the following

- Create a new R code chunk and provide it with a descriptive tile
  (e.g., `train-test`).
- Set a seed.
- Create an initial 80-20 split of the `hfi_2016` dataset
- Using your initial split R object, assign the two splits into a
  training R object and a testing R object.

``` r
#set seed before random split
set.seed(1)

#put 80% of the data into the training set
hfi_split <- initial_split(hfi_2016,prop = 0.80)

# Assign the two splits to data frames  - with descriptive names
hfi_train <- training(hfi_split)
hfi_test <- testing(hfi_split)
```

Now, you will use your training dataset to fit a SLR model.

- In the code chunk below titled `train-fit-lm`, replace “verbatim” with
  “r” just before the code chunk title and update the data set to your
  training R object you just created.

``` r
slr_train <- lm_spec %>% 
  fit(pf_score ~ pf_expression_control, data = hfi_train)

tidy(slr_train)
```

    ## # A tibble: 2 × 5
    ##   term                  estimate std.error statistic  p.value
    ##   <chr>                    <dbl>     <dbl>     <dbl>    <dbl>
    ## 1 (Intercept)              4.17     0.166       25.2 3.14e-51
    ## 2 pf_expression_control    0.568    0.0305      18.6 4.32e-38

Notice that you can reuse the `lm_spec` specification because we are
still doing a linear model.

9.  Using the `tidy` output, update the below formula with the estimated
    parameters. That is, replace “intercept” and “slope” with the
    appropriate values

$\widehat{\texttt{pf\\_score}} = 4.321 + 0.536 \times \texttt{pf\\_expression\\_control}$

10. Interpret each of the estimated parameters from (10) in the context
    of this research question. That is, what do these values represent?

Now we will assess using the testing data set.

- In the code chunk below titled `train-fit-lm`, replace “verbatim” with
  “r” just before the code chunk title and update `data_test` to
  whatever R object you assigned your testing data to above.

``` r
test_aug <- augment(slr_train, new_data = hfi_test)
test_aug
```

    ## # A tibble: 33 × 125
    ##    .pred  .resid  year ISO_code countries  region pf_rol_procedural pf_rol_civil
    ##    <dbl>   <dbl> <dbl> <chr>    <chr>      <chr>              <dbl>        <dbl>
    ##  1  7.30  0.801   2016 ARG      Argentina  Latin…              7.10         5.79
    ##  2  6.59  0.324   2016 ARM      Armenia    Cauca…             NA           NA   
    ##  3  4.32  1.36    2016 AZE      Azerbaijan Cauca…             NA           NA   
    ##  4  8.29 -0.838   2016 BHS      Bahamas    Latin…              6.93         6.01
    ##  5  6.02 -0.718   2016 BGD      Bangladesh South…              2.33         3.71
    ##  6  8.43 -0.728   2016 BRD      Barbados   Latin…              7.67         6.52
    ##  7  5.88 -0.413   2016 CAF      Central A… Sub-S…             NA           NA   
    ##  8  5.31  1.47    2016 COG      Congo, Re… Sub-S…             NA           NA   
    ##  9  7.16 -0.0940  2016 CIV      Cote d'Iv… Sub-S…              2.99         5.19
    ## 10  9.29 -0.273   2016 EST      Estonia    Easte…              8.77         7.85
    ## # ℹ 23 more rows
    ## # ℹ 117 more variables: pf_rol_criminal <dbl>, pf_rol <dbl>,
    ## #   pf_ss_homicide <dbl>, pf_ss_disappearances_disap <dbl>,
    ## #   pf_ss_disappearances_violent <dbl>, pf_ss_disappearances_organized <dbl>,
    ## #   pf_ss_disappearances_fatalities <dbl>, pf_ss_disappearances_injuries <dbl>,
    ## #   pf_ss_disappearances <dbl>, pf_ss_women_fgm <dbl>,
    ## #   pf_ss_women_missing <dbl>, pf_ss_women_inheritance_widows <dbl>, …

This takes your SLR model and applies it to your testing data.

![check-in](../README-img/noun-magnifying-glass.png) **Check in**

Look at the various information produced by this code. Can you identify
what each column represents?

The `.pred` column in this output can also be obtained by using
`predict` (i.e., `predict(slr_fit, new_data = data_test)`)

11. Now, using your responses to (7) and (8) as an example, assess how
    well your model fits your testing data. Compare your results here to
    your results from your Day 1 of this activity. Did this model
    perform any differently?

### Model diagnostics

To assess whether the linear model is reliable, we should check for (1)
linearity, (2) nearly normal residuals, and (3) constant variability.
Note that the normal residuals is not really necessary for all models
(sometimes we simply want to describe a relationship for the data that
we have or population-level data, where statistical inference is not
appropriate/necessary).

In order to do these checks we need access to the fitted (predicted)
values and the residuals. We can use `broom::augment` to calculate
these.

- In the code chunk below titled `augment`, replace “verbatim” with “r”
  just before the code chunk title and update `data_train` to whatever R
  object you assigned your training data to above.

``` r
train_aug <- augment(slr_train, new_data = hfi_test)
train_aug
```

    ## # A tibble: 33 × 125
    ##    .pred  .resid  year ISO_code countries  region pf_rol_procedural pf_rol_civil
    ##    <dbl>   <dbl> <dbl> <chr>    <chr>      <chr>              <dbl>        <dbl>
    ##  1  7.30  0.801   2016 ARG      Argentina  Latin…              7.10         5.79
    ##  2  6.59  0.324   2016 ARM      Armenia    Cauca…             NA           NA   
    ##  3  4.32  1.36    2016 AZE      Azerbaijan Cauca…             NA           NA   
    ##  4  8.29 -0.838   2016 BHS      Bahamas    Latin…              6.93         6.01
    ##  5  6.02 -0.718   2016 BGD      Bangladesh South…              2.33         3.71
    ##  6  8.43 -0.728   2016 BRD      Barbados   Latin…              7.67         6.52
    ##  7  5.88 -0.413   2016 CAF      Central A… Sub-S…             NA           NA   
    ##  8  5.31  1.47    2016 COG      Congo, Re… Sub-S…             NA           NA   
    ##  9  7.16 -0.0940  2016 CIV      Cote d'Iv… Sub-S…              2.99         5.19
    ## 10  9.29 -0.273   2016 EST      Estonia    Easte…              8.77         7.85
    ## # ℹ 23 more rows
    ## # ℹ 117 more variables: pf_rol_criminal <dbl>, pf_rol <dbl>,
    ## #   pf_ss_homicide <dbl>, pf_ss_disappearances_disap <dbl>,
    ## #   pf_ss_disappearances_violent <dbl>, pf_ss_disappearances_organized <dbl>,
    ## #   pf_ss_disappearances_fatalities <dbl>, pf_ss_disappearances_injuries <dbl>,
    ## #   pf_ss_disappearances <dbl>, pf_ss_women_fgm <dbl>,
    ## #   pf_ss_women_missing <dbl>, pf_ss_women_inheritance_widows <dbl>, …

**Linearity**: You already checked if the relationship between
`pf_score` and `pf_expression_control` is linear using a scatterplot. We
should also verify this condition with a plot of the residuals
vs. fitted (predicted) values.

- In the code chunk below titled `fitted-residual`, replace “verbatim”
  with “r” just before the code chunk title.

``` r
ggplot(data = train_aug, aes(x = .pred, y = .resid)) +
  geom_point() +
  geom_hline(yintercept = 0, linetype = "dashed", color = "red") +
  xlab("Fitted values") +
  ylab("Residuals")
```

![](activity02_files/figure-gfm/fitted-1.png)<!-- -->

Notice here that `train_aug` can also serve as a data set because stored
within it are the fitted values ($\hat{y}$) and the residuals. Also note
that we are getting fancy with the code here. After creating the
scatterplot on the first layer (first line of code), we overlay a red
horizontal dashed line at $y = 0$ (to help us check whether the
residuals are distributed around 0), and we also rename the axis labels
to be more informative.

Answer the following question:

11. Is there any apparent pattern in the residuals plot? What does this
    indicate about the linearity of the relationship between the two
    variables?

**The assumption of linearity has been met as we can see that the points
on the residual plot are randomly distributed and have no pattern.**

**Nearly normal residuals**: To check this condition, we can look at a
histogram of the residuals.

- In the code chunk below titled `residual-histogram`, replace
  “verbatim” with “r” just before the code chunk title.

``` r
ggplot(data = train_aug, aes(x = .resid)) +
  geom_histogram(binwidth = 0.25) +
  xlab("Residuals")
```

![](activity02_files/figure-gfm/fitted-residual-1.png)<!-- -->

Answer the following question:

12. Based on the histogram, does the nearly normal residuals condition
    appear to be violated? Why or why not?

**From the histogram above, it shows that the condition for normality
has been violated, this can be seen by the shape of the histogram which
does not have a bell shaped.**

**Constant variability**:

13. Based on the residuals vs. fitted plot, does the constant
    variability condition appear to be violated? Why or why not?

**The assumption of constant variance has been met. The points on the
residual plots appear to be randomly distributed.**

## Attribution

This document is based on labs from
[OpenIntro](https://www.openintro.org/).

<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/"><img src="https://i.creativecommons.org/l/by-sa/4.0/88x31.png" alt="Creative Commons License" style="border-width:0"/></a><br />This
work is licensed under a
<a rel="license" href="http://creativecommons.org/licenses/by-sa/4.0/">Creative
Commons Attribution-ShareAlike 4.0 International License</a>.
