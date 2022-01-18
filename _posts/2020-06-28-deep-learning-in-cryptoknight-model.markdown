---
layout: post
title: "Deep Learning in CryptoKnight Model"
author: Zheying Lu
categories: research
tags: [research, deep learning, english]
image: deep-learning-1.jpg
---
CryptoKnight is a learning system that can easily incorporate new samples through the scalable synthesis of customisable cryptographic algorithms. The model is inspired by NLP (Natural Language Processing) approaches. 

Nowadays, more and more deep learning techiniques are utilized in NLP problems, also in cryptographic field. In this blog, I will include the basic introduction to CNN (convolutional nueral network) and DCNN (Dynamic convolutional nueral network) which is implemented in CryptoKnight model. Here is the [CryptoKnight model](https://www.mdpi.com/2078-2489/9/9/231)

# CNN

<img src="{{ site.github.url }}/assets/img/posts/Untitled.png">

CNN is composed of different types of layers which extracts features of the input image.

convolutional layer/pooling layer/fully connected layer/classifier. (except for the classifier, what the other layers do is to extract features) 

**Convolutional layers** 

    Convolutional layers are the layers where *filters* are applied to the original image, or to other feature maps in a deep CNN. This is where most of the user-specified parameters are in the network.

*Filter:*
<img src="{{ site.github.url }}/assets/img/posts/Untitled (1).png">(example of kernel filters in CNN's)

**Pooling layers** 

    Pooling layers are similar to convolutional layers, but they perform a specific function such as max pooling, which takes the maximum value in a certain filter region, or average pooling, which takes the average value in a filter region. These are typically used to reduce the dimensionality of the network.

<img src="{{ site.github.url }}/assets/img/posts/Untitled (2).png">(example of how pooling layer work)

[How are weights represented in a convolution neural network?](https://datascience.stackexchange.com/questions/18341/how-are-weights-represented-in-a-convolution-neural-network) (explanation for weight in CNN)

**Fully connected layers** 

    Fully connected layers are placed before the classification output of a CNN and are used to flatten the results before classification.

**Classifier** 

    Classifier will assign a probability for the object on the image being what the algorithm predicts it is.

**_Helpful websites that help understanding CNN:_**

**[3D Visualization of a Convolutional Neural Network](https://www.cs.ryerson.ca/~aharley/vis/conv/)** 
(Note that the layers in the visualization goes from bottom to the top.)

[Deep Learning and DCNN](http://primo.ai/index.php?title=Deep_Learning)

[Understanding Convolutional Neural Networks for NLP](http://wildml.com/2015/11/understanding-convolutional-neural-networks-for-nlp/)




# DCNN

Relate work: A Convolutional Neural Network for Modeling Sentences

[A Convolutional Neural Network for Modelling Sentences](https://arxiv.org/abs/1404.2188)

The layers in the DCNN interleave one-dimensional convolutional layers and dynamic k-max pooling layers.

**_one-dimensional convolutional layer_**

    The one-dimensional convolution is an operation between a vector of *weights* *m* ∈ Rm and a vector of inputs viewed as a sequence *s* ∈ Rs

    *m* is the *filter* (explained in the CNN section)

    *s* is the input sentence and si ∈ R is a single feature value associated with the i-th word in the sentence

    In this layer, wide convolution is applied. A wide convolution ensures that all weights in the filter reach the entire sentence, including the words at the margins.


**_k-max pooling layer_**

    pooling layer(explained in CNN)

    the pooling factor by which the signal of the matrix is reduced at once corresponds to s − m + 1

    dynamic k-max pooling operation is a k-max pooling operation where we let k be a function of the length of the sentence and the depth of the net- work.

<img src="{{ site.github.url }}/assets/img/posts/4.png">

# Implementation of DCNN in CryptoKnight Model

For each word, embeddings are defined as d, where di corresponds to the total weight of a particular operation, multiplied by its entropic score. Feature vector wi ∈ Wd is a therefore a column in sentence matrix s such that s ∈ Wd×s.

<img src="{{ site.github.url }}/assets/img/posts/5.png">