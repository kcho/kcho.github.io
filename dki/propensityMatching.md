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

    




<iframe width="800" height="700" src="http://cran.at.r-project.org/web/packages/nonrandom/vignettes/nonrandom.pdf" frameborder="0" allowfullscreen></iframe>

##Practical
    
    nonrandom
    relative.effect()
    pscore()
    plot.pscore()
    ps.makestrata()
    ps.match()

* tool for a comprehensive data analysis using stratification, matching and covariate adjustment by PS


