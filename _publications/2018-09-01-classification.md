---
title: "A classification task to recognize simple hand drawn objects  "
excerpt: "Generate a classifier to identify hand-drawn images in 18 different categories"
collection: publications
date: 2018-09-01
location: "Montreal, Quebec"
---

[Code](https://github.com/kmualim/comp551_final/blob/master)  [Read more about it here](https://github.com/kmualim/comp551_final/blob/master/Kaggle_Report.pdf)

# Classification task

By using sklearn/tensorflow/pytorch libraries, we generated a classifier that could classify hand-drawn images from Google's *Quick, Draw!* project. 
The dataseet contained images that were not always centerred and straight, or free of noisy artifacts. In addition, the classifierrr needed to identify 
empty pictures as well. 

## Image Preprocessing 

<br><img src='/images/original.png'><br>
Original Image 

<br><img src='/images/o-processed.png'><br>
Preprocessed Image

Our implementation of classifier built on a deep learning framework improved accuracy by 11% above a baseline CNN classifier. 
We utilized several algorithms, such as CNNs and played around with utilizing pre-trained models such as Google Inception V3. 


