# Deep FeedForward Networks 
- usually requires iterative grad-based optimizer unlike linreg (linear equation solver) or logreg (convex optimization algorithm) 

SGD usually applied to non-convex optimization problems 

## Learning Conditional Statistics 
- often would only want to learn just a single conditional statistic of y given x 
- cost function can be viewed as functional (mapping from functions to real numbers) rather than a function 
As a functional, the minimum could thus occur at some specific function 
- if trained on infinitely many samples from true data distribution, minimizing the MSE cost function gives a function that predicts 
mean of y for each value of x. 
- MAE : median value of y for each x. 
MSE and MAE cost functions usually not desirable; output units produce small gradients if these cost functions are used. 

## Linear Units for Gaussian Output Distributions 
- maximizing log-likelihood is equivalent to minimizing MSE 
- max likelihood makes it easy to learn cov matrix; make cov function of input; cov must be constrained to positive definite 
matrix for all inputs. 

## Sigmoid Units for Bernoulli Output Distributions 
- unable to use linear units for Bernoulli because if values strayed from interval (0,1), value = 0 
- too many zeros prevent the model from learning 
- applying Sigmoid Units: uses linear layer to transform z = wTh+b and converts the value into a probability 
log in cost function undoes the exp of the sigmoid and prevents saturation of the sigmoid unit. 
- with large incorrect values, softplus tries to correct for this by returning the argument to its absolute value 
- allows for quick correction of mistaken z via gradient-based learning 
- train sigmoid units with maximum likelihood 

## Softmax Units for Multinoulli Output Distribution 
- used to represent a probability distribution over a discrete variable with n possible values; vector of n probabilities sum up to 1 
- when maximizing log-likelihood, the equation constitutes 2 terms - first term shows that the input z always has a direct contribution to cost function whilst second term encourages all of z to be pushed down
Second term: exp(zk) is insiginifcant for any zk that is noticeably less than maxjzj. 
- max log-likelihood penalizes most active incorrect prediction 
- output values can saturate when differences between input values become extreme, driven by amount that arg deviate from max(z) 

## Mixture Density Networks (pg 185) 
- Neural network with Gaussian mixtures 
- predict real values from conditional distribution p(y|x) that can have several different peaks in y space for same value of x. 
- 1. mixture components - form multinouolli distribution over n different components associated with latent variable c; obtained by softmax over n-D vector to guarantee outputs are + and sum to 1
- 2. means: indicate mean associateed with ith Gaussian component and are unconstrained; neg log-likelihood weighs example's contribution to loss for each component * P(component produced example) 
- 3. covariances: - cov matrix for each component i. GD would automatically follow correect proceess if given correct specification ; GD of conditional Gaussian mixtures can be unrealiable tho
    - due to divisions 
- represents multiplee output modes + control variance of output

## Selecting Hidden Units 
- some hidden units are nondifferentiable at specific points. 
- differentiability occurs only when both left and right derivatives are defined and equal to each other 

1. ReLu : g(x) = max{0,z} 
- derivatives through ReLu unit remains large whenever unit is active 
- let bias = 0.1; allow ReLu to be initially active for most inputs in training and allow derivatives to pass through 
- cannot learnr via gradient-based methods on examples for which activation is zero. 
Maxout units generalize ReLu further, divide z into groups of k values and each maxout unit then outputs maximum element of one of these groups; learns piecewise linear function that responds to multiple directions in the input x space; learning the activation function. 
- parametrized by k weight vectors instead of 1, usually requires more regularization 
- each unit driven by multiple filters, maxout units have redundancy to prevent <b> catastrophic forgetting </b> 

2. Logistic Sigmoid and Hyperbolic Tangent 
- saturation of sigmoidal units make gradient based learning v difficult; requires appropriate cost function to undo saturation 
- hyperbolic tangent activation function usually performs better than log sigmoid; resembles identity function more closely
- training deep neural network with tanh functions resemebles training linear model 
In cases where use of piecewise linear activation functions might not be suitable, sigmoidal units may be more appealing. 

Other hidden units: radial basis function, softplus, hard tanh 















