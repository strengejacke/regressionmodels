
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
<td style="text-align: left;">Trials (or proportions of <em>counts</em>)</td>
<td style="text-align: left;">20 successes out of 30 trials</td>
<td style="text-align: left;">logistic</td>
<td style="text-align: left;"><code>glm(cbind(successes, failures), family=binomial)</code></td>
<td style="text-align: left;"><a href="http://had.co.nz/notes/modelling/logistic-regression.html">Hadley’s notes</a></td>
<td style="text-align: left;"><code>brm(successes &amp;#124; trials(total), family = binomial())</code></td>
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
<td style="text-align: left;">Count data</td>
<td style="text-align: left;">Number of usage, counts of events</td>
<td style="text-align: left;">Poisson</td>
<td style="text-align: left;"><code>glm(family=poisson)</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/poisson-regression/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = poisson())</code></td>
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
<td style="text-align: left;">Count data, with excess zeros or overdispersion</td>
<td style="text-align: left;">Number of usage, counts of events (with higher variance than mean of response)</td>
<td style="text-align: left;">negative binomial</td>
<td style="text-align: left;">- <code>glm\ - nb()</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/negative-binomial-regression/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = negbinomial())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;">- <code>glmer\ - nb()</code><br />
- <code>glmmTMB(family=nbinom)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Count data with very many zeros (inflation)</td>
<td style="text-align: left;">see count data, but response is modelled as mixture of Bernoulli &amp; Poisson distribution (two sources of zeros)</td>
<td style="text-align: left;">zero-inflated</td>
<td style="text-align: left;"><code>zeroinfl()</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/zip/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = zero_inflated_poisson())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>glmmTMB(ziformula, family=poisson)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Count data, with very many zeros (inflation) and overdispersion</td>
<td style="text-align: left;">Number of usage, counts of events (with higher variance than mean of response)</td>
<td style="text-align: left;">zero-inflated negative binomial</td>
<td style="text-align: left;"><code>zeroinfl(dist="negbin")</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/zinb/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = zero_inflated_negbinomial())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>glmmTMB(ziformula, family=nbinom)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Count data, zero-truncated</td>
<td style="text-align: left;">see count data, but only for positive counts (hurdle component models zero-counts)</td>
<td style="text-align: left;">hurdle (Poisson)</td>
<td style="text-align: left;"><code>hurdle()</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/zero-truncated-poisson/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = hurdle_poisson())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>glmmTMB(family=truncated_poisson)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Count data, zero-truncated and overdispersion</td>
<td style="text-align: left;">see “Count data, zero-truncated”, but with higher variance than mean of response</td>
<td style="text-align: left;">hurdle (neg. binomial)</td>
<td style="text-align: left;"><code>vglm(family=posnegbinomial)</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/zero-truncated-negative-binomial/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = hurdle_negbinomial())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>glmmTMB(family=truncated_nbinom)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Proportion / Ratio (without zero and one)</td>
<td style="text-align: left;">Percentages, proportion of <em>continuous</em> data</td>
<td style="text-align: left;">Beta <em>(see note below)</em></td>
<td style="text-align: left;"><code>betareg()</code></td>
<td style="text-align: left;"><a href="https://www.rdatagen.net/post/binary-beta-beta-binomial/">ouR data generation</a></td>
<td style="text-align: left;"><code>brm(family = Beta())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>glmmTMB(family=beta_family)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Proportion / Ratio (including zero and one)</td>
<td style="text-align: left;">Percentages, proportions of <em>continuous</em> data</td>
<td style="text-align: left;">Beta-Binomial, zero-inflated Beta, ordered Beta <em>(see note below)</em></td>
<td style="text-align: left;">- <code>BBreg()</code><br />
- <code>betabin()</code><br />
- <code>vglm(family=betabinomial)</code><br />
- <code>ordbetareg()</code></td>
<td style="text-align: left;"><a href="https://www.rdatagen.net/post/binary-beta-beta-binomial/">ouR data generation</a></td>
<td style="text-align: left;"><code>brm(family = zero_one_inflated_beta())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;">- <code>glmmTMB(ziformula, family=beta_family)</code><br />
- <code>glmmTMB(ziformula, family= betabinomial)</code><br />
- <code>glmmTMB(ziformula, family= ordbeta)</code><br />
- <code>ordbetareg()</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Ordinal</td>
<td style="text-align: left;">Likert scale, worse/ok/better</td>
<td style="text-align: left;">ordinal, proportional odds, cumulative</td>
<td style="text-align: left;">- <code>polr()</code><br />
- <code>clm()</code><br />
- <code>bracl()</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/ordinal-logistic-regression/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = cumulative())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;">- <code>clmm()</code><br />
- <code>mixor()</code><br />
- <code>MCMCglmm(family = "ordinal")</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Multinomial</td>
<td style="text-align: left;">No natural order of categories, like red/green/blue</td>
<td style="text-align: left;">multinomial</td>
<td style="text-align: left;">- <code>multinom()</code><br />
- <code>brmultinom()</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/multinomial-logistic-regression/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = multinomial())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>MCMCglmm(family = "multinomial")</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Continuous, right-skewed</td>
<td style="text-align: left;">Financial data, reaction times</td>
<td style="text-align: left;">Gamma</td>
<td style="text-align: left;"><code>glm(family=Gamma)</code></td>
<td style="text-align: left;"><a href="https://seananderson.ca/2014/04/08/gamma-glms/">Sean Anderson</a></td>
<td style="text-align: left;"><code>brm(family = Gamma())</code>, but see also <a href="https://lindeloev.github.io/shiny-rt/">Reaction time distributions in <code>brms</code></a></td>
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
<td style="text-align: left;">(Semi-)Continuous, (right) skewed, probably with spike at zero (zero-inlfated)</td>
<td style="text-align: left;">Financial data, probably exponential dispersion of variance</td>
<td style="text-align: left;">Tweedie</td>
<td style="text-align: left;">- <code>glm(family=tweedie)</code><br />
- <code>cpglm()</code></td>
<td style="text-align: left;"><a href="https://blog.revolutionanalytics.com/2014/10/a-note-on-tweedie.html">Revolutions</a></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;">- <code>cpglmm()</code><br />
- <code>glmmTMB(*)</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">(Semi-)Continuous, (right) skewed, probably with spike at zero (zero-inlfated)</td>
<td style="text-align: left;">Normal distribution, but negative values are censored and stacked on zero</td>
<td style="text-align: left;">Tobit</td>
<td style="text-align: left;">- <code>tobit()</code><br />
- <code>censReg()</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>brm(y &amp;#124; cens(), family = gaussian())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>semLme()</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Continuous, but truncated or outliers</td>
<td style="text-align: left;"></td>
<td style="text-align: left;">truncated</td>
<td style="text-align: left;">- <code>censReg()</code><br />
- <code>tobit()</code><br />
- <code>vglm(family=tobit)</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/tobit-models/">UCLA-1</a>, <a href="https://stats.idre.ucla.edu/r/dae/truncated-regression/">UCLA-2</a></td>
<td style="text-align: left;"><code>brm(y &amp;#124; trunc(), family = gaussian())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;">Continuous, but exponential growth</td>
<td style="text-align: left;"></td>
<td style="text-align: left;">log-transformed, non-linear</td>
<td style="text-align: left;">- <code>glm(family=Gaussian("log")</code><br />
- <code>nls()</code></td>
<td style="text-align: left;"><a href="https://www.statforbiology.com/nonlinearregression/usefulequations">Some useful equations</a>, <a href="https://stats.stackexchange.com/a/61806/54740">linear vs. non-linear regression</a></td>
<td style="text-align: left;"></td>
</tr>
<tr class="odd">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;">- <code>glmmTMB(*)</code><br />
- <code>nlmer()</code><br />
- <code>nlme()</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
</tr>
<tr class="even">
<td style="text-align: left;">Proportion / Ratio with more than 2 categories</td>
<td style="text-align: left;">Biomass partitioning in plants (ratio of leaf, stem and root mass)</td>
<td style="text-align: left;">Dirichlet</td>
<td style="text-align: left;"><code>DirichReg()</code></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>brm(family = dirichlet())</code></td>
</tr>
<tr class="odd">
<td style="text-align: left;">Time-to-Event</td>
<td style="text-align: left;">Survival-analysis, time until event/death occurs</td>
<td style="text-align: left;">Cox (proportional hazards)</td>
<td style="text-align: left;"><code>coxph</code></td>
<td style="text-align: left;"><a href="https://stats.idre.ucla.edu/r/dae/mixed-effects-cox-regression/">UCLA</a></td>
<td style="text-align: left;"><code>brm(family = cox())</code></td>
</tr>
<tr class="even">
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"></td>
<td style="text-align: left;"><code>coxme()</code></td>
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
