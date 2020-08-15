---
layout: post
title: Introduction to Deep Learning
date: 2020-07-26 14:15:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: myNeuralNetGraphic.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Deep Learning, Statistics, Data Science]
---

<h2> Introduction </h2>
<p align="justify"> Deep Learning convolves state-of-the-art ML theme. Kindly visit this <a href = "https://rpubs.com/shauryajauhari/deep_learning" > link </a> for my brief presentation from the previous workshop and an <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/MachineLearning/blob/master/Machine_Learning_Deep_Learning/hands_on_deep_learning_ep.ipynb" > example workflow in R </a>.</p>

<p align="justify"> Assuming a fair understanding for the subject, let's dive right into a data analysis workflow in Galaxy. This exercise is again derived from the official training available <a href = "https://galaxyproject.github.io/training-material/topics/statistics/tutorials/intro_deep_learning/tutorial.html" > here </a>. </p>


<p align="justify"> Install the repositories- <i> keras_model_config </i>, <i> sklearn_train_test_eval </i>,  <i> model_prediction </i>, <i> ml_visualization_ex </i>, and <i> keras_model_builder </i> from the Tool Shed. </p>


<h2> Loading Data </h2>

<p align="justify"> The datasets used for this tutorial contain gene expression profiles of humans suffering from two types of cancer - acute myeloid leukemia (AML) and acute lymphoblastic leukemia (ALL). The tutorial aims to differentiate between these two cancer types, predicting a cancer type for each patient, by learning unique patterns in gene expression profiles of patients. The data is divided into 2 parts - one for training and another for prediction. Each part contains two datasets - one has the gene expression profiles and another has labels (the types of cancer). The size of the training data (X_train) is (38, 7129) where 38 is the number of patients and 7129 is the number of genes. The label dataset (y_train) is of size (38, 1) and contains the information of the type of cancer for each patient (label encoding is 0 for ALL and 1 for AML). The test dataset (X_test) is of size (34, 7129) and contains the same genes for 34 different patients. The label dataset for test is y_test and is of size (34, 1). The neural network, which will be formulated in the remaining part of the tutorial, learns on the training data and its labels to create a trained model. The prediction ability of this model is evaluated on the test data (which is unseen during training to get an unbiased estimate of prediction ability). </p>

<p align="justify"> Let us commence by loading data into a new session. The following could be renamed as <i>X_test</i>, <i>X_train</i>, <i>y_test</i>, and <i>y_train</i> respectively.</p>

<ol>
<li> <b> X_test </b><i> https://zenodo.org/record/3706539/files/X_test.tsv </i> </li>
<li> <b> X_train </b><i> https://zenodo.org/record/3706539/files/X_train.tsv </i> </li>
<li> <b> y_test </b><i> https://zenodo.org/record/3706539/files/y_test.tsv </i> </li>
<li> <b> y_train </b><i> https://zenodo.org/record/3706539/files/y_train.tsv </i> </li>
</ol>

<br>
<p align="center">
  <img width="500" src="/assets/img/kerasRun.png">
</p>
<br>

<h2> Model Structuring </h2>

<p align="justify"> The data in place, we may proceed towards building the model architecture with the following paramaters. </p>

    “Select keras model type”: Sequential
    “input_shape”: (7129, )
    In “LAYER”:
        param-repeat “1: LAYER”:
            “Choose the type of layer”: Core -- Dense
                “units”: 16
                “Activation function”: elu
        param-repeat “2: LAYER”:
            “Choose the type of layer”: Core -- Dense
                “units”: 16
                “Activation function”: elu
        param-repeat “3: LAYER”:
            “Choose the type of layer”: Core -- Dense
                “units”: 1
                “Activation function”: sigmoid

