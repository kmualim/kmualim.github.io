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

## Understanding the difference between MAP and MLE 
- data and model parameters are inputs to the likelihood function 
Likelihood function: 
When given fixed value of model parameters, what is the probability of any particular data point/data set? 
On the other hand, when data is kept fixed, what is the probability of any particular parameter setting? 
MLE simple gives you the mode of the likelihood in scenario 2. 
However, MLE frequently overfits the data, variance of parameter estimates is high causing the outcome of the parameter estimate to be sensitive to r.v in data. 
In these cases, we implore adding regularization to MLE (aims to reduce variance by introducing bias into estimate). 
In MAP, regularization is achieved by assuming that the parameters are drawn from a random process. This prior belief about parameters determine what this random process looks like. 
When these prior beliefs are strong, the observed data has little impact on parameter estimates. However, when these prior beliefs are weak, thee outcome is more like standard MLE. 
Thus, in the case for an infinite amount of data and an infinitely weak prior belief, MAP produces the same results as MLE. 

# Probabilistic Supervised Learning

## Logistic Regression 
- log sigmoid function squashes output of lienar function into interval; value is interpreted as a probability
- optimal weights are found via: minimizing negative log-likelihood using gradient descent 

## Support Vector Machines (SVM) 
- outputs class identities 
- lends itself to the kernel trick; enables learning models that are nonlinear as a function of x & more computationally efficient than naively constructing 2 vectors 
Gaussian kernel (a.k.a radial basis function) 
- performs template matching; training example x associated with training label y becomes a template for class y
- if x' is near x template according to euclidean distance, then the model puts large weights on corresponding y label. 

## k-nearest neighbours 
- returns the average of corresponding y values in training set based on k-nearest neighbours to X
- does not learn features/patterns in the data 
- non-parametric method 

## Decision trees 
- each node of decision tree is associated with a region in input space, with axis-aligned splits and constant outputs within each node 
- decision boundary has to be axis-aligned 
- uses separate parameter for each region in input space 

# Unsupervised Learning 
- to put it simply, attempts to extract information from distribution that does not require human labor to annotate examples. 
- the goal is to find a representation that preserves as much information about x while keeping the representation simpler 

## Simplier representation 
- lower-dimensional (compress as much information about x as possible) 
- sparse (embed dataset into represeentation whose entries are mostly zeros; usually requires increeasing dimensionality of representation) 
- independent (disentangle sources of variation underlying data distribution)

# Principle Component Analysis (PCA) 
- dimensionality reduction technique for extracting relevant information from datasets
- learns orthogonal, linear transformation and reduces a complex data set to a lower dimension to reveal any hidden, simplified structures that underlie it. 
Assumption: re-expresses data as a linear combination of its basis vectors 
Simply put, Let X be the original dataset, where each column is a single sample of our dataset and Y is a new representation of that dataset, where Y is related to X by a linear transformation P (PX=Y). 
P is a matrix that essentially transforms X into Y. 
With this key idea in mind, How then should we best re-express X? What is a good choice of basis P? 

High signal-to-noise ratio, indicative of high precision measurement + (large variance ?)
Redundancy lurks in our dataset, where certain measurements may have only required fewer than recorded variables. Given these two characteristics allows PCA to work. But how do we seek to find these characteristics in higher dimensions? 

## Covariance matrices 
Taking for example, two sets of measurements with zero means. 
The covariance between A and B is a straight-forward generalization, as covariance measures degree of linear r/s between two variables. 
- Large postive value indicates positively correlated data while a large negative value denotes negatively correlated data
Absolute magnitude of covariance measures degree of redundancy
- σAB = 0 if A,B is uncorrelated 
- σAB^2 = σA^2 if A=B 
Convert the set of measurements, (A, B .... etc) , into corresponding row vectors of a matrix X where each row of X corresponds to all measurements of a particular type and each column of X corresponds to a set of measurements from one particular trial. 
Covariance matrix C(x) = (1/n)(X)(X^T)
- diagonal terrms of C(x) are the variance of particular measurement types and the off-diagonal terms of C(x) are the covariance between measurement types 
Cx captures covariance between all possible pairs of measurements, with values reflecting noise and redundancy in measurements. <br> 

## Diagnalizing the Covariance Matrix 
PCA seeks the simpliest method and assumes that all basis vectors are orthonormal. 
1. Select normalized direction in m-dimensionoal space along which variance in X maximized -> p1 
2. Find another direction where variance is maximized (restricting search to all directions orthogonal to previous selected directions) -> pi 
3. Repeat until all m vectors selected 
Resulting ordered set of p's are the <b>principal components</b>. 
PCA can be solved using eigenvector decomposition  

## k-means clustering 
- divides training set into k different clusters of examples that are near each other 
- k-dimensional one-hot code vector h where h(i)=1 if x belongs to cluster i
- no single criterion that measures how well clustering of the data corresponds to real world 

## local constancy 
- if we know a good answer for input x, then that answer is probablyy good in the neighbourhood of x 

## local kernel 
- k(u,v) is large when u=v, measures how closely a test eexmaple x resembles each training example x

Local generalization and smoothness/local constancy prior only guarantees a guess is correct if the new point lay within the same grid square as a training example 
- works really well if and onlyy if there are enough examples for learning algorithm 
Deep learning assumes that the data was generated by composition of factors, features 

# Manifold learning 
- connected region of a small num of degrees of freedom embedded in a higher-dimensional space; appears to be Euclidean space 
- each dimension corresponds to a local direction of variation, dimensionality of manifold varies from one point to another 
- assumes that most of R(n) consists of invalid inputs with interesting inputs occur only along collection of manifolds containing small subset of points; with variations in ouput of learned function occuring only along directions that lie on manifold
1. probability distribution over things that occur in real life is highly concentrated 
2. examples we encounter are connected to each other by other examples, with each example being surrounded by other highly similar examples that can be reached by transformations to traverse manifold 


