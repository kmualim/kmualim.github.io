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
minimal unregularized trianing cost 
