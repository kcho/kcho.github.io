#Propensity score matching


##Summary

* first published by Paul Rosenbaum and Donald Rubin in 1983
* Matching attempts to mimic randomization by creating a sample of units that received the treatment that is comparable on all observed covariates to a sample of units that did not receive the treatment
* PSM attempts to control for these differences to make the groups receiving treatment and not-treatment more comparable.
* used to eliminate imbalances in baseline covariate distributions between groups

<iframe width="800" height="700" src="http://en.wikipedia.org/wiki/Propensity_score_matching" frameborder="0" allowfullscreen></iframe>



##Introduction

- propensity score(PS)
    - conditional probability of receiving a certain treatment given covariates
    - has to be estimated via logistic regression
    - It aims to eliminate the imbalances in the covariate distributions between groups

Four PS based methods | characteristics
---|---
stratification|used to group individuals with similar or equal PS
matching|used to match one or more subjects
covariate adjustment|easy to apply
inverse probability weighting|weighted regression


##The estimation of PS

###Selection of PS model :

    relative.effect()

- which covariates to include in the PS model
    - age
    - sex
    - handedness
    - education
    - IQ

- Define output, treatment and covariates

```
df.effect <- relative.effect(data = df,
                             formula = output~treatment+cov1+cov2+etc)
```

###Estimation of PS :

    pscore()  and  plot.pscore()

If covariates needed for the PS estimation are determined, a logistic regression model is fitted(internal use of glm()) assuming a binary treatment variable

```
df.ps <- pscore(data = df,
                formula = therapie~cov1+cov2)
```

####Density estimation of the estimated PS

```
plot.pscore(df.ps,
            main = "df study",
            with.legend = TRUE,
            par.1 = list(lty=1, lwd=2),
            par.0 = list(lty=3, lwd=2),
            xlab = "",
            ylim = c(0,4.5))
```

<iframe width="800" height="700" src="http://cran.at.r-project.org/web/packages/nonrandom/vignettes/nonrandom.pdf" frameborder="0" allowfullscreen></iframe>



##PS based methods

Observational and registry data frequently *present imbalances in covariate distributions* between treatment groups. 

Stratification and matching by PS can be used to eliminate these imbalances by creating data situation as in RCTs.

###Stratification by PS

individuals --> groups : by similar or equal values for the stratification variable

    ps.makestrata()
    stratified.by #defines the stratification variable in the data

###Matching by PS

    ps.match()

##Practical
    
    nonrandom
    relative.effect()
    pscore()
    plot.pscore()
    ps.makestrata()
    ps.match()

* tool for a comprehensive data analysis using stratification, matching and covariate adjustment by PS