<p align="justify"> The tool returns a JSON output file with the attributes about the neural networks. The same can be viewed by clicking the "eye" icon. This output goes to the next stage of consolidating the deep learning model with additional parameters as optimiser, loss function, and the number of epochs and batch size (training attributes). The loss function is chosen as <b>binary_crossentropy</b> as the learning task is classification of binary labels (0 and 1). </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/kerasNext.png">
</p>
<br>

For the next stage, we specify the following constraints.


    “Choose a building mode”: Build a training model
    “Select the dataset containing model configurations (JSON)”: Keras model config (output of Create a deep learning model architecture using Keras tool)
    “Do classification or regression?”: KerasGClassifier
    In “Compile Parameters”:
        “Select a loss function”: binary_crossentropy
        “Select an optimizer”: RMSprop - RMSProp optimizer
    In “Fit Parameters”:
        “epochs”: 10
        “batch_size”: 4

<i>KerasGClassifier</i> is chosen because the learning task is classfication i.e. assigning each patient a type of cancer. The loss function is <i>binary_crossentropy</i> because the labels are discrete and binary (0 and 1).


<h2> Training the Deep Learning Model </h2>

Install the tool- "Train, Test and Evaluation" and look for the interface as below.

<br>
<p align="center">
  <img width="500" src="/assets/img/searchTrainKeras.png">
</p>
<br>

Choose these parameters.


    “Select a scheme”: Train and validate
    “Choose the dataset containing pipeline/estimator object”: Keras model builder (output of Create deep learning model tool)
    “Select input type”: tabular data
    “Training samples dataset”: X_train
        “Does the dataset contain header”: Yes
        “Choose how to select data by column”: All columns
    “Dataset containing class labels or target values”: y_train
        “Does the dataset contain header”: Yes
        “Choose how to select data by column”: All columns


<p> The above execution produces three outputs- 

<li> <b> model weights </b> on which the training is premised (Binary HDF5 file) </li>
<li> <b> fitted estimator </b> (ZIP file) </li>
<li> <b> cross-validation accuracy </b> (<i> tabular </i> file) </li>
In our run, we achieved an accuracy score of 0.8571428656578064 (~ 85%), which is decent.
</p>

<h2> Testing Prediction Capacity</h2>

<p align="justify"> After training the model, we are tempted to examine if the model is able to make acceptable predictions. We shall execute this model on the test data and study the results. We shall apply the <b> Model Prediction </b> tool, with the following paramaters, for the same. </p>


    “Choose the dataset containing pipeline/estimator object”: Fitted estimator or estimator skeleton (output of Deep learning training and evaluation tool)
    “Choose the dataset containing weights for the estimator above”: Weights trained (output of Create deep learning model tool)
    “Select invocation method”: predict
    “Select input data type for prediction”: tabular data
        “Training samples dataset”: X_test
        “Does the dataset contain header”: Yes
        “Choose how to select data by column”: All columns


<br>
<p align="center">
  <img width="500" src="/assets/img/predictionIP.png">
</p>
<br>

<p align="justify"> The tool returns predicted labels (in a tabular format) for the test data. Note that 0 represents ALL and 1, AML. It is always good to have a visualization of results to make interpretations more intuitive. A great way to infer the prediction results from a ML model is the <a href = "https://en.wikipedia.org/wiki/Confusion_matrix" > <b> confusion matrix </b> </a>, which is a cross-tabulation of the actual and the predicted labels. The tool <b> Machine Learning Visualization Extension </b> helps do that for us. </p> 

<p> The following snapshot of the tool interface highlights all the input parameters. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/forConfusionMatrix.png">
</p>
<br>

<p align="justify"> The confusion matrix shows that 19 and 12 cases were correctly predicted for ALL and AML, by the classifier. In the top-right cell, 1 patient who has ALL is predicted having AML. In the bottom-left cell, 2 patients have AML but are predicted suffering from ALL.  </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/confusionMatrixKeras.png">
</p>
<br>


<h2> References </h2>

<ol>
<li> Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012  </li>
</ol>

