---
layout: post
title: Regression in Machine Learning
date: 2020-07-30 10:08:52 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: regressionCore.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Machine Learning, Data Science]
---

<h2> Introduction </h2>

<p align="justify"> Regression is a technique, extensively used in Machine Learning domain for <b> predicition of continuous values </b>, as an assignment to the target variable, given a series of independent variables. The model learns the input values from an instance (data-row), for each variable/ feature. A line/ curve (regression line) is then attempted to fit the data that is reminiscent of the overall data scatter/ distribution. There are several flavors to regression technique, eg. simple linear regression (fitting straight line to the data, with a dependent/ target variable and an independent variable ), multiple linear regression (series of independent variables and a dependent variable), etc. As can be inferred from the salutation graphic, the better model is the one that is able to accomodate every data point with minimum error, i.e. <b> the true value is as close possible to the predicted value</b>. </p>

<p align="justify"> Let us recall the attributes of a line from the annals of geometry. A line could be strcutured with a <i> slope </i> and an<i> intercept </i>. These values can be realized as pictured below. Assume a data-point lying in a virtual line; and then there is the regression line. Intuitively, if the equations of both lines are same, then it's a perfect match. </p>

<figure>
<p align="center">
<img width="600" height= "400" src="/assets/img/lineEquation.jpg">
</p>
</figure>

<p align="justify"> The slope and intercept are the purported coefficients to the equation of a regression line, as for a regular line. If the slope is constant, the only difference between these two lines is that of <i> intercept </i>, meaning thereby that the lines are parallel. In technical terms, this error (difference between actual and predicted value) for all data-points is gauged and optimized using a <b>cost function</b>; cost is the error incurred in prediciting values. The cost function is typically the <b>Mean Squared Error (MSE)</b> or the <a href = "https://www.wikihow.com/Calculate-the-Sum-of-Squares-for-Error-(SSE)" > <b>Sum of Squared Error (SSE)</b> </a>. </p>

<p align="justify"> It is appropriate to draw a comparison between <b>correlation</b> and <b>regression</b> techniques. While correlation attempts to establish relationships amongst variables, being <i>positively correlated</i> (values following an upward scaling pattern), <i>negatively correlated</i> (values following an downward scaling pattern), or a <i>not correlated</i> at all, regression models the overall data profile by fitting a curve that best defines the pattern. </p>

<p align="justify"> The case study we use in this exercise is that of <i> age prediction </i>. An <a href = "https://www.sciencedirect.com/science/article/pii/S1872497317301643?via%3Dihub" > exegesis </a> is referred where the DNA methylation profiles were analyzed to predict age of the individuals. This is premised over the dogma that the methylation patterns are dynamic and variable to the age. The CpG sites with the highest correlation to age are selected as the biomarkers (and therefore features for building a regression model). </p>

Let us move to the hands-on now. First, we will fetch the testing and training datasets.

<h2> Data </h2>

<p align="justify"> Whole blood samples are collected from humans with their ages falling in the range 18-69 and the best age-correlated CpG sites in the genome are chosen as features. The DNA methylation at the CpG sites offers best biomarking for individuals and their respective age. The training set contains 208 rows corresponding to individual samples and 13 features (age-correlated CpG sites in DNA methylation dataset). The last column is <i>Age</i>. The test set contains 104 rows and the same number of features as the training set. The <i>Age</i> column in the test set is predicted after training on the training set. Another dataset <i>test_rows_labels</i> contains the true age values of the test set which is used to compute scores between true and predicted age. The <i>train_rows</i> contains a column <i>Age</i> which is the label/ target. We will evaluate our model on <i>test_rows</i> and compare the predicted age with the true age in <i>test_rows_labels</i>. </p>

<br>
<figure>
<p align="center">
<img width="250" height= "400" src="/assets/img/regressionData.png">
</p>
</figure>
<br>

We shall proceed to rename the data to <i>test_rows</i>, <i>test_rows_labels</i>, and <i>train_rows</i>  respectively, and confirm that the datatype is <i>tabular</i>.

<p align="justify"> The <i>age</i> is a real number and also the target variable. It cannot be classified as some discrete value and hence the problem becomes a regression problem rather than a classification task. <p>


<h2> Tool Execution </h2>
<h3> Training the Model </h3>

<br>
<figure>
<p align="center">
<img width="750" height="400" src="/assets/img/regressionToolInstall.png">
</p>
</figure>
<br>

Choose the following paramaters.

<ul>
<li><i> “Select a Classification Task” </i>: <b>Train a model</b></li>
<li><i> “Select a linear method” </i>: <b> Linear Regression model </b></li>
<li><i> “Select input type”</i>: <b> tabular data</b></li>
<li><i> param-file “Training samples dataset”</i>: <b> train_rows</b></li>
<li><i> param-check “Does the dataset contain header”</i>: <b> Yes</b></li>
<li><i> param-select “Choose how to select data by column”</i>: <b> All columns EXCLUDING some by column header name(s)</b></li>
<li><i> param-text “Type header name(s)”</i>: <b> Age</b></li>
<li><i> param-file “Dataset containing class labels or target values”</i>: <b> train_rows</b></li>
<li><i> param-check “Does the dataset contain header”</i>: <b> Yes</b></li>
<li><i> param-select “Choose how to select data by column”</i>: <b> Select columns by column header name(s)</b></li>
<li><i> param-text “Type header name(s)”</i>: <b> Age</b></li>
</ul>

<p align="justify"> The output is a <b> compressed ZIP file </b> that contains the fitted model. Now that we have the model, we shall try it with the test data and subsequently visualize the results. </p>

<h3> Testing the Model </h3>

Execute the same tool as above, with the choices as depicted in the screenshot below.

<br>
<figure>
<p align="center">
<img width="700" height="450" src="/assets/img/regressionTest.png">
</p>
</figure>
<br>

<p align="justify"> The predicted data is renamed as <i> predicted_data_linear </i>. It contains no header. A dataset called <i> test_rows_labels</i> has the actual labels and contains a header, which we shall remove (use <i><b> Remove beginning of a file </b></i>, which is a default tool available in Galaxy, and rename the resulting table to <i> test_rows_labels_without_header </i>). This is the data we'll be pitting the predicted values against and then compare and visualize the results. </p>

<br>
<figure>
<p align="center">
<img width="750" height="400" src="/assets/img/regressionResultPlot.png">
</p>
</figure>
<br>

<p align="justify"> The tool <b>Plot actual vs predicted curves and residual plots</b> is available in the repository <b><i> plotly_regression_performance_plots </i></b>. The output from the current run are three plots served as HTML files. </p>

<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/regressionPlot.png">
<figcaption><b>Figure 1: True vs. Predicted Targets</b> <i> The distinctly colored dots represent repsective data-points. Again, lower the difference between actual and preicted values, the better are the results.</i> </figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/regressionResidualPlot.png">
<figcaption><b>Figure 2: Residual Plot</b> <i>Ideally the scatter should be symmetric across y= 0 and exhibit a random spread.</i> </figcaption>
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/regressionScatterPlot.png">
<figcaption><b>Figure 3: Scatter Plot</b> <i> If the prediction is precise, the scatter shall lie close to the line x= y.</i> </figcaption>
</p>
</figure>
<br>



<h2> References </h2>
<ol>
<li> Alireza Khanteymoori, Anup Kumar, Simon Bray, 2020 Regression in Machine Learning (Galaxy Training Materials). /training-material/topics/statistics/tutorials/regression_machinelearning/tutorial.html Online; accessed Fri Jul 31 2020  </li>
</ol>