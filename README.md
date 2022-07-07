
# MVSE

MVSE, Mosquito-borne Viral Suitability Estimator, provides methods for
the estimation of an index of climate-based transmission potential for
mosquito-borne viruses. It can be parametrized for any combination of
host, virus and mosquito-species of interest with local climate data.

## Installation

The MVSE package is currently not hosted on CRAN (Comprehensive R
Archive Network). We thus need to install the package directly from the
GithHub repo where it is hosted.

    #> Installing package into '/private/var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T/RtmpUyvcPp/temp_libpath912f5a637bc4'
    #> (as 'lib' is unspecified)
    #> 
    #> The downloaded binary packages are in
    #>  /var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T//RtmphVjdOW/downloaded_packages
    #> Installing package into '/private/var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T/RtmpUyvcPp/temp_libpath912f5a637bc4'
    #> (as 'lib' is unspecified)
    #> 
    #> The downloaded binary packages are in
    #>  /var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T//RtmphVjdOW/downloaded_packages
    #> Loading required package: tidyverse
    #> ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.1 ──
    #> ✓ ggplot2 3.3.6     ✓ purrr   0.3.4
    #> ✓ tibble  3.1.6     ✓ dplyr   1.0.7
    #> ✓ tidyr   1.1.4     ✓ stringr 1.4.0
    #> ✓ readr   2.1.1     ✓ forcats 0.5.1
    #> ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
    #> x dplyr::filter() masks stats::filter()
    #> x dplyr::lag()    masks stats::lag()
    #> Loading required package: devtools
    #> Loading required package: usethis
    #> Downloading GitHub repo TaishiNakase/MVSE@HEAD
    #> rlang        (0.4.12 -> 1.0.3  ) [CRAN]
    #> magrittr     (2.0.1  -> 2.0.3  ) [CRAN]
    #> vctrs        (0.3.8  -> 0.4.1  ) [CRAN]
    #> glue         (1.6.0  -> 1.6.2  ) [CRAN]
    #> fansi        (1.0.2  -> 1.0.3  ) [CRAN]
    #> crayon       (1.4.2  -> 1.5.1  ) [CRAN]
    #> cli          (3.1.1  -> 3.3.0  ) [CRAN]
    #> Rcpp         (1.0.8  -> 1.0.8.3) [CRAN]
    #> plyr         (1.8.6  -> 1.8.7  ) [CRAN]
    #> colorspace   (2.0-2  -> 2.0-3  ) [CRAN]
    #> RColorBrewer (1.1-2  -> 1.1-3  ) [CRAN]
    #> withr        (2.4.3  -> 2.5.0  ) [CRAN]
    #> farver       (2.1.0  -> 2.1.1  ) [CRAN]
    #> scales       (1.1.1  -> 1.2.0  ) [CRAN]
    #> generics     (0.1.1  -> 0.1.3  ) [CRAN]
    #> matrixStats  (0.61.0 -> 0.62.0 ) [CRAN]
    #> pillar       (1.6.4  -> 1.7.0  ) [CRAN]
    #> tibble       (3.1.6  -> 3.1.7  ) [CRAN]
    #> checkmate    (2.0.0  -> 2.1.0  ) [CRAN]
    #> tidyselect   (1.1.1  -> 1.1.2  ) [CRAN]
    #> dplyr        (1.0.7  -> 1.0.9  ) [CRAN]
    #> tidyr        (1.1.4  -> 1.2.0  ) [CRAN]
    #> bayesplot    (1.8.1  -> 1.9.0  ) [CRAN]
    #> Installing 23 packages: rlang, magrittr, vctrs, glue, fansi, crayon, cli, Rcpp, plyr, colorspace, RColorBrewer, withr, farver, scales, generics, matrixStats, pillar, tibble, checkmate, tidyselect, dplyr, tidyr, bayesplot
    #> Installing packages into '/private/var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T/RtmpUyvcPp/temp_libpath912f5a637bc4'
    #> (as 'lib' is unspecified)
    #> 
    #>   There is a binary version available but the source version is later:
    #>        binary source needs_compilation
    #> farver  2.1.0  2.1.1              TRUE
    #> 
    #> 
    #> The downloaded binary packages are in
    #>  /var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T//RtmphVjdOW/downloaded_packages
    #> installing the source package 'farver'
    #> * checking for file ‘/private/var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T/RtmphVjdOW/remotes939e42b7f57a/TaishiNakase-MVSE-3c23dc7/DESCRIPTION’ ... OK
    #> * preparing ‘MVSE’:
    #> * checking DESCRIPTION meta-information ... OK
    #> * cleaning src
    #> * checking for LF line-endings in source and make files and shell scripts
    #> * checking for empty or unneeded directories
    #> * building ‘MVSE_1.0.tar.gz’
    #> Installing package into '/private/var/folders/j2/b7c7t8j976z3zxy0tgc4b9jw0000gn/T/RtmpUyvcPp/temp_libpath912f5a637bc4'
    #> (as 'lib' is unspecified)

