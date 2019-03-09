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
- 
