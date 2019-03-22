# Probabilistic Matrix Factorization 
An Optimization problem with loss functions and constraints. Given a sparse matrix R, most of the values of R are empty.
Making predictions for empty values of R by approximating non-empty values in R via decomposition 

PMF : learning models using maximum a posterior approximation, where (MAP) estimate is an estimate of unknown quantity that equals the mode of posterior distribution. 

SVD, PCA : decompose original sparse matrix into product of 2 low rank orthogonal matrices 
SVD, or Low rank matrix factorization, tries to minimize L2 loss of matrix approximation by multiplying 2 low rank matrices. 
 
However MAP objective of PMF is equivalent to the L2 loss of SVD with weight decay. 