## Example

Let’s go through a short example of how one might use MVSE to estimate
Index P for some mosquito-borne virus.

First, we will install some packages.

    #> 
    #> Attaching package: 'MVSE'
    #> The following object is masked from 'package:tidyr':
    #> 
    #>     extract

We first need to create a `mvse_model` object, which requires time
series data for climatic variables (i.e. temperature, humidity and
rainfall) as well as epi-entomological prior distributions for the
virus/vector/host system of interest.

``` r
# climate data
data("climateFSA")

# user-defined model
priors <- list(mosq_life_exp=list(pars=c(mean=12, sd=2), dist="normal"),
               mosq_inc_per=list(pars=c(mean=7, sd=2), dist="normal"),
               mosq_biting_freq=list(pars=c(mean=0.25, sd=0.01), dist="normal"),
               human_life_exp=list(pars=c(mean=71.1, sd=2), dist="normal"),
               human_inc_per=list(pars=c(mean=5.8, sd=1), dist="normal"),
               human_inf_per=list(pars=c(mean=5.9, sd=1), dist="normal"))
example_mvse_model <- mvse_model(model_name="user_test", climate_data=climateFSA, priors=priors)
```

Let’s take a look at the input data to be used in the sampling
procedure.

``` r
example_mvse_model
#> Class: mvsemodel 
#> Model name: user_test 
#> Model category: user-defined 
#> Climate data (limited to first 10 rows): 
#>          date        T        H            R
#> 1  1981-01-02 25.13554 73.84253 0.0022509235
#> 2  1981-02-02 25.01051 73.56940 0.0017562567
#> 3  1981-03-02 25.44149 76.77259 0.0091257023
#> 4  1981-04-02 23.51202 84.59996 0.0029805890
#> 5  1981-05-02 22.42301 85.48878 0.0020460677
#> 6  1981-06-02 21.85287 85.16210 0.0020688535
#> 7  1981-07-02 20.71406 83.57096 0.0017366349
#> 8  1981-08-02 20.99485 79.70238 0.0012274350
#> 9  1981-09-02 22.46040 70.62206 0.0005982321
#> 10 1981-10-02 25.42501 65.91237 0.0006568354
#> Priors: 
#>   Mosquito life expectancy (days)        : normal(mean=12, sd=2) 
#>   Mosquito incubation period (days)      : normal(mean=7, sd=2) 
#>   Mosquito biting frequency (bites/female/day)   : normal(mean=0.25, sd=0.01) 
#>   Human life expectancy (years)          : normal(mean=71.1, sd=2) 
#>   Human incubation period (days)         : normal(mean=5.8, sd=1) 
#>   Human infectious period (days)         : normal(mean=5.9, sd=1)
```

Next, let’s perform the MCMC (Markov chain Monte Carlo) sampling
procedure to estimate Index P.

``` r
example_mvse_fit <- fitting(example_mvse_model, verbose=FALSE)
```

Finally, let’s take a look at the estimated distribution of the time
series of Index P.

``` r
indexP_plot <- mcmc_index_dist(example_mvse_fit, index="indexP")
```
