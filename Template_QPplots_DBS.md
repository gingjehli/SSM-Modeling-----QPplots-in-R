Template_QP-plots_DBS_Rmarkdown_github
================

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

    ## 
    ## Attaching package: 'gridExtra'

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     combine

    ## -- Attaching packages --------------------------------------- tidyverse 1.3.1 --

    ## v tibble  3.1.6     v purrr   0.3.4
    ## v tidyr   1.1.4     v stringr 1.4.0
    ## v readr   2.1.0     v forcats 0.5.1

    ## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
    ## x gridExtra::combine() masks dplyr::combine()
    ## x dplyr::filter()      masks stats::filter()
    ## x dplyr::lag()         masks stats::lag()

    ## 
    ## Attaching package: 'rstatix'

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## 
    ## Attaching package: 'ggpubr'

    ## The following object is masked from 'package:cowplot':
    ## 
    ##     get_legend

    ## 
    ## Attaching package: 'dbplyr'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     ident, sql

    ## NOTE: Either Arial Narrow or Roboto Condensed fonts are required to use these themes.

    ##       Please use hrbrthemes::import_roboto_condensed() to install Roboto Condensed and

    ##       if Arial Narrow is not on your system, please see https://bit.ly/arialnarrow

    ## 
    ## Attaching package: 'MASS'

    ## The following object is masked from 'package:rstatix':
    ## 
    ##     select

    ## The following object is masked from 'package:dplyr':
    ## 
    ##     select

    ## Loading required package: mice

    ## 
    ## Attaching package: 'mice'

    ## The following object is masked from 'package:stats':
    ## 
    ##     filter

    ## The following objects are masked from 'package:base':
    ## 
    ##     cbind, rbind

    ## * miceadds 3.11-6 (2021-01-21 11:48:47)

    ## Loading required package: coda

    ## Loading required package: Matrix

    ## 
    ## Attaching package: 'Matrix'

    ## The following objects are masked from 'package:tidyr':
    ## 
    ##     expand, pack, unpack

    ## ************
    ## Welcome to BayesFactor 0.9.12-4.2. If you have questions, please contact Richard Morey (richarddmorey@gmail.com).
    ## 
    ## Type BFManual() to open the manual.
    ## ************

    ## Loading required package: StanHeaders

    ## rstan (Version 2.21.2, GitRev: 2e1f913d3ca3)

    ## For execution on a local, multicore CPU with excess RAM we recommend calling
    ## options(mc.cores = parallel::detectCores()).
    ## To avoid recompilation of unchanged Stan programs, we recommend calling
    ## rstan_options(auto_write = TRUE)

    ## Do not specify '-march=native' in 'LOCAL_CPPFLAGS' or a Makevars file

    ## 
    ## Attaching package: 'rstan'

    ## The following object is masked from 'package:coda':
    ## 
    ##     traceplot

    ## The following object is masked from 'package:tidyr':
    ## 
    ##     extract

    ## Loading required package: Rcpp

    ## Loading 'brms' package (version 2.16.3). Useful instructions
    ## can be found by typing help('brms'). A more detailed introduction
    ## to the package is available through vignette('brms_overview').

    ## 
    ## Attaching package: 'brms'

    ## The following object is masked from 'package:rstan':
    ## 
    ##     loo

    ## The following object is masked from 'package:stats':
    ## 
    ##     ar

    ## Warning: package 'ggthemes' was built under R version 4.1.3

    ## 
    ## Attaching package: 'ggthemes'

    ## The following object is masked from 'package:cowplot':
    ## 
    ##     theme_map

    ## Warning: package 'ggridges' was built under R version 4.1.3

    ## Warning: package 'gmodels' was built under R version 4.1.3

    ## 
    ## Attaching package: 'gmodels'

    ## The following object is masked from 'package:bayestestR':
    ## 
    ##     ci

``` r
dat = read.table( file = 'C:/Users/nadja/OneDrive - Ging-Jehli/Dokumente Nadja/00.Research/McLean/EMU/data/EMU_data_cleaned_091522.txt', 
                                        header = T,
                                        sep = "") 
```

``` r
#out.width="70%"

### Variable: "Conflict2"
dat$conflict2 = dat$sub_reward - dat$sub_averse

#### Forming 4 conflict categories (higher number ==> higher conflict):
   quantsConflict = quantile(dat$conflict2, probs=seq(0,1,0.25))

   dat$catConfl2 = ifelse(dat$conflict2<=quantsConflict[2],1,
                             ifelse(dat$conflict2>quantsConflict[2] & dat$conflict2<=quantsConflict[3],2,
                                    ifelse(dat$conflict2>quantsConflict[3] & dat$conflict2<=quantsConflict[4],3,4)))
```

## Quantile-Probability plots

