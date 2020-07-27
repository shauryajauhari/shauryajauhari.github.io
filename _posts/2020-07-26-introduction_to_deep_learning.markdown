---
layout: post
title: Introduction to Deep Learning
date: 2020-07-26 14:15:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Deep Learning, Statistics, Data Science]
---

<h2> Introduction </h2>
<p> Deep Learning convolves state-of-the-art ML theme. Kindly visit this <a href = "https://rpubs.com/shauryajauhari/deep_learning" > link </a> for my brief presentation from the previous workshop and an <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/MachineLearning/blob/master/Machine_Learning_Deep_Learning/hands_on_deep_learning_ep.ipynb" > example workflow in R </a>.</p>

<p> Assuming a fair understanding for the subject, let's dive right into a data analysis workflow in Galaxy. This exercise is again derived from the official training available <a href = "https://galaxyproject.github.io/training-material/topics/statistics/tutorials/intro_deep_learning/tutorial.html" > here </a>. </p>


<p> Install the repositories- <i> keras_model_config </i>, <i> sklearn_train_test_eval </i>,  and <i> keras_model_builder </i> from the Tool Shed. </p>


<h2> Loading Data </h2>

<p> Let us commence by loading data into a new session. The following could be renamed as <i>X_test</i>, <i>X_train</i>, <i>y_test</i>, and <i>y_train</i> respectively.</p>

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

<p> The data in place, we may proceed towards building the model architecture with the following paramaters. </p>

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

<p> The tool returns a JSON output file with the attributes about the neural networks. The same can be viewed by clicking the "eye" icon. This output goes to the next stage of consolidating the deep learning model with additional parameters as optimiser, loss function, and the number of epochs and batch size (training attributes). The loss function is chosen as <b>binary_crossentropy</b> as the learning task is classification of binary labels (0 and 1). </p>

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

