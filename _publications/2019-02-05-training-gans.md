# What is a GAN? 
A Generative Adversarial Network takes the idea of using a generator model to generate fake examples and 
discriminator model that decides if image it receives is a fake. A classic analogy for a GAN takes the case of the police (discriminator) and the counterfeiter (generator). 
I am, of course, really oversimplifying what GANs are and I do recommend reading more material to find out more! <br> 
[An overview paper](https://arxiv.org/abs/1710.07035) <br> 
[GANs for the non-technical](https://www.analyticsvidhya.com/blog/2017/06/introductory-generative-adversarial-networks-gans/) <br> 
[Fantastic GANs and where to find them](http://guimperarnau.com/blog/2017/03/Fantastic-GANs-and-where-to-find-them) <br> 
[Keeping up with GANs](https://medium.com/nurture-ai/keeping-up-with-the-gans-66e89343b46) 

## Deep Convolutional Generative Adversarial Network (DCGAN) 
A DCGAN focuses on deep convolutional networks in places of fully-connected networks. 
These convolutional nets find areas of correlation within images and looks for spatial correlations, enabling it to be more fitting for image/video data.
In addition, DCGANs also experience higher stability during training than GANs, giving you possibly an easier time at building a GAN. 
These convolutional nets find areas of correlation within images and looks for spatial correlations, enabling it to be more fitting for image/video data.

I built a DCGAN for the first time as an interest project and met with some challenges during training. Google is a wonderful resource for helping you solve problems associated to GANs, but
I didn't find a comprehensive compilation of the respective solutions for some problems in building a GAN.
If you're building a GAN and utilizing it on a more complex dataset, I would recommend trying it out on a simple MNIST dataset first before proceeding. 
This way, you'll know that your model works brilliantly. 
Thus, this is my attempt at illustrating my entire journey & perhaps how I've overcame my obstacles might help you too! 

The general architecture of a DCGAN looks like this: 
![](https://github.com/kmualim/DCGAN-Keras-Implementation/blob/master/files/dcgan-image.png)

The main issues I faced after building the model infrastructure was that:
  1. Initial runs causes model to converge very quickly to loss = 0 
  2. I noticed that my <b>discriminator loss<br> converges rapidly to zero thus preventing the generator from learning
  3. Adversarial loss decreases to 0 almost immediately after initiation
all possibly attributed to the instability of building a GAN/DCGAN. 
![](https://github.com/kmualim/kmualim.github.io/tree/master/images/gan-initialrun.png)
  <i> Fig 1. Epoch v Loss </i> 
 
What I tried and what worked: 
  1. Addition of noise to both input and fake images 
  2. Helped not to pre-train the discriminator 
  3. Tried changing convolutional layers located in the generator 
  4. Changed convolutional filter size to 3x3, was previously 5x5 (I've seen most places put this at 4) 
  5. Reduced depths of conv layers to a consistent value of 128 in v2.0 for the discriminator slowed the convergence
  6. lowered dropout values (should be ideally kept around 0.3-0.6)
  
In particular, 1 & 2 are really popular solutions cited in most places. 
My model seemed to work fine after I adjusted the different points above. 
However, there are also additional things you could try that might help if you'e still having some issues. 

What you could additionally try:
  7. Flipping the labels!
  8. Try weight initialization 
  9. Don’t stop training early, <b>unless</b> discriminator loss approaches 0 fairly quickly 
    - I’ve learnt that GANs take an excruciatingly long time to train and too stopping the training early might be disadvantageous 

Final architecture that worked for 28x28 images, following ![2](https://arxiv.org/pdf/1511.06434.pdf)
** differently sized images may require different parameter changes 
Loss values were also consistently low: 
![](https://github.com/kmualim/kmualim.github.io/tree/master/images/final-run.png) <br>

The generated image obtained at epoch 0 was incredibly different from the generated image obtained at epoch 4000: <br>
![](https://github.com/kmualim/kmualim.github.io/tree/master/images/origin-img.png) <br> 
![](https://github.com/kmualim/kmualim.github.io/tree/master/images/final-img.png) <br>

However, the image resolution/the generation of images could still be vastly improved. The numbers are discernible but still blurry and could be more concise. Any tips and comments are welcomed and do reach out, perhaps even running the model for more epochs might make the images better. (People have noted that their implementations have often needed to run for more epochs than predicted.)

Summary of architectural guidelines for stable Deep Convolutional GANs, as illustrated in [2]: 
• Replace any pooling layers with strided convolutions (discriminator) and fractional-strided
convolutions (generator).
• Use batchnorm in both the generator and the discriminator.
• Remove fully connected hidden layers for deeper architectures.
• Use ReLU activation in generator for all layers except for the output, which uses Tanh.
• Use LeakyReLU activation in the discriminator for all layers.

The [paper](https://arxiv.org/pdf/1511.06434.pdf) also gives a really good explanation as to how they attained the respective guidelines, it serves 
as a very interesting read and i would definitely recommend! 

References: 
1. [Improved Techniques for Training GANs](https://arxiv.org/pdf/1606.03498.pdf)
2. [Unsupervised Representation Learning with Deep Convolutional Generative Adversarial Network](https://arxiv.org/pdf/1511.06434.pdf
3. [Awesome gan applications](https://github.com/nashory/gans-awesome-applications). 
4. [Gan Pitfalls and Solutions](https://medium.com/@utk.is.here/keep-calm-and-train-a-gan-pitfalls-and-tips-on-training-generative-adversarial-networks-edd529764aa)
5. [GAN](https://skymind.ai/wiki/generative-adversarial-network-gan) 
6. https://github.com/soumith/ganhacks#13-add-noise-to-inputs-decay-over-time 