``` r
datBySBJByConf2byQuant <- dat %>%
  group_by(subj_idx,catConfl2) %>%
  summarise(
    chAp = sum(response,na.rm=T)/n(),
    # RT-Quantiles in terms of 40pixels
    RTQ1_Ap_PT40 = quantile(DT40pix[Choice=="approach"],probs=c(0.1)),
    RTQ3_Ap_PT40 = quantile(DT40pix[Choice=="approach"],probs=c(0.3)),
    RTQ5_Ap_PT40 = quantile(DT40pix[Choice=="approach"],probs=c(0.5)),
    RTQ7_Ap_PT40 = quantile(DT40pix[Choice=="approach"],probs=c(0.7)),
    RTQ9_Ap_PT40 = quantile(DT40pix[Choice=="approach"],probs=c(0.9)),
    RTQ1_Av_PT40 = quantile(DT40pix[Choice=="avoid"],probs=c(0.1)),
    RTQ3_Av_PT40 = quantile(DT40pix[Choice=="avoid"],probs=c(0.3)),
    RTQ5_Av_PT40 = quantile(DT40pix[Choice=="avoid"],probs=c(0.5)),
    RTQ7_Av_PT40 = quantile(DT40pix[Choice=="avoid"],probs=c(0.7)),
    RTQ9_Av_PT40 = quantile(DT40pix[Choice=="avoid"],probs=c(0.9))
  )
```

    ## `summarise()` has grouped output by 'subj_idx'. You can override using the `.groups` argument.

``` r
datByConf2byQuant <- datBySBJByConf2byQuant %>%
  group_by(catConfl2) %>%
  summarise(
    CHAp = mean(chAp,na.rm=T),
    
    # RT-Quantiles in terms of 40pixels
    mRTQ1_Ap_PT40 = mean(RTQ1_Ap_PT40,na.rm=T)*1000,
    mRTQ3_Ap_PT40 = mean(RTQ3_Ap_PT40,na.rm=T)*1000,
    mRTQ5_Ap_PT40 = mean(RTQ5_Ap_PT40,na.rm=T)*1000,
    mRTQ7_Ap_PT40 = mean(RTQ7_Ap_PT40,na.rm=T)*1000,
    mRTQ9_Ap_PT40 = mean(RTQ9_Ap_PT40,na.rm=T)*1000,
    mRTQ1_Av_PT40 = mean(RTQ1_Av_PT40,na.rm=T)*1000,
    mRTQ3_Av_PT40 = mean(RTQ3_Av_PT40,na.rm=T)*1000,
    mRTQ5_Av_PT40 = mean(RTQ5_Av_PT40,na.rm=T)*1000,
    mRTQ7_Av_PT40 = mean(RTQ7_Av_PT40,na.rm=T)*1000,
    mRTQ9_Av_PT40 = mean(RTQ9_Av_PT40,na.rm=T)*1000
    
  )

 datByConf2byQuant$catConfl_Labels = ifelse(datByConf2byQuant$catConfl2==1,'4_reward_Mlower',
                             ifelse(datByConf2byQuant$catConfl2==2,'3_reward_Llower',
                                    ifelse(datByConf2byQuant$catConfl2==3,'2_reward_Lhigher','1_reward_Mhigher')))



###### Quantile-Probability Plot ###############


accspread=0.05
matplot(datByConf2byQuant[1,2],datByConf2byQuant[1,3:7], #cond1, Ap-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='black',
        pch=15,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='Response Frequency (filled: Ap, unfilled: Av)',ylab='RT-quantiles',
        axes=F,
        main='QP plots')
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
par(new=T)
matplot(1-datByConf2byQuant[1,2],datByConf2byQuant[1,8:12], #cond1, Av-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='black',
        pch=0,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='',ylab='',
        axes=F)
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
par(new=T)
matplot(datByConf2byQuant[2,2],datByConf2byQuant[2,3:7], #cond2, Ap-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='blue',
        pch=15,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='',ylab='',
        axes=F,
        main='')
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
par(new=T)
matplot(1-datByConf2byQuant[2,2],datByConf2byQuant[2,8:12], #cond2, Av-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='blue',
        pch=0,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='',ylab='',
        axes=F)
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
par(new=T)
matplot(datByConf2byQuant[3,2],datByConf2byQuant[3,3:7], #cond3, Ap-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='red',
        pch=15,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='',ylab='',
        axes=F,
        main='')
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
par(new=T)
matplot(1-datByConf2byQuant[3,2],datByConf2byQuant[3,8:12], #cond3, Av-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='red',
        pch=0,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='',ylab='',
        axes=F)
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
par(new=T)
matplot(datByConf2byQuant[4,2],datByConf2byQuant[4,3:7], #cond4, Ap-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='green',
        pch=15,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='',ylab='',
        axes=F,
        main='')
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
par(new=T)
matplot(1-datByConf2byQuant[4,2],datByConf2byQuant[4,8:12], #cond4, Av-choices
        xlim=c(0,1),ylim=c(400,4400),
        col='green',
        pch=0,
        cex=2,
        cex.lab=1.5,
        cex.axis=1.5,
        xlab='',ylab='',
        axes=F)
axis(2,at = seq(400, 4400, by = 200))
axis(1,at = seq(0, 1, by = accspread))
legend("topright",
       legend = c('RewardLowest_Ap','RewardLowest_Av', 'RewardLower_Ap','RewardLower_Av','RewardHigher_Ap','RewardHigher_Av','RewardHighest_Ap','RewardHighest_Av'),
       pch = c(15,0,15,0,15,0,15,0), 
       col = c('black','black','blue','blue','red','red','green','green'), 
       cex=1,bty="p")
```

![](Template_QPplots_DBS_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->
