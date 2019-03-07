# Estimator 
- Point estimation: best prediction of a quantiy of interest (whether this be a single parameter or a vector of parameters)
- Function estimation: best prediction of a value y given an input vector x(whether this is a parameter w or a function that maps x to y) 

# Bias of an estimator 
- defined as the subtraction of the expectation over the samples and the true underlying value of theta. 
An unbiased estimator is observed when the expectation over the data is equal to the true underlying value of theta such that bias = 0 
usually the mean of the training samples; in other words, it falls within the same distirbution as the training samples 

# Variance
- defined as the measure of how we expect the estimate of the underlying data to vary with each independently sampled portion of the data. 
just the variance of the training set

# Standard Error 
- estimated via an estimate of std deviation (either of the sample or the unbiased estimate of the std deviation) 
- estimation gets better with more samples 

Generalization error usually estimated using the sample mean of the test set; 
mean usually approximately distributed with normal distribution
- SE can thus be used to give the probability of the true expectation mean falling within an interval. 

# Mean-squared error 
Bias and variance are connected in a trade-off via MSE and closely linked to underfitting, overfitting and capacity. 
Increase in capacity (where capacity is defined as how well a model can fit the dataset) would increase variance and lower bias

# Consistency 
Almost-sure consistency defined as the convergence of the expected theta to the true theta. 
- ensures that bias of the estimator diminishes with increase data 

# Maximum Likelihood Estimator 
- defined as the function trying to find parameter estimates for a given statistical model by maximizing a likelihood function; in other words, 
minimizing the dissimilarity between the empirical distribution defined by training data and the model distribution
- metric of dissimilarity is KL divergence (defined by the expectation of the subtraction of the log(empirical distirbution of x) and 
the log(distribution of the model)
- minimizing the maximum likelihood/KL divergence can be seen as minimizing cross-entropy bet distributions 
- cross-entropy: any loss consisting of a negative log-likelihood bet empirical distibution defined by the training set and the probability distribution of the model. 

Rescaling the estimator: 
- usually take the log of the likelihood because the original equation is prone to numerical underflow
- dividing by a scalar m expresses the estimator as an expectation w.r.t the distribution of the data

# Conditional log-likelihood & MSE 
MLE can be generalized as estimating the parameters to maximize the conditional probability distribution of Y given X.

In linear regression, the model can thus be seen as producing a conditional distribution of p(y|x) to different y values that re all compatible to x. 
The maximization of conditional log-likelihood w.r.t parameters w can be reduced to minimizing the MSE w.r.t parameters w. 

## Maximum Likelihood properties 
Under given conditions, the max likelihood of a parameter converges to the true value of the parameter 
Condition 1. true distribution of the empirical distribution of the data given by training data falls within the model family. 
Condition 2. true distribution of the empirical distirbution of the training data must correspond to exactly one value of theta; 
otherwise while the max likelihood can determine the correct distribution, it cannot determine the correct parameter value that led to 
the data-generating process. 

While maximum likelihood estimators share similar properties to consistent estimators, it is the preferred estimator of choice in ML because of : 
1. statistical efficiency - where one consistent estimator may reach a lower generalization error with a fewer # of examples.
- usually studieed in the parametric case; where thee goal is to estimate value of parameter and not of the function. 

# Bayesian Statistics 
- uses the probability to reflect degrees of uncertainty in states of knowledge
true parameter seen as a random variable, not fixed; usually represented using prior distribution (uniform/Gaussian distribution with high entropy) 
With successive observation of the data, posterior loses entropy and concentrates around highly likely values of the parameteer

It differs from maximum likelihood estimation in 2 ways: 
1. MLE makes predictions using point estimation of theta, while Bayesian estimation makes predictions using the full distribution over theta
- every value of theta with positive probability distribution thus contributes to the prediction, weighted by the posterior density.
MLE calculates uncertainty in a given point estimate via evaluating variance, Bayesian estimation integrates over the uncertainty. 
2. Contribution of Bayesian prior distribution - shifts probability mass density towards regions of parameter space preferred a priori. 
- cannot begin bayesian learning with infinitely wide prior of w 
- Bayesian estimate provides covariance matrix, shows how likely different values of w are. 

# Maximum a Posteriori (MAP) Estimation 
- chooses point of maximum posterior probability; utilizes prior distribution 
- introduction of the prior distribution helps to lower variance 

# Probabilistic Supervised Learning







