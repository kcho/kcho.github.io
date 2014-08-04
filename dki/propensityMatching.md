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


##Using "MatchIt"

###Example

```
# Email to ehsan at alumni.ubc.ca to report error/suggestions

################################################################
###### Synthetic Data Generation
################################################################

n = 3500
x1 = rnorm(n, 1, 100)
x2 = rnorm(n, 10, 100)
x3 = rnorm(n, 5, 1)
x4 = rnorm(n, 10, 10)
x5 = rbinom(n, 1, .4)
x6 = rnorm(n, 30, 5)
treatment = rbinom(n, 1, .15)
data = cbind(x1,x2,x3,x4,x5,x6, treatment)
dim(data)

################################################################
###### Propensity score matching
###### nearest neighbor matching (1:1)
################################################################

install.packages("MatchIt")
require(MatchIt)
# data1 is the subset of data with only the selected variables mentioned below
data1 = data[,c("x1","x2","x3","x4","x5","x6", "treatment")]
# getting rid of missing values (below)
data1 = as.data.frame(na.omit(data1)) 
# matching is performed below using propensity scores given the covariates mentioned below
m.out = matchit(treatment~x1+x2+x3+x4+x5+x6,method="nearest", data=data1, ratio = 1)
# check the sample sizes (below)
m.out 
# Final matched data saved as final_data
final_data = match.data(m.out) 
# (here distance = propensity score)
# After performing command below check your computer for NN.csv file that can be imported in SPSS
write.csv(final_data, file = "matchNN.csv")
# check balance (below)
plot(m.out) # covariate balance
plot(m.out, type = "jitter") # propensity score locations
plot(m.out, type = "hist") #check matched treated vs matched control


################################################################
###### Propensity score matching
###### caliper matching
################################################################

require(MatchIt)
# data1 is the subset of data with only the selected variables mentioned below
data1 = data[,c("x1","x2","x3","x4","x5","x6", "treatment")]
# getting rid of missing values (below)
data1 = as.data.frame(na.omit(data1)) 
m.out.test = matchit(treatment~x1+x2+x3+x4+x5+x6,method="nearest", data=data1, ratio = 1)
test_data = match.data(m.out.test) 
ps.sd = sd(test_data$distance)
# matching is performed below using propensity scores given the covariates mentioned below
# caliper = 0.25 times sd of propensity scores (optimal)
m.out = matchit(treatment~x1+x2+x3+x4+x5+x6,method="nearest", data=data1, caliper = 0.25*ps.sd)
# check the sample sizes (below)
m.out 
# Final matched data saved as final_data
final_data = match.data(m.out) 
# (here distance = propensity score)
# After performing command below check your computer for matchC.csv file that can be imported in SPSS
write.csv(final_data, file = "matchC.csv")
# check balance (below)
plot(m.out) # covariate balance
plot(m.out, type = "jitter") # propensity score locations
plot(m.out, type = "hist") #check matched treated vs matched control



################################################################
###### Propensity score matching
###### nearest neighbor matching (1:4)
################################################################

require(MatchIt)
# data1 is the subset of data with only the selected variables mentioned below
data1 = data[,c("x1","x2","x3","x4","x5","x6", "treatment")]
# getting rid of missing values (below)
data1 = as.data.frame(na.omit(data1)) 
# matching is performed below using propensity scores given the covariates mentioned below
m.out = matchit(treatment~x1+x2+x3+x4+x5+x6,method="nearest", data=data1, ratio = 4)
# check the sample sizes (below)
m.out 
# Final matched data saved as final_data
final_data = match.data(m.out) 
# (here distance = propensity score)
# After performing command below check your computer for matchNN4.csv file that can be imported in SPSS
write.csv(final_data, file = "matchNN4.csv")
# check balance (below)
plot(m.out) # covariate balance
plot(m.out, type = "jitter") # propensity score locations
plot(m.out, type = "hist") #check matched treated vs matched control

################################################################
###### Propensity score matching 
###### subclassification by Propensity score
################################################################

require(MatchIt)
# data1 is the subset of data with only the selected variables mentioned below
data1 = data[,c("x1","x2","x3","x4","x5","x6", "treatment")]
# getting rid of missing values (below)
data1 = as.data.frame(na.omit(data1)) 
# matching is performed below using propensity scores given the covariates mentioned below
m.out = matchit(treatment~x1+x2+x3+x4+x5+x6, method = "subclass", subclass = 4, data=data1)
# check the sample sizes (below)
m.out 
# Final matched data saved as final_data 
final_data = match.data(m.out) 
# (here distance = propensity score and subclass = the subclass variable)
# ****put this subclass in the final outcome model****
# After performing command below check your computer for matchSC.csv file that can be imported in SPSS
write.csv(final_data, file = "matchSC.csv")
# check balance (below)
plot(m.out) # covariate balance
plot(m.out, type = "jitter") # propensity score locations
plot(m.out, type = "hist") #check matched treated vs matched control

################################################################
###### Propensity score matching
###### full matching
################################################################
install.packages("optmatch")
require(optmatch)
require(MatchIt)
# data1 is the subset of data with only the selected variables mentioned below
data1 = data[,c("x1","x2","x3","x4","x5","x6", "treatment")]
# getting rid of missing values (below)
data1 = as.data.frame(na.omit(data1)) 
# matching is performed below using propensity scores given the covariates mentioned below
m.out = matchit(treatment~x1+x2+x3+x4+x5+x6,method="full", data=data1)
# check the sample sizes (below)
m.out 
# Final matched data saved as final_data
final_data = match.data(m.out) 
# (here distance = propensity score)
# After performing command below check your computer for matchF.csv file that can be imported in SPSS
write.csv(final_data, file = "matchF.csv")
# check balance (below)
plot(m.out) # covariate balance
plot(m.out, type = "jitter") # propensity score locations
plot(m.out, type = "hist") #check matched treated vs matched control
```

<iframe width="800" height="700" src="http://imai.princeton.edu/research/files/matchit.pdf" frameborder="0" allowfullscreen></iframe>


##Script for my data


<br>
<br>
<br>
<br>
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




##PS based methods

Observational and registry data frequently *present imbalances in covariate distributions* between treatment groups. 

Stratification and matching by PS can be used to eliminate these imbalances by creating data situation as in RCTs.

###Stratification by PS

individuals --> groups : by similar or equal values for the stratification variable

    ps.makestrata()
    stratified.by #defines the stratification variable in the data

###Matching by PS

The most popular PS method to cope with covariate imbalances is matching by PS

    ps.match()

One or more untreated individuals are matched to treated individuals (or vice versa) according to the estimated PS

- depends both on the 
    - class and 
    - the numbers of the input objects

- treatment variable is not necessarily needed since it is alrady stored in $treat

- in ps.match()
    - possible to pass two df by using the argument "object.control"
    - one df for treated individuals and a second df for the untreated individuals





##Practical
    
    nonrandom
    relative.effect()
    pscore()
    plot.pscore()
    ps.makestrata()
    ps.match()

* tool for a comprehensive data analysis using stratification, matching and covariate adjustment by PS


<iframe width="800" height="700" src="http://cran.at.r-project.org/web/packages/nonrandom/vignettes/nonrandom.pdf" frameborder="0" allowfullscreen></iframe>
