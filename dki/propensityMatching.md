#Propensity score matching


##Background

* first published by Paul Rosenbaum and Donald Rubin in 1983
* Matching attempts to mimic randomization by creating a sample of units that received the treatment that is comparable on all observed covariates to a sample of units that did not receive the treatment
* PSM attempts to control for these differences to make the groups receiving treatment and not-treatment more comparable.
* used to eliminate imbalances in baseline covariate distributions between groups

<iframe width="800" height="700" src="http://http://en.wikipedia.org/wiki/Propensity_score_matching" frameborder="0" allowfullscreen></iframe>

##Practical
    
    nonrandom
    relative.effect()
    pscore()
    plot.pscore()
    ps.makestrata()
    ps.match()

* tool for a comprehensive data analysis using stratification, matching and covariate adjustment by PS

<iframe width="800" height="700" src="http://cran.at.r-project.org/web/packages/nonrandom/vignettes/nonrandom.pdf" frameborder="0" allowfullscreen></iframe>

