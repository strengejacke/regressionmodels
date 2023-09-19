
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

<table>
<colgroup>
<col style="width: 14%" />
<col style="width: 20%" />
<col style="width: 12%" />
<col style="width: 27%" />
<col style="width: 10%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th style="text-align: left;">Nature of Response</th>
<th style="text-align: left;">Example</th>
<th style="text-align: left;">Type of Regression</th>
<th style="text-align: left;">R package or function</th>
<th style="text-align: left;">Example Webpage</th>
<th style="text-align: left;">Bayesian with <a href="https://paul-buerkner.github.io/brms/reference/brmsfamily.html"><code>brms</code></a></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td style="text-align: left;">Continuous</td>
<td style="text-align: left;">Quality of Life, linear scales</td>
<td style="text-align: left;">linear</td>
<td style="text-align: left;"><code>lm()</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>brm(family = gaussian())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;">- <code>lmer()</code><br />
- <code>glmmTMB()</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Binary</td>
<td style="text-align: left;">Success yes/no</td>
<td style="text-align: left;">binary logistic</td>
<td style="text-align: left;"><code>glm(family=binomial)</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/logit-regression/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = binomial())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;">- <code>glmer(*)</code><br />
- <code>glmmTMB(*)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Binary, weighted</td>
<td style="text-align: left;">Success yes/no, with weights</td>
<td style="text-align: left;">quasi-binary logistic</td>
<td style="text-align: left;"><code>glm(family=quasibinomial)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>glmmPQL(family="quasibinomial")                                                                                                                    |                                                        |                                                                            | |Trials (or proportions of _counts_)                                            |20 successes out of 30 trials                                                                                  |logistic                                                           |</code>glm(cbind(successes, failures), family=binomial)<code>|[Hadley’s notes](http://had.co.nz/notes/modelling/logistic-regression.html)|</code>brm(successes | trials(total), family = binomial())<code>| |                                                                               |                                                                                                               |                                                                   |-</code>glmer(<em>)<code>\ -</code>glmmTMB(</em>)<code>|                                                        |                                                                            | |Count data                                                                     |Number of usage, counts of events                                                                              |Poisson                                                            |</code>glm(family=poisson)<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/poisson-regression/)|</code>brm(family = poisson())<code>| |                                                                               |                                                                                                               |                                                                   |-</code>glmer(<em>)<code>\ -</code>glmmTMB(</em>)<code>|                                                        |                                                                            | |Count data, with excess zeros or overdispersion                                |Number of usage, counts of events (with higher variance than mean of response)                                 |negative binomial                                                  |-</code>glm<br />
- nb()<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/negative-binomial-regression/)|</code>brm(family = negbinomial())<code>| |                                                                               |                                                                                                               |                                                                   |-</code>glmer<br />
- nb()<code>\ -</code>glmmTMB(family=nbinom)<code>|                                                        |                                                                            | |Count data with very many zeros (inflation)                                    |see count data, but response is modelled as mixture of Bernoulli &amp; Poisson distribution (two sources of zeros) |zero-inflated                                                      |</code>zeroinfl()<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/zip/)          |</code>brm(family = zero_inflated_poisson())<code>| |                                                                               |                                                                                                               |                                                                   |</code>glmmTMB(ziformula, family=poisson)<code>|                                                        |                                                                            | |Count data, with very many zeros (inflation) and overdispersion                |Number of usage, counts of events (with higher variance than mean of response)                                 |zero-inflated negative binomial                                    |</code>zeroinfl(dist=“negbin”)<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/zinb/)         |</code>brm(family = zero_inflated_negbinomial())<code>| |                                                                               |                                                                                                               |                                                                   |</code>glmmTMB(ziformula, family=nbinom)<code>|                                                        |                                                                            | |Count data, zero-truncated                                                     |see count data, but only for positive counts (hurdle component models zero-counts)                             |hurdle (Poisson)                                                   |</code>hurdle()<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/zero-truncated-poisson/)|</code>brm(family = hurdle_poisson())<code>| |                                                                               |                                                                                                               |                                                                   |</code>glmmTMB(family=truncated_poisson)<code>|                                                        |                                                                            | |Count data, zero-truncated and overdispersion                                  |see “Count data, zero-truncated”, but with higher variance than mean of response                               |hurdle (neg. binomial)                                             |</code>vglm(family=posnegbinomial)<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/zero-truncated-negative-binomial/)|</code>brm(family = hurdle_negbinomial())<code>| |                                                                               |                                                                                                               |                                                                   |</code>glmmTMB(family=truncated_nbinom)<code>|                                                        |                                                                            | |Proportion / Ratio (without zero and one)                                      |Percentages, proportion of _continuous_ data                                                                   |Beta _(see note below)_                                            |</code>betareg()<code>|[ouR data generation]( https://www.rdatagen.net/post/binary-beta-beta-binomial/)|</code>brm(family = Beta())<code>| |                                                                               |                                                                                                               |                                                                   |</code>glmmTMB(family=beta_family)<code>|                                                        |                                                                            | |Proportion / Ratio (including zero and one)                                    |Percentages, proportions of _continuous_ data                                                                  |Beta-Binomial, zero-inflated Beta, ordered Beta _(see note below)_ |-</code>BBreg()<code>\ -</code>betabin()<code>\ -</code>vglm(family=betabinomial)<code>\ -</code>ordbetareg()<code>|[ouR data generation]( https://www.rdatagen.net/post/binary-beta-beta-binomial/)|</code>brm(family = zero_one_inflated_beta())<code>| |                                                                               |                                                                                                               |                                                                   |-</code>glmmTMB(ziformula, family=beta_family)<code>\ -</code>glmmTMB(ziformula, family= betabinomial)<code>\ -</code>glmmTMB(ziformula, family= ordbeta)<code>\ -</code>ordbetareg()<code>|                                                        |                                                                            | |Ordinal                                                                        |Likert scale, worse/ok/better                                                                                  |ordinal, proportional odds, cumulative                             |-</code>polr()<code>\ -</code>clm()<code>\ -</code>bracl()<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/ordinal-logistic-regression/)|</code>brm(family = cumulative())<code>| |                                                                               |                                                                                                               |                                                                   |-</code>clmm()<code>\ -</code>mixor()<code>\ -</code>MCMCglmm(family = “ordinal”)<code>|                                                        |                                                                            | |Multinomial                                                                    |No natural order of categories, like red/green/blue                                                            |multinomial                                                        |-</code>multinom()<code>\ -</code>brmultinom()<code>|[UCLA](https://stats.idre.ucla.edu/r/dae/multinomial-logistic-regression/)|</code>brm(family = multinomial())<code>| |                                                                               |                                                                                                               |                                                                   |</code>MCMCglmm(family = “multinomial”)<code>|                                                        |                                                                            | |Continuous, right-skewed                                                       |Financial data, reaction times                                                                                 |Gamma                                                              |</code>glm(family=Gamma)<code>|[Sean Anderson]( https://seananderson.ca/2014/04/08/gamma-glms/)|</code>brm(family = Gamma())<code>, but see also [Reaction time distributions in</code>brms<code>](https://lindeloev.github.io/shiny-rt/)| |                                                                               |                                                                                                               |                                                                   |-</code>glmer(<em>)<code>\ -</code>glmmTMB(</em>)<code>|                                                        |                                                                            | |(Semi-)Continuous, (right) skewed, probably with spike at zero (zero-inlfated) |Financial data, probably exponential dispersion of variance                                                    |Tweedie                                                            |-</code>glm(family=tweedie)<code>\ -</code>cpglm()<code>|[Revolutions](https://blog.revolutionanalytics.com/2014/10/a-note-on-tweedie.html)|                                                                            | |                                                                               |                                                                                                               |                                                                   |-</code>cpglmm()<code>\ -</code>glmmTMB(<em>)<code>|                                                        |                                                                            | |(Semi-)Continuous, (right) skewed, probably with spike at zero (zero-inlfated) |Normal distribution, but negative values are censored and stacked on zero                                      |Tobit                                                              |-</code>tobit()<code>\ -</code>censReg()<code>|                                                        |</code>brm(y | cens(), family = gaussian())<code>| |                                                                               |                                                                                                               |                                                                   |</code>semLme()<code>|                                                        |                                                                            | |Continuous, but truncated or outliers                                          |                                                                                                               |truncated                                                          |-</code>censReg()<code>\ -</code>tobit()<code>\ -</code>vglm(family=tobit)<code>|[UCLA-1](https://stats.idre.ucla.edu/r/dae/tobit-models/), [UCLA-2](https://stats.idre.ucla.edu/r/dae/truncated-regression/)|</code>brm(y | trunc(), family = gaussian())<code>| |Continuous, but exponential growth                                             |                                                                                                               |log-transformed, non-linear                                        |-</code>glm(family=Gaussian(“log”)<code>\ -</code>nls()<code>|[Some useful equations](https://www.statforbiology.com/nonlinearregression/usefulequations), [linear vs. non-linear regression](https://stats.stackexchange.com/a/61806/54740)|                                                                            | |                                                                               |                                                                                                               |                                                                   |-</code>glmmTMB(</em>)<code>\ -</code>nlmer()<code>\ -</code>nlme()<code>|                                                        |                                                                            | |Proportion / Ratio with more than 2 categories                                 |Biomass partitioning in plants (ratio of leaf, stem and root mass)                                             |Dirichlet                                                          |</code>DirichReg()<code>|                                                        |</code>brm(family = dirichlet())<code>| |Time-to-Event                                                                  |Survival-analysis, time until event/death occurs                                                               |Cox (proportional hazards)                                         |</code>coxph<code>|[UCLA]( https://stats.idre.ucla.edu/r/dae/mixed-effects-cox-regression/)|</code>brm(family = cox())<code>| |                                                                               |                                                                                                               |                                                                   |</code>coxme()`</td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
</tbody>
</table>

  - `*` indicates that for the mixed models functions the same
    response-type and family should be used as for their `glm`
    counterpart.

  - *Note that ratios or proportions from **count data**, like
    `cbind(successes, failures)`, are modelled as logistic regression
    with `glm(cbind(successes, failures), family=binomial())`, while
    ratios from **continuous data** (where the response ranges from 0 to
    1) are modelled using beta-regression.*

  - *Usually, zero-inflated models are used when 0 or 1 come from a
    separate process or category. However, when the 0/1 values are most
    consistent with censoring rather than with a separate
    category/process, the ordered beta regression is probably a better
    choice (i.e., 0 mean “below detection”, not “something qualitatively
    different happened”) (Source:
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
  - [MASS](https://CRAN.R-project.org/package=MASS): `glmmPQL()`
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
