---
title: "Training Generative Adversarial Networks (GANs)"
excerpt: "A brief introduction into GANs and training one"
collection: publications
date: 2019-02-05
location: "Palo Alto, CA"
---

# What is a GAN? 
Generative Adversarial Networks (GANs) were introduced in this [paper](https://arxiv.org/abs/1406.2661) by Ian Goodfellow and other researchers located at the Universite de Montreal. A Generative Adversarial Network falls into the cateogry of [generative models](https://en.wikipedia.org/wiki/Generative_model), that have the ability to produce new content. 
A particular GAN, utilizes both generative and discriminative models, the [two distinguished classes](http://papers.nips.cc/paper/2020-on-discriminative-vs-generative-classifiers-a-comparison-of-logistic-regression-and-naive-bayes.pdf) defined in [statistical classification](https://en.wikipedia.org/wiki/Generative_model).
A clear discriminating definition between the two is that discriminative models <b>learn boundaries</b> between classes 
while generative models <b>models the distrirbution</b> of individual classes. <br> 
[MLEngineer](https://medium.com/@mlengineer/generative-and-discriminative-models-af5637a66a3) has also written a quick analogy to illustrate generative v discriminative models. 
Some standard examples of the two could include as generative classifiers: naive bayes classifier and linear discriminant analysis; discriminative models: logistic regression. 

TL;DR The generator produces new images and passes it to the discriminator model that decides if image it receives is a fake. 

## How do GANs ctually work? 
A classic analogy for a GAN takes the case of the police (discriminator) and the counterfeiter (generator). The counterfeiter (generator) creates new images and passes it to the police (discriminator), where the generated images gets evaluated for its authenticity. The police (discriminator) then provides feedback by comparing generated images with real images. The police (discriminator) strives to identify the images coming from the counterfeiter (generator) as fake whilst the counterfeiter (generator) seeks to generate images authentic enough to pass as real. 

![](https://github.com/kmualim/kmualim.github.io/blob/master/images/gan_schema.png) <br>
Credit: O'Reilly <br>
1. The generator initially takes in random noise and returns an image/text
2. This generated image is passed to the discriminator with a collection of real images from the dataset
3. The discriminator then takes in the images and generates a probability to determine if the generated image is real (1) or fake (0) , generating a feedback loop. 

The generator in turn learns to create more believable data to fool the discriminator while the discriminator learns to better discriminate between the fake and real samples. 

[Joseph Rocca](https://towardsdatascience.com/understanding-generative-adversarial-networks-gans-cd6e4651a29) wrote an incredible blog post into understanding the step-by-step mechanics of GANs where he illustrates: 
- how the generator seeks to rephrase the problem of generating a new image of "dog" into the problem of generating a random vector in the N dimensional vector space that follows the "dog probability distribution"

## Deep Convolutional Generative Adversarial Network (DCGAN) 
[Code for DCGAN Implementation on MNIST](https://github.com/kmualim/DCGAN-Keras-Implementation)

A DCGAN focuses on deep convolutional networks in places of fully-connected networks but conceptually work the same as GANs.
<br> The general architecture of a DCGAN looks like this: 
![](https://github.com/kmualim/DCGAN-Keras-Implementation/blob/master/files/dcgan-image.png) </br> 
These convolutional nets find areas of correlation within images and looks for spatial correlations, enabling it to be more fitting for image/video data.
In addition, DCGANs also experience higher stability during training than GANs, giving you possibly an easier time at building a GAN. 


I built a DCGAN for the first time as an interest project and met with some challenges during training. While google serves as a wonderful resource for helping you solve problems associated to GANs, 
I wasn't able to find a comprehensive compilation of the respective solutions for some problems in building a GAN.Thus, this is my attempt at illustrating my entire journey & perhaps how I've overcame my obstacles might help you too! 

P.S If you're building a GAN and utilizing it on a more complex dataset, I would recommend trying it out on a simple MNIST dataset first before proceeding. This way, you'll know that your model works brilliantly. 

## Main Issues
The main issues I faced after building the model infrastructure was that:
  1. I noticed that my <b>discriminator loss</b> converges rapidly to zero thus preventing the generator from learning
  2. Adversarial loss decreases to 0 almost immediately after initiation
all possibly attributed to the instability of building a GAN/DCGAN. <br> 
![](https://github.com/kmualim/kmualim.github.io/blob/master/images/gan-initialrun.png)
  <i> Fig 1. Epoch v Loss </i> 

## Solutions
What I tried and what worked: <br>
  <b>1</b>. Try implementing weight initialization <br>
  <b>2</b>. Addition of noise to both input and fake images <br>
  <b>3</b>. Helped not to pre-train the discriminator <br>
  <b>4</b>. When training either discriminator/generator, hold the generator/discriminator values constant <br>
  5. Changed convolutional filter size to 3x3, was previously 5x5 (I've seen most places put this at 4) <br>
  6. Reduced depths of conv layers to a consistent value of 128 for the discriminator improved the model <br>
  7. added and lowered dropout values (should be ideally kept around 0.3-0.6)
  
In particular, <b>1, 2 and 3</b> are really popular solutions cited in most places. 

Generally, GANs are highly unstable and require proper design to prevent either sides of the GAN to overpower each other. When this happens, the discriminator might return values close 0 or 1 causing the generator to struggle to read the gradient. Hence, altering the <b> respective learning rates </b> could help in training. 

My model seemed to work fine after I adjusted the different points above. 
However, there are also additional things you could try that might help if you'e still having some issues. 

What you could additionally try: <br>
  8. Flipping the labels!<br>
  9. Don’t stop training early, <b>unless</b> discriminator loss approaches 0 fairly quickly <br>
    - I’ve learnt that GANs take an excruciatingly long time to train and too stopping the training early might be disadvantageous <br>

## Results
Final architecture that worked for 28x28 images, following [this paper](https://arxiv.org/pdf/1511.06434.pdf): <br>
** differently sized images may require different parameter changes 
<br>
Loss values were also consistently low: 
![](https://github.com/kmualim/kmualim.github.io/blob/master/images/final-run.png) <br>

The generated image obtained at epoch 0 was incredibly different from the generated image obtained at epoch 4000: <br>
![](https://github.com/kmualim/kmualim.github.io/blob/master/images/origin-img.png) <br> 
![](https://github.com/kmualim/kmualim.github.io/blob/master/images/final-img.png) <br>
<br>
However, the image resolution/the generation of images could still be vastly improved. The numbers are discernible but still blurry and could be more concise. Any tips and comments are welcomed and do reach out, perhaps even running the model for more epochs might make the images better. (People have noted that their implementations have often needed to run for more epochs than predicted.)

## Conclusions
Summary of architectural guidelines for stable Deep Convolutional GANs: 
• Replace any pooling layers with strided convolutions (discriminator) and fractional-strided
convolutions (generator).
• Use batchnorm in both the generator and the discriminator.
• Remove fully connected hidden layers for deeper architectures.
• Use ReLU activation in generator for all layers except for the output, which uses Tanh.
• Use LeakyReLU activation in the discriminator for all layers.

The [original paper](https://arxiv.org/pdf/1511.06434.pdf) also gives a really good explanation as to how they attained the respective guidelines, it serves as a very interesting read and I would definitely recommend! 

I am, of course, really oversimplifying what GANs are and I do recommend reading more material to find out more! <br> 
[An overview paper](https://arxiv.org/abs/1710.07035) <br> 
[GANs for the non-technical](https://www.analyticsvidhya.com/blog/2017/06/introductory-generative-adversarial-networks-gans/) <br> 
[Fantastic GANs and where to find them](http://guimperarnau.com/blog/2017/03/Fantastic-GANs-and-where-to-find-them) <br> 
[Keeping up with GANs](https://medium.com/nurture-ai/keeping-up-with-the-gans-66e89343b46) 

## References 
1. [Improved Techniques for Training GANs](https://arxiv.org/pdf/1606.03498.pdf)
2. [Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Network](https://arxiv.org/pdf/1511.06434.pdf)
3. [Awesome gan applications](https://github.com/nashory/gans-awesome-applications). 
4. [Gan Pitfalls and Solutions](https://medium.com/@utk.is.here/keep-calm-and-train-a-gan-pitfalls-and-tips-on-training-generative-adversarial-networks-edd529764aa)
5. [GAN](https://skymind.ai/wiki/generative-adversarial-network-gan) 
6. [GanHacks](https://github.com/soumith/ganhacks#13-add-noise-to-inputs-decay-over-time)
