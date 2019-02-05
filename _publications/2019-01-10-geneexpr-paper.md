---
title: "Applying deep learning to gene expression - a review"
excerpt: "Improving current baselines and methodologies to enable more accurate gene expression inference"
collection: publications
date: 2019-01-10
location: "Palo Alto, CA & Montreal, Quebec"
---

# Deep learning on gene expression inference  

One of the greatest progressions in Biology has been attributed to employing gene expression profiling to understanding the expression of thousands of genes under given circumstances. Gene expression profiling has served in understanding cellular functionality and differentiation during disease pathogeneity as well as in determining the regulatory mechanisms associated with different system perturbations. 

## Data 

Since the discovery of the LINCS Consortium, where ~1,000 carefully selected genes could capture approximately 80% of the information present in cMap data, researchers have often used expression signatures of landmark genes to characterize cellular states of samaples under various experimental conditions. The expression profiles of the remaining genes can then be computationally inferred based on existing expression profiles. Currently, this inference utilizes linear regression - a model that inevitably ignores the nonlinearity within gene expression profiles. 

## The Model 

[Chen et al.](files/geneexpr.pdf) were one of the first to apply deep neural networks to multi-task regression problem for gene expression inference. The authors constructed a fully connected neural network that outperformed linear regression. A re-implementation of the paper and an attempt to improve baseline comparisons were partially successful - given limited computational power. 
 Alternatively, [Wang et al.](files/gans-geneexpr.pdf) were one of the first to utilize aa novel GAN for the problem of gene expression inference. The GAN implemented is conditioned on target genes from a given gene expression profile of landmark genes. The generator is a convolutional DenseNet, 3 layers with 9000 hidden units each. 
 

## Concerns to address

The application of GANs to gene expression inference is an incredibly fascinating experiment that seems predictably good at outperforming previous implementations of resolving this task - such as linear regression, k nearest neighbours and most recently deep neural networks. However, the use of DenseNet on data without any obvious or underlying spatial structure is perplexing and intriguing. A successful attempt to overcome this obstacle could allow its extension and generalization to other similar datasets. The lack of a given open source implementation of this model on gene expression hence serves as a bottleneck in advancing the progression of its applications. 

(in progress) [Code for GAN Implementation on MNIST](https://github.com/kmualim/DCGAN-Keras-Implementation)
