# Motherhood and the Gender Pay Gap in the European Union  in R

## Overview

This project was conducted as part of the **Conducting an Empirical Project** course during my Master's studies in **Econometrics and Statistics – Data Science**.

The study investigates the relationship between **fertility and the gender pay gap** across European Union countries.

Using harmonized **Eurostat data**, the analysis covers **27 EU countries over the period 2010–2023**. The empirical strategy combines data preparation, descriptive statistics, graphical analysis, panel-data econometrics and diagnostic testing.

The main empirical question is:

> **To what extent is fertility associated with the gender pay gap in the European Union?**

Motherhood is not directly observed at the individual level. Instead, the study uses the **fertility rate as a macroeconomic proxy for motherhood**.

---

## Research Question

The project examines whether countries and years with higher fertility rates are associated with larger gender pay gaps, while controlling for other dimensions of women's position in the labour market.

The analysis focuses on four main explanatory variables:

* Fertility rate
* Share of women in managerial positions
* Female employment rate
* Employment of adults according to the number of children and age of the youngest child

The dependent variable is the **gender pay gap**, expressed as a percentage.

---

## Research Hypothesis

The research hypothesis is that:

> An increase in the fertility rate is associated with an increase in the gender pay gap.

This hypothesis is motivated by mechanisms discussed in the literature, including career interruptions, part-time employment and differences in career progression following parenthood.

The analysis is explicitly **associational rather than causal**, since fertility is an aggregate indicator and does not directly measure individual women's motherhood or career trajectories.

---

## Data

The study uses data from **Eurostat**.

The initial panel covers:

* **27 European Union countries**
* **2010–2023**
* Country-year observations

After handling missing values, the final estimation sample contains **311 observations**.

### Main variables

| Variable                      | Description                                                                                   |
| ----------------------------- | --------------------------------------------------------------------------------------------- |
| Gender pay gap                | Difference between men's and women's average gross hourly earnings, expressed as a percentage |
| Fertility rate                | Average number of children a woman would have under observed age-specific fertility rates     |
| Women in managerial positions | Share of women in selected managerial/directorial positions                                   |
| Female employment rate        | Percentage of working-age women in employment                                                 |
| Adult employment              | Employment measure differentiated by number of children and age of the youngest child         |

---

## Data Preparation

Several Eurostat datasets were imported and processed in R.

The project combines five main data sources:

* Gender pay gap
* Fertility rate
* Women in managerial positions
* Adult employment by household characteristics
* Female employment

### Data cleaning steps

The preprocessing workflow includes:

* Importing Eurostat CSV files
* Inspecting dataset structures
* Selecting relevant variables
* Filtering the study period
* Handling missing observations
* Aggregating observations by country and year
* Constructing a country-year panel
* Merging the different datasets
* Converting `NaN` values to `NA`
* Removing incomplete observations before estimation

For the gender pay gap, observations from different economic activities were aggregated by country and year.

For the managerial-position variable, the analysis retains the `BRD` professional-position category because of missing observations in the `EXEC` category.

---

## Descriptive Statistics

The final dataset contains 311 observations.

The descriptive analysis reports:

| Variable                      |   Mean | Standard Deviation | Minimum | Maximum |
| ----------------------------- | -----: | -----------------: | ------: | ------: |
| Gender pay gap                | 13.26% |               4.44 |    1.67 |   25.96 |
| Fertility rate                |   1.53 |               0.19 |    1.06 |    2.05 |
| Women in managerial positions | 20.62% |              10.46 |    2.10 |   46.10 |
| Female employment rate        | 62.14% |               8.34 |   39.50 |   78.90 |
| Adult employment              | 35.70% |              21.13 |    6.70 |   92.30 |

These statistics highlight substantial heterogeneity across countries and years.

---

## Exploratory Data Analysis

The project includes several graphical analyses developed with **ggplot2**.

### Gender Pay Gap Distribution

A histogram and density curve are used to examine the distribution of the gender pay gap across the sample.

### Evolution Over Time

The average gender pay gap is calculated for each year to examine its evolution across the European Union.

The study reports a decline in the average gender pay gap from approximately **15.3% in 2010 to 11.1% in 2023**.

### Country Comparison

The evolution of the gender pay gap is also visualized for selected countries:

* France
* Germany
* Spain
* Sweden

### Explanatory Variables

The project also examines the evolution of:

* Fertility
* Women's representation in managerial positions
* Female employment
* Adult employment

These visualizations provide an overview of the main trends before estimating the econometric models.

---

## Empirical Strategy

The main empirical model is a **fixed-effects panel regression**.

The model is specified as:

```text
Gender Pay Gap_it =
β₀
+ β₁ Fertility Rate_it
+ δ₁ Women Managers_it
+ δ₂ Female Employment_it
+ δ₃ Adult Employment_it
+ α_i
+ ε_it
```

where:

* `i` represents the country
* `t` represents the year
* `α_i` represents country fixed effects
* `ε_it` represents the error term

The fixed-effects specification focuses on **within-country variation over time**, controlling for time-invariant characteristics specific to each country.

---

## Econometric Models

### Simple Fixed-Effects Model

A first model examines the relationship between:

* Fertility rate
* Gender pay gap

using a fixed-effects panel specification.

### Multiple Fixed-Effects Model

The main model adds three control variables:

```text
Gender Pay Gap ~
Fertility Rate
+ Women in Managerial Positions
+ Female Employment
+ Adult Employment
```

The model is estimated using the `plm` package in R.

---

## Econometric Diagnostics

Several diagnostic tests are performed to assess the quality of the empirical model.

### Multicollinearity

Variance Inflation Factors (**VIF**) are calculated to assess potential multicollinearity between explanatory variables.

### Residual Normality

A **Shapiro–Wilk test** and a Q-Q plot are used to examine the distribution of residuals.

### Heteroskedasticity

The **Breusch–Pagan test** is used to detect heteroskedasticity.

### Serial Correlation

A **Wooldridge test** is performed to investigate autocorrelation in the panel residuals.

### Cross-Sectional Dependence

The **Pesaran CD test** is used to investigate dependence between cross-sectional units.

The analysis identifies heteroskedasticity and autocorrelation. Therefore, the project also reports results using **robust standard errors**.

---

## Main Results

The fixed-effects estimation reports a positive association between fertility and the gender pay gap.

The estimated coefficient for the fertility rate is approximately:

**5.794**

with statistical significance in both the standard and robust specifications.

Within the model, a one-unit increase in the fertility rate is associated with an increase of approximately **5.79 percentage points in the gender pay gap**, holding the other included variables constant.

The model also reports negative coefficients for:

* Women's representation in managerial positions
* Female employment rate

The coefficient for the adult-employment variable is negative but is not statistically significant in the reported specifications.

The fixed-effects model reports:

* **311 observations**
* **R² = 0.537**
* **Adjusted R² = 0.489**
* Country fixed effects

The results should be interpreted as **statistical associations rather than causal effects**.

---

## Interpretation

The positive association between fertility and the gender pay gap is consistent with the research hypothesis and with the mechanisms discussed in the literature on the **motherhood penalty**.

However, fertility is an aggregate demographic indicator and does not directly measure individual motherhood, career interruptions or individual wage trajectories.

Consequently, the estimated coefficient should not be interpreted as evidence that fertility itself mechanically causes the gender pay gap.

The negative associations observed for female employment and women's representation in managerial positions provide additional evidence on the relationship between women's labour-market integration and wage inequality within the empirical framework.

---

## Limitations

Several limitations are identified in the study.

### Aggregate Measure of Motherhood

Fertility is used as a proxy for motherhood at the country level. It does not directly capture individual mothers' employment histories, working hours or career interruptions.

### Omitted Variables

The model does not include all potentially relevant factors, such as cultural and social norms or country-specific institutional characteristics that may influence both fertility and gender wage inequality.

### Time Period

The study covers 2010–2023, which provides a relatively limited period for analysing long-term structural changes.

### Measurement of Women in Managerial Positions

The selected indicator focuses on specific managerial/directorial positions and does not fully capture women's representation in leadership positions across the entire private and public economy.

### Causal Interpretation

The empirical strategy identifies associations within the panel-data framework but does not establish a causal effect of fertility on the gender pay gap.

---

## Technologies

| Category                | Tools                          |
| ----------------------- | ------------------------------ |
| Programming             | R                              |
| Statistical environment | RStudio                        |
| Data manipulation       | tidyverse, dplyr, tidyr, readr |
| Data visualization      | ggplot2                        |
| Panel econometrics      | plm                            |
| Statistical testing     | lmtest, sandwich, car          |
| Regression tables       | modelsummary, gt               |
| Plot composition        | patchwork, gridExtra           |
| Data source             | Eurostat                       |

---

## Skills Demonstrated

This project demonstrates practical skills in:

* Empirical research design
* Economic literature review
* Eurostat data collection
* Data cleaning and preprocessing
* Panel-data construction
* Data integration
* Descriptive statistics
* Exploratory data analysis
* Data visualization
* Fixed-effects regression
* Panel-data econometrics
* Robust standard errors
* Econometric diagnostic testing
* Statistical inference
* Interpretation of regression results
* Reproducible analysis with R

---

## Project Structure

```text
Motherhood-Gender-Pay-Gap/
│
├── AMOUSSOU Orianne_GARANGO Bintou_TOGNIBO Hariane.r
│
├── AMOUSSOU Orianne_GARANGO Bintou_TOGNIBO Hariane.pdf
│
└── data/
    └── raw/
        ├── demo_frate.csv
        ├── earn_gr_gpgr2.csv
        ├── lfsi_emp_a.csv
        ├── lfst_hhptechi.csv
        └── sdg_05_60.csv
```

---

## Academic Context

This project was completed as part of the **Conducting an Empirical Project** course during the **2025–2026 academic year**.

The project combines economic research, Eurostat data and panel-data econometrics to investigate gender inequalities in the European labour market.

---

## Authors

* **Orianne AMOUSSOU**
* **Bintou Daouda GARANGO**
* **Hariane TOGNIBO**

---

## Data Source

All empirical indicators used in the analysis are obtained from **Eurostat**.

The analysis and statistical processing were performed using **R/RStudio**.

