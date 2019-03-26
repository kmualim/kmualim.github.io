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

# Early Stopping 
- has the effect of restricting optimization procedure to small volume of parameter space in neighbourhood. 
With L2 regularization, we are empirically modelling the cost function J with a quadratic approximation in the neighbourhood of empirically optimal values  of weights. 

L1: uses penalty term which encourages sum of absolute values of parameters to be small
L2: encourages sum of squares of parameters to be small

# Parameter sharing and tying 
Between two models performing same classification task but with somewhat different distributions. 
Model A with parameters w(A) and B with parameters w(B) map two different but related outputs. 
If we believe that the model parameters should be close to each other, we can leverage this through regularization. 
More popular way: force sets of parameters to be equal; i.e parameter sharing 
- allows a reduction in parameters 

# Sparse Representationos 
1. Weight decay(regularization), acts by placing a penalty directly on model parameters. 
2. Another strategy is to place penalty on activations of units in neural networks
<b> Sparse parametrization </b> occurs with L1 regularization, meaning that many parameters become zero. 
Representational sparsity describes a representationo where many elements of representation are zero. That is h, which is a function of x, represents information present in x, but does so with a sparse vector. 
Norm penalty regularization of representatino is perfoormed by adding to the loss function, J, a norm penalty of representation. 
- others include penalty derived from student t prior on representation, KL divergence penalties; both provide examples of strategies based on regularizing avg activation across several examples to be near some target value, such as a vector with 0.01 for each entry.  
- orthognoal matching pursuit : encodes x with representation h that solves constrained optimization problem. 

# Bagging & Other ensemble methods 
Bagging is a technique for reducing generalization error by combining several models. 
- train several different moodels separately, have all models vote on output for test examples, called model averaging. 
Model averaging usually works because diffetnt models will usually not make the same errors on test set. 
Error made by average predictioono oof all ensemble models = 1/k sum(error)

*If errors are perfectly correlated and c=v, mean squared error reduces to v, so model averaging does not help at all. 
In the case where errors are perfectly uncorrelated and c=0, expected squared error of ensemble = 1/k (v) 
- this means expected squared eerror is inversely proportional to ensemble size. 

Bagging allows same kind of model, training algorithm and objective function to be reused seveeral times. 
- involves constructing k different datasets via sampling with replacement

Boosting constructs an ensemble with higher capacity than individual models 
- applied to build ensembles of neural networks by incrementallyy adding neural networks to the ensemble. 

# Dropout 
- trains ensemble consisting of subnetworks that can be formed by removing nonoutput units from underlying base network. 
- can effectively remove unit from network by multiplying output value by 0 
Dropout seeks to approximate the approach of bagging, but with exponentially large number of neural networks. 
Training dropout would require using minibatch-based learning algorithm like SGD. 
Examples are loaded in minibatches, where a randomly sampled different binary mask to apply to input and hidden units in network; probability of a mask being sampled is a hyperparameter that requires tuning. 

Mask vector specifies which units to include, J defines cost of model by parameters Q and mask u. Dropout consists of minimizing the expectation value of J as a function of theata and miu. 
In dropout, models share parameters with each model inheriting a different subset of parameters while in bagging models are independent.  
In dropout, usually because models are so huge, tiny fraction of possible subnetworks are trained for a single step, parameter sharing causes remaining subnetworks to arrive at good settings of parameters. In dropout, all the models are trained to convergence on its own respective training set. 

+ computationally cheap 
+ does not limit type of model/training procedure 

Dropout being a regularization technique deecreases effective capacity of a model, thus to offset this, must lower when using dropout. 
With few labeled training examples, dropout is less effective. 
<b> Bayesian neural networks </b> outperform drropout on Alternative Splicing Dataset where fewer than 5,000 examples are available. When unlabeled data is available, unsupervised feature learning gets an advantage over dropout. 

