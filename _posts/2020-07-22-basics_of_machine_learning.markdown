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

<p> In loose terms, ML can help with <i>classification</i>, <i>clustering</i>, and <i>regression</i> for the data to come up with meaningful patterns. </p>


<figure>
<p align="left">
  <img src="/assets/img/basicML.jpg" width="500" alt="" title="">
  <figcaption> <b>Figure 1.</b> Generic ML Applications </figcaption>
</p>
</figure>
<br>

<h2> Uploading Data </h2>

<p> The datasets required for this tutorial contain 9 features/ variables from profiling of breast cells which include the thickness of clump, cell-size, cell-shape, etc. In addition to these features, the training dataset contains one more column as <b>target</b>, or a class. It has a binary value (0 or 1) for each row. 0 indicates no breast cancer and 1 indicates breast cancer. The test dataset does not contain the target column. </p>

<p> The data we'll be using is listed below. Again, we can choose to upload the data via web-links (below) as mentioned in a previous tutorial.</p>


<ol>
<li> <i> https://zenodo.org/record/1401230/files/breast-w_train.tsv </i> </li>
<li> <i> https://zenodo.org/record/1401230/files/breast-w_test.tsv </i> </li>
</ol>

<br>
<p align="center">
  <img width="200" height="250" src="/assets/img/renameMLData.png">
</p>
<br>

<p> Rename the data for easy working. </p>


<br>
<p align="center">
  <img width="200" height="200" src="/assets/img/renamedMLData.png">
</p>
<br>

<p> Again, if we want to view data, we can click on the "eye" icon next to the file name. The initial data points in the <i>train</i> data look as below. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/dataML.png">
</p>
<br>


<h2> Setting up the Classifier </h2>

<p> Since we are interested in a classification problem, we shall be structuring a ML model or classifier that better represents the patterns in the data and encompasses it's inherent features. The efficiency of the classifier is solely derived from the data it is trained upon and hence it is on the utmost importance to provide <i> clean and comprehensive data </i> to bring out the best. </p>

<p> There are manu flavors of classifiers available out there, but for this exercise, we shall be using the <b> Support Vector Machines (SVMs) </b> to accomplish the task at hand. We will employ the <a href = "https://scikit-learn.org/stable/" > <i>scikit-learn</i> </a> library in python; search for <i><b>sklearn_svm_classifier</b></i> in the repository and install the tool. Particularly, we shall be using the <b>Linear Support Vector Classifier (Linear SVC)</b> because of it's effiency over other options. </p>

<h3> Support Vector Machines (SVMs) </h3>

<p> <a href = "https://scikit-learn.org/stable/modules/svm.html#" > <b>SVMs</b> </a> have supported classification tasks quite formidably and essentially need no introduction to the field. The following graphics depict the fundamental idea. Also, various texts are available in print and online that can be accessed for the same. </p>


<figure>
<p align="left">
  <img src="/assets/img/svmCore1.jpg" width="500" alt="" title="">
  <figcaption> <b>Figure 2.</b> Class seperating hyperplanes in SVM </figcaption>
</p>
</figure>
<br>

<figure>
<p align="left">
  <img src="/assets/img/svmCore2.jpg" width="500" alt="" title="">
  <figcaption> <b>Text Graphic 1.</b> SVM: Under the hood </figcaption>
</p>
</figure>
<br>

<p> Once installed, we can trace the following screenshots. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/svmInstalled1.png">
</p>
<br>

<br>
<p align="center">
  <img width="500" src="/assets/img/svmInstalled2.png">
</p>
<br>


<p> Next, we can proceed with the execution with the following input parameters.
<ul>
<li> <i>“Select a Classification Task”</i>: Train a model </li>
<li> <i>“Classifier type”</i>: Linear Support Vector Classification</li>
<li> <i>“Select input type”</i>: tabular data</li>
<li> <i>“Training samples dataset”</i>: breast-w_train</li>
<li> <i>“Does the dataset contain header” </i>: Yes</li>
<li> <i>“Choose how to select data by column” </i>: All columns EXCLUDING some by column header name(s)</li>
<li> <i>“Type header name(s)” </i>: target</li>
<li> <i>“Dataset containing class labels or target values” </i>: breast-w_train</li>
<li> <i>“Does the dataset contain header” </i>: Yes</li>
<li> <i>“Choose how to select data by column” </i>: Select columns by column header name(s)</li>
<li> <i>“Type header name(s):” </i>: target</li>
</ul>
</p>

<p> The output of the above execution is a <i> zip archive </i> that shall subsequently be used for making predictions on the test data. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/svmOut.png">
</p>
<br>

<h2> Making Predicitions </h2>

Make choices for parameters as follows.

<br>
<p align="center">
  <img width="500" src="/assets/img/svmPredictParameters.png">
</p>
<br>

The output is a data table with the last column as the predicted class labels.

<br>
<p align="center">
  <img width="500" src="/assets/img/svmPredictions.png">
</p>
<br>


<span style="color:#800080">
<p><b>Exercise</b></p>
<ol>
<li> Run SVM with C- and Nu- Support Vector Classification profiles for training data and examine the results. </li>
</ol>
</span>


<h2> References </h2>

<ol>
<li> Anup Kumar, 2020 Basics of machine learning (Galaxy Training Materials). /training-material/topics/statistics/tutorials/machinelearning/tutorial.html Online; accessed Sun Jul 26 2020  </li>
</ol>