---
layout: post
title: Basics of Machine Learning
date: 2020-07-22 15:43:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Mathematics, Statistics, Data Science]
---

<h2> Preface </h2>

<p> We've extensively discussed the theory behind several Machine Learning (ML) algorithms, namely <a href = "https://github.com/shauryajauhari/Machine_Learning/blob/master/Machine_Learning_Logistic_Regression/Logistic_Regression_Lab/glmnet_stats_glm_ep.pdf" > Logistic Regression </a>, <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/Machine_Learning/blob/master/Machine_Learning_Random_Forests/hands_on_random_forests_ep.ipynb" > Random Forests </a>, and <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/Machine_Learning/blob/master/Machine_Learning_Deep_Learning/hands_on_deep_learning_ep.ipynb" > Deep Learning </a>. These also encompass a practical application on the enhancer-prediction exercise (See <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/Machine_Learning/blob/master/Machine_Learning_Deep_Learning/enhancer_prediction_dataset_protocol.ipynb" > this </a>). I am not going to delve into that back again. Rather, in this session, let us figure out the ways to implement ML algorithms in Galaxy, from setting it up to inferring results. Let's cut to the chase. This tutorial has been sourced from this <a href = "https://galaxyproject.github.io/training-material/topics/statistics/tutorials/machinelearning/tutorial.html" > link </a>. </p>

<h2> Uploading Data </h2>

<p> The datasets required for this tutorial contain 9 features/ variables of breast cells which include the thickness of clump, cell-size, cell-shape, etc. In addition to these features, the training dataset contains one more column as <b>target</b>, or a class. It has a binary value (0 or 1) for each row. 0 indicates no breast cancer and 1 indicates breast cancer. The test dataset does not contain the target column. </p>

