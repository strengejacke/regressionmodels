
# Overview of R Modelling Packages

This is an overview of R packages and functions for fitting different
types of regression models. For each row, the upper cells in the last
column (*packages and functions*) refer to “simple” models, while the
lower cells refer to their mixed models counterpart (if available and
known).

This overview raises no claims towards completeness of available
modelling packages. Rather, it shows commonly or more often used
packages, but there a plenty of other packages as well (that might even
perform better in doing those mentioned tasks - if you’re aware of such
packages or think that an important package or function is missing,
please [file an
issue](https://github.com/strengejacke/regressionmodels/issues)).

## Modelling Packages

| Nature of Response                                                             | Example                                                                                                        | Type of Regression                                                 | R package or function                                                                                                                       | Example Webpage                                                                                                                                                                | Bayesian with [`brms`](https://paul-buerkner.github.io/brms/reference/brmsfamily.html)                               |
| :----------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------- | :----------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------------ | :----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------------------------------------------------------------------------------- |
| Continuous                                                                     | Quality of Life, linear scales                                                                                 | linear                                                             | `lm()`                                                                                                                                      |                                                                                                                                                                                | `brm(family = gaussian())`                                                                                           |
|                                                                                |                                                                                                                |                                                                    | \* `lmer()`\* `glmmTMB()`                                                                                                                   |                                                                                                                                                                                |                                                                                                                      |
| Binary                                                                         | Success yes/no                                                                                                 | binary logistic                                                    | `glm(family=binomial)`                                                                                                                      | [UCLA](https://stats.idre.ucla.edu/r/dae/logit-regression/)                                                                                                                    | `brm(family = binomial())`                                                                                           |
|                                                                                |                                                                                                                |                                                                    | \- `glmer(family=binomial)`- `glmmTMB(family=binomial)`                                                                                     |                                                                                                                                                                                |                                                                                                                      |
| Trials (or proportions of *counts*)                                            | 20 successes out of 30 trials                                                                                  | logistic                                                           | `glm(cbind(successes, failures), family=binomial)`                                                                                          | [Hadley’s notes](http://had.co.nz/notes/modelling/logistic-regression.html)                                                                                                    | `brm(successes &#124; trials(total), family = binomial())`                                                           |
|                                                                                |                                                                                                                |                                                                    | \- `glmer(cbind(successes, failures), family=binomial)`- `glmmTMB(cbind(successes, failures), family=binomial)`                             |                                                                                                                                                                                |                                                                                                                      |
| Count data                                                                     | Number of usage, counts of events                                                                              | Poisson                                                            | `glm(family=poisson)`                                                                                                                       | [UCLA](https://stats.idre.ucla.edu/r/dae/poisson-regression/)                                                                                                                  | `brm(family = poisson())`                                                                                            |
|                                                                                |                                                                                                                |                                                                    | \- `glmer(family=poisson)`- `glmmTMB(family=poisson)`                                                                                       |                                                                                                                                                                                |                                                                                                                      |
| Count data, with excess zeros or overdispersion                                | Number of usage, counts of events (with higher variance than mean of response)                                 | negative binomial                                                  | `glm.nb()`                                                                                                                                  | [UCLA](https://stats.idre.ucla.edu/r/dae/negative-binomial-regression/)                                                                                                        | `brm(family = negbinomial())`                                                                                        |
|                                                                                |                                                                                                                |                                                                    | \- `glmer.nb()`- `glmmTMB(family=nbinom)`                                                                                                   |                                                                                                                                                                                |                                                                                                                      |
| Count data with very many zeros (inflation)                                    | see count data, but response is modelled as mixture of Bernoulli & Poisson distribution (two sources of zeros) | zero-inflated                                                      | `zeroinfl()`                                                                                                                                | [UCLA](https://stats.idre.ucla.edu/r/dae/zip/)                                                                                                                                 | `brm(family = zero_inflated_poisson())`                                                                              |
|                                                                                |                                                                                                                |                                                                    | `glmmTMB(ziformula, family=poisson)`                                                                                                        |                                                                                                                                                                                |                                                                                                                      |
| Count data, with very many zeros (inflation) and overdispersion                | Number of usage, counts of events (with higher variance than mean of response)                                 | zero-inflated negative binomial                                    | `zeroinfl(dist="negbin")`                                                                                                                   | [UCLA](https://stats.idre.ucla.edu/r/dae/zinb/)                                                                                                                                | `brm(family = zero_inflated_negbinomial())`                                                                          |
|                                                                                |                                                                                                                |                                                                    | `glmmTMB(ziformula, family=nbinom)`                                                                                                         |                                                                                                                                                                                |                                                                                                                      |
| Count data, zero-truncated                                                     | see count data, but only for positive counts (hurdle component models zero-counts)                             | hurdle (Poisson)                                                   | `hurdle()`                                                                                                                                  | [UCLA](https://stats.idre.ucla.edu/r/dae/zero-truncated-poisson/)                                                                                                              | `brm(family = hurdle_poisson())`                                                                                     |
|                                                                                |                                                                                                                |                                                                    | `glmmTMB(family=truncated_poisson)`                                                                                                         |                                                                                                                                                                                |                                                                                                                      |
| Count data, zero-truncated and overdispersion                                  | see “Count data, zero-truncated”, but with higher variance than mean of response                               | hurdle (neg. binomial)                                             | `vglm(family=posnegbinomial)`                                                                                                               | [UCLA](https://stats.idre.ucla.edu/r/dae/zero-truncated-negative-binomial/)                                                                                                    | `brm(family = hurdle_negbinomial())`                                                                                 |
|                                                                                |                                                                                                                |                                                                    | `glmmTMB(family=truncated_nbinom)`                                                                                                          |                                                                                                                                                                                |                                                                                                                      |
| Proportion / Ratio (without zero and one)                                      | Percentages, proportion of *continuous* data                                                                   | Beta *(see note below)*                                            | `betareg()`                                                                                                                                 | [ouR data generation](https://www.rdatagen.net/post/binary-beta-beta-binomial/)                                                                                                | `brm(family = Beta())`                                                                                               |
|                                                                                |                                                                                                                |                                                                    | `glmmTMB(family=beta_family)`                                                                                                               |                                                                                                                                                                                |                                                                                                                      |
| Proportion / Ratio (including zero and one)                                    | Percentages, proportions of *continuous* data                                                                  | Beta-Binomial, zero-inflated Beta, ordered Beta *(see note below)* | `BBreg()`, `betabin()`, `vglm(family=betabinomial)`, `ordbetareg()`                                                                         | [ouR data generation](https://www.rdatagen.net/post/binary-beta-beta-binomial/)                                                                                                | `brm(family = zero_one_inflated_beta())`                                                                             |
|                                                                                |                                                                                                                |                                                                    | `glmmTMB(ziformula, family=beta_family)`, `glmmTMB(ziformula, family= betabinomial)`, `glmmTMB(ziformula, family= ordbeta)`, `ordbetareg()` |                                                                                                                                                                                |                                                                                                                      |
| Ordinal                                                                        | Likert scale, worse/ok/better                                                                                  | ordinal, proportional odds, cumulative                             | `polr()`, `clm()`, `bracl()`                                                                                                                | [UCLA](https://stats.idre.ucla.edu/r/dae/ordinal-logistic-regression/)                                                                                                         | `brm(family = cumulative())`                                                                                         |
|                                                                                |                                                                                                                |                                                                    | `clmm()`, `mixor()`, `MCMCglmm(family = "ordinal")`                                                                                         |                                                                                                                                                                                |                                                                                                                      |
| Multinomial                                                                    | No natural order of categories, like red/green/blue                                                            | multinomial                                                        | `multinom()`, `brmultinom()`                                                                                                                | [UCLA](https://stats.idre.ucla.edu/r/dae/multinomial-logistic-regression/)                                                                                                     | `brm(family = multinomial())`                                                                                        |
|                                                                                |                                                                                                                |                                                                    | `MCMCglmm(family = "multinomial")`                                                                                                          |                                                                                                                                                                                |                                                                                                                      |
| Continuous, right-skewed                                                       | Financial data, reaction times                                                                                 | Gamma                                                              | `glm(family=Gamma)`                                                                                                                         | [Sean Anderson](https://seananderson.ca/2014/04/08/gamma-glms/)                                                                                                                | `brm(family = Gamma())`, but see also [Reaction time distributions in `brms`](https://lindeloev.github.io/shiny-rt/) |
|                                                                                |                                                                                                                |                                                                    | `glmer()`, `glmmTMB()`                                                                                                                      |                                                                                                                                                                                |                                                                                                                      |
| (Semi-)Continuous, (right) skewed, probably with spike at zero (zero-inlfated) | Financial data, probably exponential dispersion of variance                                                    | Tweedie                                                            | `glm(family=tweedie)`, `cpglm()`                                                                                                            | [Revolutions](https://blog.revolutionanalytics.com/2014/10/a-note-on-tweedie.html)                                                                                             |                                                                                                                      |
|                                                                                |                                                                                                                |                                                                    | `cpglmm()`, `glmmTMB(family=tweedie)`                                                                                                       |                                                                                                                                                                                |                                                                                                                      |
| (Semi-)Continuous, (right) skewed, probably with spike at zero (zero-inlfated) | Normal distribution, but negative values are censored and stacked on zero                                      | Tobit                                                              | `tobit()`, `censReg()`                                                                                                                      |                                                                                                                                                                                | `brm(y &#124; cens(), family = gaussian())`                                                                          |
|                                                                                |                                                                                                                |                                                                    | `semLme()`                                                                                                                                  |                                                                                                                                                                                |                                                                                                                      |
| Continuous, but truncated or outliers                                          |                                                                                                                | truncated                                                          | `censReg()`, `tobit()`, `vglm(family=tobit)`                                                                                                | [UCLA-1](https://stats.idre.ucla.edu/r/dae/tobit-models/), [UCLA-2](https://stats.idre.ucla.edu/r/dae/truncated-regression/)                                                   | `brm(y &#124; trunc(), family = gaussian())`                                                                         |
| Continuous, but exponential growth                                             |                                                                                                                | log-transformed, non-linear                                        | `glm(family=Gaussian("log")`, `nls()`                                                                                                       | [Some useful equations](https://www.statforbiology.com/nonlinearregression/usefulequations), [linear vs. non-linear regression](https://stats.stackexchange.com/a/61806/54740) |                                                                                                                      |
|                                                                                |                                                                                                                |                                                                    | `glmmTMB(family=Gaussian("log"))`, `nlmer()`, `nlme()`                                                                                      |                                                                                                                                                                                |                                                                                                                      |
| Proportion / Ratio with more than 2 categories                                 | Biomass partitioning in plants (ratio of leaf, stem and root mass)                                             | Dirichlet                                                          | `DirichReg()`                                                                                                                               |                                                                                                                                                                                | `brm(family = dirichlet())`                                                                                          |
| Time-to-Event                                                                  | Survival-analysis, time until event/death occurs                                                               | Cox (proportional hazards)                                         | `coxph`                                                                                                                                     | [UCLA](https://stats.idre.ucla.edu/r/dae/mixed-effects-cox-regression/)                                                                                                        | `brm(family = cox())`                                                                                                |
|                                                                                |                                                                                                                |                                                                    | `coxme()`                                                                                                                                   |                                                                                                                                                                                |                                                                                                                      |

*Note that ratios or proportions from **count data**, like
`cbind(successes, failures)`, are modelled as logistic regression with
`glm(cbind(successes, failures), family=binomial())`, while ratios from
**continuous data** (where the response ranges from 0 to 1) are modelled
using beta-regression.*

*Usually, zero-inflated models are used when 0 or 1 come from a separate
process or category. However, when the 0/1 values are most consistent
with censoring rather than with a separate category/process, the ordered
beta regression is probably a better choice (i.e., 0 mean “below
detection”, not “something qualitatively different happened”) (Source:
<https://twitter.com/bolkerb/status/1577755600808775680>)*

## Included packages for non-mixed models:

  - Base R: `lm()`, `glm()`
  - [AER](https://CRAN.R-project.org/package=AER): `tobit()`
  - [aod](https://CRAN.R-project.org/package=aod): `betabin()`
  - [betareg](https://CRAN.R-project.org/package=betareg): `betareg()`
  - [brglm2](https://CRAN.R-project.org/package=brglm2): `bracl()`,
    `brmultinom()`
  - [censReg](https://CRAN.R-project.org/package=censReg): `censReg()`
  - [cplm](https://CRAN.R-project.org/package=cplm): `cpglm()`
  - [coxph](https://CRAN.R-project.org/package=survival): `coxph()`
  - [DirichletReg](https://CRAN.R-project.org/package=DirichletReg):
    `DirichReg()`
  - [HRQoL](https://CRAN.R-project.org/package=HRQoL): `BBreg()`
  - [MASS](https://CRAN.R-project.org/package=MASS): `glm.nb()`,
    `polr()`
  - [nnet](https://CRAN.R-project.org/package=nnet): `multinom()`
  - [ordbetareg](https://cran.r-project.org/package=ordbetareg):
    `ordbetareg()`
  - [ordinal](https://CRAN.R-project.org/package=ordinal): `clm()`,
    `clm2()`
  - [pscl](https://CRAN.R-project.org/package=pscl): `zeroinfl()`,
    `hurdle()`
  - [statmod](https://CRAN.R-project.org/package=statmod): `tweedie()`
  - [VGAM](https://CRAN.R-project.org/package=VGAM): `vglm()`

## Included packages for mixed models:

  - [cplm](https://CRAN.R-project.org/package=cplm): `cpglmm()`
  - [coxme](https://CRAN.R-project.org/package=coxme): `coxme()`
  - [glmmTMB](https://CRAN.R-project.org/package=glmmTMB): `glmmTMB()`
  - [lme4](https://CRAN.R-project.org/package=lme4): `lmer()`,
    `glmer()`, `glmer.nb()`
  - [MCMCglmm](https://CRAN.R-project.org/package=MCMCglmm):
    `MCMCglmm()`
  - [mixor](https://CRAN.R-project.org/package=mixor): `mixor()`
  - [ordbetareg](https://cran.r-project.org/package=ordbetareg):
    `ordbetareg()`
  - [ordinal](https://CRAN.R-project.org/package=ordinal): `clmm()`,
    `clmm2()`
  - [smicd](https://cran.r-project.org/package=smicd): `semLme()`

## Included packages for Bayesian models (mixed an non-mixed):

  - [brms](https://cran.r-project.org/package=brms): `brm()`

## Handout

There is a [handout](pdf/regression_pkgs_handout.pdf) in PDF-format.
