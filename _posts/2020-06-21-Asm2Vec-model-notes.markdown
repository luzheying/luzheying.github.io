---
layout: post
title: "Asm2Vec: Binary Clone Search"
author: Zheying Lu
categories: research
tags: [research, crypto, english]
image: asm2vec-1.jpg
---
Asm2Vec is an assembly code representation learning model also an assembly clone search approach. In this blog, I am going to share the notes i took when reading the paper. 

Here is the [Asm2Vec paper](https://www.computer.org/csdl/proceedings-article/sp/2019/666000a038/19skfc3ZfKo "Asm2Vec: Boosting Static Representation Robustness for Binary Clone Search against Code Obfuscation and Compiler Optimization"). 

## Problems with existing approaches and Solutions:

**Problem1 :**
Failed to consider the relationships among features. They assumed each feature or category is an independent dimension.
Proposed solution: incorporate lexical semantic relationship by learning these relationships directly from plain assembly code. (eh. memcpy, strcpy, memncpy)

**Problem2 :**
Assume that features are equally important or assign the features with unideal weights.
Proposed solution: train a neural network model to read many assembly code data and let the model identify the best representation that distinguishes one function from the rest.

## Overall Workflow
<img src="{{ site.github.url }}/assets/img/posts/Screen_Shot_2020-06-04_at_11.16.34_AM.png">
**Steps**
1. **Training**: build NN model
2. **Produce**: produce a vector representation for each RP
3. **Estimate**: given ft(target function), use the model in 1 to estimate vector rep
4. **Compare**: compare the vector of ft against the other vectors in the RP

## The Asm2Vec Model (Step1+2)
<img src="{{ site.github.url }}/assets/img/posts/Screen_Shot_2020-06-04_at_11.28.19_AM.png">

* How to treat each RP 

fs → multiple sequences → list of instructions → contain a list of operands and one operation

* How to model assembly function into multiple sequences

Selective Callee Expansion: Using function inlining to expand callee 
Edge coverage. sample all edges
Random Walk → generated sequence is much longer than the edge sampling

* How to deal with RP function

Map each EP fun fs to vector with size of R2xd
size is 2xd because vector is consist of the operation and operands. 
Intuition is to use the current function's vector and the context provided by the neighbor instructors tp predict the current instruction.

- **Math behind it**

treat operands and operations in assembly code as token. Map each token t into a numeric vector vt with size Rd and another vt' with size R2xd. 

vt - visualize the relationship / vt' - token prediction