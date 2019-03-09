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
Also, if 














