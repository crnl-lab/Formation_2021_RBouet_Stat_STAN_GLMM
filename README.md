# Formation_2021_RBouet_Stat_STAN_GLMM

**UNDER CONSTRUCTION !!!!!!**    



***
A general approach to **statistical inference** tends to rely less on inference about a particular hypothesis and more on parameter estimation. The basic idea is to fit a **model** whose parameters describe substantive hypotheses about the generating sources of the dataset, and then to interpret these parameters based on their magnitude and the precision of the estimate. The key tool for this kind of estimation is not tests like the t-test or the chi-squared. Instead, it's typically some variant of regression, usually mixed effects models.   
 
 
These models (also known as hierarchical linear models) let you estimate sources of **random variation** ("random effects") in the data across various grouping factors. For example, in a reaction time experiment some participants will be faster or slower (and so all data from those particular individuals will tend to be faster or slower in a correlated way). Similarly, some stimulus items will be faster or slower and so all the data from these groupings will vary. The lme4 package in R was a game-changer for using these models (in a **frequentist** paradigm).   
 
 
How do you reason about the relationship between your data and your hypotheses ? **Bayesian** inference provides a way to make normative inferences under uncertainty. We are interested in knowing the probability of some hypothesis given the data we observe.    
Bayesian statistical framework offers unique advantages, for example in terms of inter- pretability of estimates and the flexibility of fitting.   
 
 
Enter Bayesian methods. For several years, it's been possible to fit Bayesian regression models using **Stan**, a powerful probabilistic programming language that interfaces with R. Stan, building on BUGS before it, has put Bayesian regression within reach for someone who knows how to write these models (and interpret the outputs). But in practice, when you could fit an lmer in one line of code and five seconds, it seemed like a bit of a trial to hew the model by hand out of solid Stan code (which looks a little like C: you have to declare your variable types, etc.).     

# Modelisation

Bayesian inference for GLMs with group-specific coefficients that have unknown covariance matrices with flexible priors.    
The **stan_glmer** function is similar in syntax to glmer but rather than performing maximum likelihood estimation of generalized linear models, Bayesian estimation is performed via MCMC. The Bayesian model adds priors on the regression coefficients and priors on the terms of a decomposition of the covariance matrices of the group-specific parameters.    
We build all possible models.     
This will allow us to have an estimation of the posterior distributions.    
We have to save the diagnostics files for futur models comparaison.    


```{r, warning=FALSE, fig.align='center', message = FALSE}
model.stan.00 <- stan_glmer(Ratio~ 1 + (1+Window|Patient) + (0+Stade|Patient), 
                            data = filter(Datas, Window != "Midle", Window != "Last"),
                            diagnostic_file = "~/Datas/R/Baysian/test_STAN/diagnostic_00.csv")
```
