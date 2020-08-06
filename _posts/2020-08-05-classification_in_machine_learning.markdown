---
layout: post
title: Classification in Machine Learning
date: 2020-08-05 14:17:52 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: garbageClassification.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Machine Learning, Data Science]
---

<h2> Introduction </h2>

<p align="justify"> In this tutorial, we shall learn to deal with classification problems using Galaxy. We shall examine <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/transcriptionFactoriesGREG/blob/master/MachineLearning/LogisticRegressionA549GREG.ipynb" > <b>Logistic Regression</b> </a> (a linear classifier), the <b>Nearest Neighbor</b> (a nonlinear classifier), <a href = "https://shauryajauhari.github.io/basics_of_machine_learning/" > <b>Support Vector Machines</b> </a>, <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/transcriptionFactoriesGREG/blob/master/MachineLearning/RandomForestsA549GREG.ipynb" > <b>Random Forest</b> </a> and other ensemble classifiers, with data visualization for each application. We will also explore ways to minimize the cost function.</p>

<h3> Supervised Learning </h3>

<p align="justify"> Classification is a supervised learning method in machine learning and the algorithm which is used for this learning task is called a <i>classifier</i>. The idea is to map data instances to certain pre-defined class labels, and this is carried out by perusing nuances from the attributes of the input data. My best intuition that fits the theme and is often reciprocated on the adverts in the public domain, is that of <a href = "https://news.cgtn.com/news/2019-08-12/Why-China-has-started-to-classify-its-garbage-J6aPiHBA6Q/index.html" > <b>Garbage Classification</b> </a>; a simple notion that has a tremendous impact in the recycling of waste products. So depending on the physical and chemical properties of a junk, it is dispensed in the appropriate (color-coded) bin.</p> 

<p align="justify"> To explore this theme, we will perform a case study on cheminformatics data, arguing if a chemical substance is biodegradable; a purposeful examination that aligns to the environmental safety aspects. A <a href = "https://pubs.acs.org/doi/10.1021/ci4000213" > database </a> (Mansouri et al.) of compounds is collected for which the property of interest is known. For each compound, molecular descriptors are collected which describe the structure (for example: molecular weight, number of nitrogen atoms, number of carbon-carbon double bonds). Using these descriptors, a model is constructed which is capable of predicting the property of interest for a new, unknown molecule. This database contains 1055 molecules, together with precalculated molecular descriptors. </p>


<h2> Data Sourcing </h2>

<p align="justify"> We have the data pre-clustered into training and testing sets and could be downloaded into the Galaxy instance via the following links: </p>

<ul>
<li><i> https://zenodo.org/record/3738729/files/train_rows.csv </i></li>
<li><i> https://zenodo.org/record/3738729/files/test_rows_labels.csv </i></li>
<li><i> https://zenodo.org/record/3738729/files/test_rows.csv  </i></li>
</ul>

As usual, we rename the datasets for our convenience. Now that we have the data, we will get into the core of our analysis. Let us begin by applying the logistic regression classifier to model the data.


<h2> Logistic Regression Classifier </h2>

<p align="justify"> The <a href = "https://www.sciencedirect.com/topics/computer-science/logistic-function" > <b>logistic function</b> </a> aims to calculate the weight(coefficient/ slope) and bias(error/ intercept) for the line that will fit the data in question, and innately, project the predicted class labels over the true class labels. The dissimilarity or the distance between these respective labels is the <i>loss/ cost function</i>. The second thing we need is an optimization algorithm for iteratively updating the weights so as to minimize this loss function. The standard algorithm for this is <b>gradient descent</b>. </p>


<p align="justify"> We will use the tool <b>Generalized linear models</b> from the repository <b><i>sklearn_generalized_linear</i></b>, and make the following choices for paramaters. </p>

<ul>
<li><i>“Select a Classification Task”</i>:<b> Train a model</b></li>
<li><i>“Select a linear method”</i>:<b> Logistic Regression</b></li>
<li><i>“Select input type”</i>:<b> tabular data</b></li>
<li><i>“Training samples dataset”</i>:<b> train_rows</b></li>
<li><i>“Does the dataset contain header”</i>:<b> Yes</b></li>
<li><i>“Choose how to select data by column”</i>:<b> All columns EXCLUDING some by column header name(s)</b></li>
<li><i>“Type header name(s)”</i>:<b> Class</b></li>
<li><i>“Dataset containing class labels”</i>:<b> train_rows</b></li>
<li><i>“Does the dataset contain header”</i>:<b> Yes</b></li>
<li><i>“Choose how to select data by column”</i>:<b> Select columns by column header name(s)</b></li>
<li><i>“Select target column(s)”</i>:<b> Class</b></li>
</ul>


<p align="justify"> We rename the generated file to <b>LogisticRegression_model</b> and proceed towards making predictions by applying the model on test data. That will lead us to determine the accuracy of the model. </p>


<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/logisticRegressionTest.png">
</p>
</figure>
<br>

<p align="justify"> <i><b>Note:</b> The training data has features as well as the corresponding class-labels. Although, the test data we use for making predictions is without class-labels (just values for features). Additionally, the data we employ for testing model accuracy is just the class-labels for test data.</i> </p>

<p align="justify"> We rename the results of the logistic regression model to <i>LogisticRegression_result</i>, and remove the header from the <i>test_rows_labels</i> file. </p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/repeatedHeader.png">
</p>
</figure>
<br>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/removeFirstLine.png">
</p>
</figure>
<br>

Let us view the results.

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/plotLogisticRegressionResults.png">
</p>
</figure>
<br>

<p align="justify"> The visualization tool created three plots for, viz. <a href = "https://en.wikipedia.org/wiki/Confusion_matrix" > <b>Confusion Matrix</b></a>, <a href = "https://en.wikipedia.org/wiki/Precision_and_recall" > <b>Precision, recall and F1 score</b> </a>, and <a href = "https://towardsdatascience.com/understanding-auc-roc-curve-68b2303cc9c5" > <b>Receiver Operator Characteristics (ROC) and Area Under ROC (AUC)</b> </a>, as depicted below.


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/precisionRecallF.png">
<figcaption><b>Figure 1: Precision, recall and F1 score</b> <i> These scores determine the accuracy of classification and any conceivable biaseness towards any class in particular.</i> </figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/rocAUC.png">
<figcaption><b>Figure 2: Receiver Operator Characteristics (ROC) and Area Under ROC (AUC)</b> <i> This metric is a crossover between sensitivity and specificity, and broadly estimates the model accuracy of prediciting class labels for positive and negative classes.</i> </figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/confusionMatrixClassification.png">
<figcaption><b>Figure 3: Confusion Matrix</b> <i> It is a table of 2 rows and 2 columns, summarizing the classification results with respect to the test data, in terms of True Positives, True Negatives, False Positives, and False Negatives.</i> </figcaption>
</p>
</figure>
<br>



<h2> References </h2>
<ol>
<li>Alireza Khanteymoori, Anup Kumar, Simon Bray, 2020 Classification in Machine Learning (Galaxy Training Materials). /training-material/topics/statistics/tutorials/classification_machinelearning/tutorial.html Online; accessed Thu Aug 06 2020</li>
<li>Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012</li>
</ol>