Dropout trains not just bagged ensemble of models, but an ensemble of models that share hidden units. 
- each hidden unit must perform well regardless of which other hidden units are in model, hidden units prepared to be swapped and interchanged between models. 
Large portion of power of dropout comes from masking noise that is applied to hidden units
- adaptive destruction of information content of input rather than destruction of raw values of input 
- for example, if model learns hidden unit h(i) that corresponds to a nose, then dropping h(i) corresponds to erasing the information that there is a nose. 
Model must thus learn another h(i), that either redundantly encodes presencee of a nose or detects face by another feature. 
Traditional noise injection that add unstructured noise at input not able to randomlyy erase information about a nose unless magnitude of noise is so great that nearly all the information gets removed. 
Noise is multiplicative - whihc does not allow pathological solution to noise robustness problem 

## Batch Norm 
- reparametrizes model to introducee both additive and multiplicative noise on hidden units at training time. 
- improve optimization but noise can have reegularizing effect, making dropout unnecessary. 

# Adversarial Training 
In the context of regularization, one can reduce error rate on original i.i.d test set via adversarial training - training on adversarially perturbed examples from training set 
- discourages highly sensitive locally linear behavior by encouraging neetwork to be locally constant in neighborhood of training data; similar to introducing a local constancy prior into supervised neural nets 
The motivation is because neural networks are built out of primarily linear building blocks. In some experiments, overall function they implement proves to be highly linear as a result, linear functions are easy to optimize. Unfortunately, these values can change rapidly with numerous inputs which accounts to a very large amount if w is highdimensional. 
- means of accomplishing semi-supervised learning. 
At a point x not associated with label in dataset, the model itself assigns some label y. 
- model's label y may not be true label, but if model is high quality, then y" has high probability of providing true label. 
- classifier can then be trained to assign same label to x and x". 
Assumption: different classes usually lie on disconnected manifolds & small perturbation should not be able to jump from 1 class manifold to another class manifold. 

TODO; what is this even? 
# Tangent Distance, Tangent Prop and Manifold Tangent Classifier 

Many ML algorithms aim to overcome curse of dimensionalityy by assuming data lies near low-dimensional manifold 

1. Tangent Distance 
- nonparametric nearest neighbour algorithm in which metric used is not generic Euclidean distance but one that is <b>derived from knowledge of manifolds near which probability concentrates</b>.
It is assumed that we are trying to classify exmaples, and that examples on same manifold share same category. 
Since classifier should be invariant to local factors of variation that correspond to movement on manifold, thus makes sense to use as nearest neighbor distance between two points 

2. Tangent Prop
- trains neural net classifier w extra penalty to make each output f(x) of neuralnet locally invariant to known factors of variation, these factors of variation correspond to movement along manifold near which examples of same class concentrate. 
Local invariance is achieved by requiring the gradient of f(x) to be orthogonal to known manifold tangent vectors. 
- regularizer can be scaled by an appropriate hyperparameter, need to sum over manyy outputs rather than lone output described here for simplicity. 
- closely related to dataset augmentation 

Both cases, user of algorithm encodes his/her prior knowledge of task by specifying set of transformations that should not alter output of network. 
difference is that in case of dataset augmentation, network is explicitly trained to correctly classify distinct inputs that were created by applying more than an infinitesimal amount of transformations while tangent prop does not explicitly require visiting a new input point and analytically regularizes model to resist perturbation in the directions corresponding to specified transformation. 
- analytical approach only regularizes model to resist infinitesimal perturbation 
- infinitesimal approach poses difficulties for models based on ReLu; only shrink derivatives by turning units on/off. 

- related to <b> double backprop </b> & <b> adversarial training </b> 
Double BP regularizes Jacobian to be small, while adversarial training finds inputs near original inputs and trains model to produce same output on these as on the original inputs. 
Tan prop and dataset augmentation both require <b> model invariance to certain specified directions of change in input </b> . 
while Double BP and Adversarial training both require that model is invariant to ALL directions of change in input as long as change is small. 

- Autoencoders can estimate manifold tangent vectors by unsupervised learning and use these tangents to regularize a nn classifier as in tangent prop 







