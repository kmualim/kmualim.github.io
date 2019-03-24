# Regularization for Deep Learning 
- making an algorithm perform well on new inputs, usually through regularizing estimators 
In regularizing estimators, we make a tradeoff between increasing bias to reduce variance 
Some regularization strategies are listed below: 

# Parameter Norm Penalties
- limiting capacity of models by adding parameter norm penalty to objective function 
- this penalty is governed by a hyperparameter that weights the relative contribution of this norm penalty term.
For neural networks: 
- penalize weights of affine transformation at each layer & leave biases unregularized 
- desirable to use separate penalty with different alpha coefficient for each layer of network

## 1. L2 Parameter Regularization 
- weight decay seeks to drive the weights closer to origin by adding a regularization term to the objective function 
- multiplicatively shrink weight vector by constant factor on each step, before performing usual gradient update 
For the entire course of training, we make a quadratic approximation to the objective function in the neighborhood of the value of weights that obtains 
minimal unregularized training cost 
*review the math behind Hessian matrix and how it decomposes* 
Basically, regularization seeks to heavily penalize directions that do not contribute significantly to reducing the objective function; pulling these weights closer to zero.
In directionos that do not contribute to reducing objective function, a small eigenvalue of the Hessian tells us movement in this direction will not significantly increase the gradient. 
*L2 regularization math*

## 2. L1 Parameter Regularization 
- defined as the sum of absolute values of the individual parameters. 
Similar to L2, L1 weight decay controls strength of regularization by scaling penalty 
- regularization is a constant factor with sign equal to sign(w(i)) 
- L1 penalty does not admit clean algebraic expressions in the case of a fully general Hessian. 
Assumption: if data for linear regression problem has been preprocessed to remove all correlation between input features via PCA, Hessian can be assumed to be diagonal. 
L1 can be decomposed to a quadratic approximation that has an analytical solution. 
- results in a more sparse solution 

L2 does not cause parameters to become sparse while L1 regularization would do so for large hyperparameter, alpha. 
While L2 is equivalent to MAP Bayesian inference with a Gaussian prior on the weights, L1's penalty term used to regularize a cost function is equivalent to log-prior term that is maximized by MAP Bayesian inference, with prior being an isotropic Laplae distribution over w. 

This intrinsic characteristic of L1 Regularization makes it good in its use as a feature selection mechanism. 
- causes subset of weights to become zero, thus allowing these corresponding features to be safely discarded. 

# Norm Penalties as Constrained Optimization 
(?) From 4.4, able to minimize function subject to constraint by constructing Lagrange function, consisting of original objective function + set of penalties. 
Each penalty is a product between a coefficient (KKT multiplier) & function representing whether constraint is satisfied. 
- If we wish to apply a constrain to our norm penalty, then we could construct the equation as the following Equation 7.26. 
- to solve this problem, need to modify both theta and alpha (regularization hyperparameter). 
The hyperparameter controlling the norm penalty, however, would follow the corresponding rules: 
1. increase whenever the norm penalty > k 
2. decreases whenever the norm penalty < k 
- optimal value of alpha would encourage the norm penalty to shrink but not beyond the constraint, k. 

TODO: (why is this the case.... that increasing alpha would make the constraint smaller) 

Let's fix alpha and view the problem as a function of the theata
- if L2/L1 norm, the weights are constrained to lie in either L2/L1 region. 
- increasing/decreasing alpha would grow/shrink constraint region -> larger alpha results in smaller constraint region and vice versa. 
Enforcing absolute upper bound as opposed to a strict L1/L2 regularization. 
1. Adding a constaint is useful in finding the correct estimation via sgd, that satisfies a particular inequality. (eg. having the norm penalty be less than k). Thus, this narrows the search in estimating parameters. 
2. Another reason to use explicit constraints would be that penalities can causes nonconvex optimization procedures to get stuck in local minima when associated with small parameters. 
When the weights going into and out of units in a neural network are very small, we consider these units to be "dead units" as they stop contributing much to the behavior of the function learned byy the network. 
Explicit constraints do not encourage the weights to approach the origin and thus do not encounter a similar problem. 
- have an effect only when weights are large and want to leave constraint region. 
- impose stability on optimization procedure; prevent feedback loop of continual increase in magnitude of weights without bound 
Recommended: using constraints combined with high learning rate to enable rapid exploration
- constrain norm of each column of weight matrix of a nn layer instead of the Frobenius norm of entire weight matrix
- similar to using separate KKT multiplier for weights of each hidden unit, each KKT dynamically updated separately to make each hidden unit obey constraint. 

Linear porblems have closed form solutions when matrix is invertible; we usually seek to make X^TX + aI invertible instead. 
Most forms of regularization will guarantee convergence of iterative methods applied to underdetermined problems.
*Moore-Penrose pseudoinverse* : stabilizing underdetermined problems using regularization

# Data Augmentation 

