# Deep Tensor Factorizations

An interesting idea to impute epigenomics data

A simplier but similar idea to Deep Tensor Factorizations

# Probabilistic Matrix Factorization 

An Optimization problem with loss functions and constraints. Given a sparse matrix R, most of the values of R are empty.
Making predictions for empty values of R by approximating non-empty values in R via decomposition. 
PMF : learning models using maximum a posterior approximation, where (MAP) estimate is an estimate of unknown quantity that equals the mode of posterior distribution. 
SVD, [PCA](/_posts/ml-basic.md#L120) : decompose original sparse matrix into product of 2 low rank orthogonal matrices 
SVD, or Low rank matrix factorization, tries to minimize L2 loss of matrix approximation by multiplying 2 low rank matrices. 
However MAP objective of PMF is equivalent to the L2 loss of SVD with weight decay. 

## Case Study: A widely used application in Collaborative filtering in Recommendation Systems. 
What is Collaborative filtering? 
- methods based on collecting and analyzing large amounts of information on users' behaviors, activities or preferences and predicting what users will like based on similarity to other users. 
- does not require an "understanding" of the item itself since it does not rely on machine analyzable content 
Assumption: people who agree in the past will agree in the future. 

## How do these methods suffer? 
Cold Start: systems often require lage amount of existing data on user in order to make accurate recommendations. 
Scalability: Large amount of computation power is necessary to calculate recommeendations in the case of millions of users/products 


## PMF in Deep Learning? 
- 
