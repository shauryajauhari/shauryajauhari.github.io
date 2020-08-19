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

<ol>
<li><i> https://zenodo.org/record/3738729/files/train_rows.csv </i></li>
<li><i> https://zenodo.org/record/3738729/files/test_rows_labels.csv </i></li>
<li><i> https://zenodo.org/record/3738729/files/test_rows.csv  </i></li>
</ol>

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
<figcaption><b>Figure 3: Confusion Matrix</b> <i> It is a table of 2 rows and 2 columns, summarizing the classification results with respect to the test data, in terms of True Positives, True Negatives, False Positives, and False Negatives. P.S. The comparison is between actual and predicted values; one could either, but not both.</i> </figcaption>
</p>
</figure>
<br>


<h2> K-Nearest Neighbor (KNN) Classifier </h2>

<p align="justify"> In this classification scheme, <b>a data sample is assigned to the class that is most common to its neighbors</b>, the variable <i>k</i> defines the number of nearest neighbors to look out for. This value is critical and while a small <i>k</i> could induce a lot of noise, a larger <i>k</i> might well contain points from other classes and engender erroneous classification. A prefered way is to run the classifier with varying <i>k</i> and then choose the model with optimum error. </p>

<p align="justify">To run this algorithm in Galaxy, we'll install the tool <b>Nearest Neighbors Classification</b> from the repository <i><b>sklearn_nn_classifier</b></i>. As you would find out, the classifier was trained with <i>k = 5</i>, which is the default value.</p> 

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/nearestNeighborClassifierOptions.png">
</p>
</figure>
<br>

<p align="justify"> With the model in place now, let us use it for the test data and gauge it's potency. </p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/nearestNeighborTest.png">
</p>
</figure>
<br>

<h3> Visualizing Results </h3>


<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/plotNearestNeighborOptions.png">
</p>
</figure>
<br>

Subsequently.


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/precisionRecallFNearestNeighbor.png">
<figcaption><b>Figure 1: Precision, recall and F1 score</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/rocAUCNearestNeighbor.png">
<figcaption><b>Figure 2: Receiver Operator Characteristics (ROC) and Area Under ROC (AUC)</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/confusionMatrixNearestNeighbor.png">
<figcaption><b>Figure 3: Confusion Matrix</b></figcaption>
</p>
</figure>
<br>

<p align="justify"> As you would note, the accuracy of this classifier (AUC = 0.95) is tad better than the logistic regression model (AUC = 0.94).</p>



<h2> Support Vector Machines (SVMs) </h2>

<p align="justify"> A primer for this classification scheme is available <a href = "https://shauryajauhari.github.io/basics_of_machine_learning/" > here </a>. Let us dive right into the application.</p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/svmOptions.png">
</p>
</figure>
<br>

<p align="justify"> The SVM model learns the coefficients of the hyperplane with the maximal margin in the kernel space, between classes. Let us apply the model on test data and then visualize the results.</p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/svmTest.png">
</p>
</figure>
<br>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/svmResults.png">
</p>
</figure>
<br>

Again,


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/precisionRecallFSVM.png">
<figcaption><b>Figure 1: Precision, recall and F1 score</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/rocAUCSVM.png">
<figcaption><b>Figure 2: Receiver Operator Characteristics (ROC) and Area Under ROC (AUC)</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/confusionMatrixSVM.png">
<figcaption><b>Figure 3: Confusion Matrix</b></figcaption>
</p>
</figure>
<br>


<h2> Random Forest </h2>

<p align="justify"> An ensemble of decision trees, this classifier improvises the overall results by aggregating results from a multitude of learning models. It is a "boosting and bagging" methodology that iteratively minimizes error. See this <a href = "https://rpubs.com/shauryajauhari/decision_trees_random_forests" > presentation </a> for reference. The problem of <i>overfitting</i> is least likely in an ensemble method as it generalizes well, being trained on several instances of the data. </p>


<h3> Building Model </h3>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/randomForestOptions.png">
</p>
</figure>
<br>


<h3> Application on Test Data </h3>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/randomForestTest.png">
</p>
</figure>
<br>


<h3> Visualizing Results </h3>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/randomForestResults.png">
</p>
</figure>
<br>

Finally, 

<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/precisionRecallFRandomForest.png">
<figcaption><b>Figure 1: Precision, recall and F1 score</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/rocAUCRandomForest.png">
<figcaption><b>Figure 2: Receiver Operator Characteristics (ROC) and Area Under ROC (AUC)</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/confusionMatrixRandomForest.png">
<figcaption><b>Figure 3: Confusion Matrix</b></figcaption>
</p>
</figure>
<br>


The results are perfect. The AUC = 1.0 indicates absolutely no error. 


<h2> Creating a Data Processing Pipeline | Ensemble Classifier </h2>

<h3> Pipeline Builder </h3>

<p align="justify"> We need a list of hyperparameters of the estimators. This is the output of pipeline builder that shall eventually be fed to the <i>Hyperparameter search</i> tool. However, we shall particularly focus on the constraint, <i>n_estimators</i>, as this defines the number of stages for the "bagging" operation. As we know, "bagging" allows for aggregation of results for a concensus. In addition, it must be examined that this value is neither too high (as we'll be making unnecessary expenditure on processing and time), neither too low (so that the accuracy is hampered). The <i>Hyperparameter search</i> tool gives us just the optimal number we need. <i>(<b>Note:</b> The default value of n_estimators for this regressor is 10)</i></p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/pipelineBuilderEnsembleOptions.png">
</p>
</figure>
<br>

<h3> Hyperparameter Search </h3>

Try the following choices.

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/hyperparameterSearchOptions1.png">
</p>
</figure>
<br>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/hyperparameterSearchOptions2.png">
</p>
</figure>
<br>

<p align="justify"> This run results in two files; the model (zip file) and the hyperparameter values (tabular file). Have a look at the tabular file. </p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/hyperparameterSearchResult.png">
</p>
</figure>
<br>

<p align="justify"> The column <i>mean_test_score</i> gives the accuracy for the model, corresponding to the given parameter value. So, although the default value is 10, yet 50 gives us a better model. That is exactly why it is important to tune the model in accord to these parameters to give us the optima. Agin, we'll make the prediction with the new model. </p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/hyperparameterSearchModelRun.png">
</p>
</figure>
<br>

<h3> Visualization of Results </h3>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/hyperparameterSearchResultsPlot.png">
</p>
</figure>
<br>

Pulling the plots,

<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/precisionRecallFHyperparameterSearch.png">
<figcaption><b>Figure 1: Precision, recall and F1 score</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/rocAUCHyperparameterSearch.png">
<figcaption><b>Figure 2: Receiver Operator Characteristics (ROC) and Area Under ROC (AUC)</b></figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/confusionMatrixHyperparameterSearch.png">
<figcaption><b>Figure 3: Confusion Matrix</b></figcaption>
</p>
</figure>
<br>


<p align="justify"> So, we can see that the ensemble methods have a high quality prediction on deciphering whether or not a chemical substance is biodegradable. Surely, the mix of flavors in data brings about all the magic and the classifier is able to perform noticeably better than the isolate models.</p>



<h2> References </h2>
<ol>
<li>Alireza Khanteymoori, Anup Kumar, Simon Bray, 2020 Classification in Machine Learning (Galaxy Training Materials). /training-material/topics/statistics/tutorials/classification_machinelearning/tutorial.html Online; accessed Thu Aug 06 2020</li>
<li>Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012</li>
</ol>