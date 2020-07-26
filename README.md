<!-- README.md is generated from README.Rmd. Please edit that file -->
OpenCaseStudies
===============

[![Build
Status](https://travis-ci.org/opencasestudies/ocs-right-to-carry-case-study.svg?branch=master)](https://travis-ci.org/opencasestudies/ocs-right-to-carry-case-study)

### Disclaimer

The purpose of the [Open Case
Studies](https://opencasestudies.github.io) project is **to demonstrate
the use of various data science methods, tools, and software in the
context of messy, real-world data**. A given case study does not cover
all aspects of the research process, is not claiming to be the most
appropriate way to analyze a given dataset, and should not be used in
the context of making policy decisions without external consultation
from scientific experts.

### License

This case study is part of the
[OpenCaseStudies](https://opencasestudies.github.io) project. This work
is licensed under the Creative Commons Attribution-NonCommercial 3.0
([CC BY-NC 3.0](https://creativecommons.org/licenses/by-nc/3.0/us/))
United States License.

### Citation

To cite this case study:

Wright, Carrie, and Ontiveros, Michael and Jager, Leah and Taub,
Margaret and Hicks, Stephanie. (2020).
<a href="https://github.com/opencasestudies/ocs-right-to-carry-case-study" class="uri">https://github.com/opencasestudies/ocs-right-to-carry-case-study</a>.
Vaping Behaviors in American Youth (Version v1.0.0).

### Acknowledgements

We would like to acknowledge [Daniel
Webster](https://www.jhsph.edu/faculty/directory/profile/739/daniel-webster)
for assisting in framing the major direction of the case study.

We would also like to acknowledge the [Bloomberg American Health
Initiative](https://americanhealth.jhu.edu/) for funding this work.

### Title

Examination of Multicollinearity Influence on Inference Using
Right-to-Carry Gun Law and Violent Crime Data

### Motivation

The influence of the implementation of less restrictive right-to-carry
gun laws on violent crime is a historically controversial topic. One
reason for the contriversy, is concern that some earlier reports examing
this topic may have used methods that were inappropriate.

One of the major concerns is that an earlier report included multiple
demographic variables that were collinear with one another. This
resulted in different a very coefficient estimate for right-to-carry gun
law adoption than other reports that did not include colinear varaibles.
This phenomenon is called
[multicollinearity](https://en.wikipedia.org/wiki/Multicollinearity),
and it can result in abberant findings for particular explanatory
variables, despite not altering the overall predictive power of a model.

In this case study we use data peform simplified analyses similar to
those of reports on this topic to explore the influence of
multicolinearity on coeffcient estimate stability. We however, do not
recreate the previous analyses. The reports that we use as a guide for
our analysis are:

1.  John J. Donohue et al., Right‐to‐Carry Laws and Violent Crime: A
    Comprehensive Assessment Using Panel Data and a State‐Level
    Synthetic Control Analysis. *Journal of Empirical Legal Studies*,
    16,2 (2019).

2.  David B. Mustard & John Lott. Crime, Deterrence, and Right-to-Carry
    Concealed Handguns. *Coase-Sandor Institute for Law & Economics*
    Working Paper No. 41, (1996).

### Motivating question

1.  How does the inclusion of different numbers of age groups influence
    the results of an analysis of right to carry laws and violence
    rates?

### Data

In this case study, we perform analyses similar to those in
<a href="https://www.nber.org/papers/w23510.pdf" target="_blank">Donohue, et al.</a>
article and the
<a href="https://chicagounbound.uchicago.edu/cgi/viewcontent.cgi?article=1150&amp;context=law_and_economics" target="_blank">Lott and Mustard</a>
article, however **we do not try to recreate them**, instead we perform
simplified analyses to allow us to focus on multicolinearity.

Therefore we use a subset of the explanatory variables used by each
article including: 1) Data about state demographics in terms of
population compositions for age, sex, race, as well as overall
population values from the US Census Bureau:

<table>
<colgroup>
<col style="width: 43%" />
<col style="width: 56%" />
</colgroup>
<thead>
<tr class="header">
<th>Data</th>
<th>Link</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>years 1977 to 1979</strong></td>
<td><a href="https://www2.census.gov/programs-surveys/popest/tables/1900-1980/state/asrh/">link</a></td>
</tr>
<tr class="even">
<td><strong>years 1980 to 1989</strong></td>
<td><a href="https://www2.census.gov/programs-surveys/popest/tables/1980-1990/counties/asrh/">link</a> * county data was used for this decade which also has state information</td>
</tr>
<tr class="odd">
<td><strong>years 1990 to 1999</strong></td>
<td><a href="https://www2.census.gov/programs-surveys/popest/tables/1990-2000/state/asrh/">link</a></td>
</tr>
<tr class="even">
<td><strong>years 2000 to 2010</strong></td>
<td><a href="https://www.census.gov/data/datasets/time-series/demo/popest/intercensal-2000-2010-state.html">link</a> <br> <a href="https://www2.census.gov/programs-surveys/popest/technical-documentation/file-layouts/2000-2010/intercensal/state/st-est00int-alldata.pdf" target="_blank">technical documentation</a></td>
</tr>
</tbody>
</table>

Six demographic variables are created for the
<a href="https://www.nber.org/papers/w23510.pdf" target="_blank">Donohue, et al.</a>-like
analysis and 36 were created for the
<a href="https://chicagounbound.uchicago.edu/cgi/viewcontent.cgi?article=1150&amp;context=law_and_economics" target="_blank">Lott and Mustard</a>-like
analysis.

To use this data, we also need [Federal Information Processing Standard
(FIPS) state
codes](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standard_state_code){target="\_blank",
to identify what demographic data corresponds to what state. This is
also available from the
<a href="https://www.census.gov/geographies/reference-files/2014/demo/popest/2014-geocodes-state.html" target="_blank">US Census Bureau</a>.

1.  Police staffing data, which was downloaded from the [Federal Bureau
    of
    Investigation](https://crime-data-explorer.fr.cloud.gov/downloads-and-docs).

2.  Unemployment data, which was downloaded from the [U.S. Bureau of
    Labor Statistics](https://data.bls.gov/cgi-bin/dsrv?la).

3.  Poverty data, extracted from Table 21 from this [US Census Bureau
    Poverty
    Data](https://www.census.gov/data/tables/time-series/demo/income-poverty/historical-poverty-people.html)

4.  Right-to-carry law data, which is available in a table in the
    [Donohue paper](https://www.nber.org/papers/w23510.pdf)
    {target="\_blank"}.

Finally our outcome of interest is violent crime rates. The violent
crime data was downloaded from the [FBI uniform crime reporting
system](https://www.ucrdatatool.gov/Search/Crime/State/StatebyState.cfm)

#### Learning Objectives

The skills, methods, and concepts that students will be familiar with by
the end of this case study are:

<u>**Statistical Learning Objectives:**</u>

1.  what multicollinearity is and how it can influence linear regression
    coefficients  
2.  how to look for the presence of multicollinarity and determine the
    severity
3.  the difference between multicollinearity and correlation

<u>**Data science Learning Objectives:**</u>

1.  data import of many different file types with special cases
    (`readr`, `readxl`, `pdftools`)
2.  joining data from multiple sources (`dplyr`)  
3.  working with character strings (`stringr`)
4.  data comparisons (`dplyr` and `janitor`)
5.  reshaping data into different formats (`tidyr`)  
6.  visualizations (`ggplot2`)
7.  perform iterative simulations (`rsample`)

#### Data import

In this case study particularly covers many different types of data
import. We cover data import using the Tidyverse `readr` package to
import the various types of text files, the Tidyverse `readxl` package
to import excel files, and the Tidyverse `pdftools` package to import a
PDF file. We demonstrate special cases where header rows need to be
skipped, or colum data types need to be specified. We also use the the
`list.files()` base function together with the `map()` function of the
Tidyverse `purrr` package to efficiently perform data importation of
multiple files with one command.

#### Data wrangling

This case study is covers many details about wrangling data from excel
files with unusual header structures and with similar data in multiple
tables within the same file. This involves using the `stringr` package
to split, subset, detect, extract, and modify patterns of text. This
also involves using the `tidyr` package to change data shape and using
the `dplyr` package to summarise, select, filter, modify, and join data.
They case study also covers using various `map_*()` functions of the
`purrr` package to perform functions across tibbles within lists and the
`across()` function of the `dplyr` package to perform functions across
columns of an individual tibble. This case study provides especially
diverse material about data wrangling.

#### Data Visualization

This case study demonstrates how to make correaltion plots and scatter
plots with error bars. We also show how to add labels and arrows to
plots.

### Analysis

This case study covers balanced panel regression model data analysis
with fixed effects. In doing so we provide an introduction to
longitudinal analysis in general, as well as use of the `plm` package.
We also show how to calculate [Variance inflation factor
(VIF)](https://en.wikipedia.org/wiki/Variance_inflation_factor) values
using the `car` package to quantify the severity of multicollinearity.
As another assesment of multicollinearity, we demonstrate how to perform
simulations to evaluate the stability of coefficient estimates.

### Other notes and resources

<a href="https://www.tidyverse.org/" target="_blank">Tidyverse</a>  
<a href="https://r4ds.had.co.nz/functions.html" target="_blank">Writing functions</a>  
<a href="https://www.bmj.com/about-bmj/resources-readers/publications/epidemiology-uninitiated/7-longitudinal-studies" target="_blank">Longitudinal studies</a>  
<a href="https://en.wikipedia.org/wiki/Panel_data" target="_blank">Panel data</a>  
<a href="https://en.wikipedia.org/wiki/Confidence_interval" target="_blank">Confidence intervals</a>  
<a href="https://en.wikipedia.org/wiki/Linear_regression" target="_blank">Linear regression model</a>

For more information on linear regression see this
<a href="https://rafalab.github.io/dsbook/linear-models.html#linear-regression-in-the-tidyverse" target="_blank">book</a>
and this
<a href="https://opencasestudies.github.io/ocs-bp-diet/" target="_blank">case study</a>.

avocado fill this out

#### For users

There is a [`Makefile`](Makefile) in this folder that allows you to type
`make` to knit the case study contained in the `index.Rmd` to
`index.html` and it will also knit the [`README.Rmd`](README.Rmd) to a
markdown file (`README.md`).

#### For instructors

avocado fill this out

#### Target audience

For individuals or classes with some familiarity with regression. See
this
<a href="https://opencasestudies.github.io/ocs-bp-diet/" target="_blank">case study</a>
for an introduction to regression.

#### Suggested homework

avocado fill this out
