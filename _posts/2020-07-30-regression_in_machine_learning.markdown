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


<h2> Using Ensemble Methods </h2>

<p align="justify"> Frequently, a single model is a feeble exposition of the data. It is always advisable to work with multiple instances of a model (learner with varying supplements of choice of data-instances, parameters, partitioning, tuning convergence, etc.) and lionize the aggregation of results. A linear regression might not always be the best fit for the data. What if the spread is more concave or convex? </p>


<p align="justify"> To exemplify, a <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/MachineLearning/blob/master/Machine_Learning_Random_Forests/hands_on_random_forests_ep.ipynb" > <b>Random Forest</b> </a> algorithm is a better choice than a <a href = "https://nbviewer.jupyter.org/github/shauryajauhari/MachineLearning/blob/master/Machine_Learning_Random_Forests/hands_on_random_forests_ep.ipynb" > <b>Decision Tree</b> </a>. Why? Because <i>multiple trees consistute a forest</i>, and aggregation of many decision trees converges into the output of a random forest. It is an ensemble based classifier and always preferable to employ. Machine Learning is always about the intricacies of statistics (working with sample data to train and test), and so to maximize our chances of a win, it must be ensured that randomness has been cornered as far possible.</p>

<p align="justify"> To work with ensemble methods, we shall load the tool <b> Ensemble methods <i>for classification and regression</i> </b> from the repository <b>sklearn_ensemble</b>. We shall be using <a href = "https://scikit-learn.org/stable/modules/generated/sklearn.ensemble.GradientBoostingRegressor.html#sklearn.ensemble.GradientBoostingRegressor" > <b>Gradient Boosting regressor </b> </a>. Make the choices for the paramaters as pictured below.</p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/gradientBoosterOptions.png">
</p>
</figure>
<br>

<p align="justify"> After training, let's examine the performance of the model on the test data. Prior though, rename the model to <i>gradient_boosting_model</i>. For testing, the parameters could be chosen like below.</p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/gradientBoosterTest.png">
</p>
</figure>
<br>

<p align="justify"> Again, rename the results to <i>predicted_data_gradient_boosting</i>. Now, load the tool <b> Plot actual vs predicted curves and residual plots</b>.</p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/plotActualPredictedOptions.png">
</p>
</figure>
<br>

Let's visualize the results. The justification of the results could be reciprocated from the explanations above.

<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/ensembleActualPredictedPlot.png">
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/ensembleResidualPlot.png">
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/ensembleScatterPlot.png">
</p>
</figure>
<br>



<h2> Creating Data Processing Pipeline </h2>

To further our analysis, we shall install a tool <i>Pipeline Builder</i> first.

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/pipelineBuilderInstall.png">
</p>
</figure>
<br>

After installation, let us execute the tool with the results we have.

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/pipelineBuilderOptions.png">
</p>
</figure>
<br>

<p align="justify"> The output is rudimentarily a <i>wrapper</i> that encapsulates this ensemble leaner. The paramaters choosen for this model shall be engendered in a seperate archive. Likewise, we can extend the same pipeline for any other <i>optimum</i> set of arguments. For that we need another tool called <i> Hyperparamater search </i>. We will install it too. </p>  


<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/hyperparameterSearchInstall.png">
</p>
</figure>
<br>

<h3> Hyperparameter Search </h3>

<p align="justify"> After creating a pipeline builder, we will use  the tool <i> Hyperparameter search </i> to trace the best values for each hyperparameter, so as to establish an optimum model based on the search space chosen for each hyperparameter. We use only one parameter <i>n_estimators</i> of Gradient boosting regressor for this task. This parameter specifies the number of boosting stages the learning process has to go through. The default value of <i>n_estimators</i> for this regressor is 100. However, we are not sure if this gives the best accuracy. Therefore, it is important to try setting this parameter to different values to find the optimal one. We choose some values which are less than 100 and a few more than 100. The hyperparameter search will look for the optimal number of estimators and gives the best-trained model as one of the outputs. This model is used in the next step to predict age in the test dataset. </p>

Install the tool and make the following choices.

<ul>
<li><i>“Select a model selection search scheme”</i>: <b>GridSearchCV - Exhaustive search over specified parameter values for an estimator</b></li>
<li><i>param-files “Choose the dataset containing pipeline/estimator object”</i>: <b>zipped file (output of Pipeline builder tool)</b></li>
<li><i>“Is the estimator a deep learning model?”</i>: <b>No</b></li>
- In “Search parameters Builder”:
<li><i>param-files “Choose the dataset containing parameter names”</i>: <b>tabular file (the other output of Pipeline builder tool)</b></li>
- In “Parameter settings for search”:
<li><i>param-repeat “1: Parameter settings for search”</i></li>
<li><i>“Choose a parameter name (with current value)”</i>: <b>n_estimators: 100</b></li>
<li><i>“Search list”</i>: <b>[25, 50, 75, 100, 200]</b></li>
- In “Advanced Options for SearchCV”:
<li><i>“Select the primary metric (scoring)”</i>: <b>Regression -- 'r2'</b></li>
<li><i>“Select the cv splitter”</i>: <b>KFold</b></li>
</ul>

<p align="justify"> There are different ways to split the dataset into training and validation sets. In our tutorial, we will use KFold which splits the dataset into K consecutive parts. It is used for cross-validation. It is set to 5 using another parameter n_splits. </p>

<ul>
<li><i>“n_splits”</i>:<b>5</b></li>
<li><i>“Whether to shuffle data before splitting”</i>: <b>Yes</b></li>
<li><i>“Random seed number”</i> :<b>3111696</b></li>                        
</ul>

<p align="justify"> It is set to an integer and used to retain the randomness/accuracy when “Whether to shuffle data before splitting” is Yes across successive experiments. </p>

<ul>
<li><i>“Raise fit error”</i>:<b>No</b></li>
</ul>

<p align="justify"> While setting different values for a parameter during hyperparameter search, it can happen that wrong values are set, which may generate an error. To avoid stopping the execution of a regressor, it is set to No which means even if a wrong parameter value is encountered, the regressor does not stop running and simply skips that value. </p>

<ul>
<li><i>“Select input type”</i>: <b> tabular data</b></li>
<li><i>param-files “Training samples dataset”</i>: <b> train_rows tabular file</b></li>
<li><i>“Does the dataset contain header”</i>: <b> Yes</b></li>
<li><i>“Choose how to select data by column”</i>: <b> All columns EXCLUDING some by column header name(s)</b></li>
<li><i>“Type header name(s)”</i>: <b> Age</b></li>
<li><i>param-files “Dataset containing class labels or target values”</i>: <b> train_rows tabular file</b></li>
<li><i>“Does the dataset contain header”</i>: <b> Yes</b></li>
<li><i>“Choose how to select data by column”</i>: <b> Select columns by column header name(s)</b></li>
<li><i>“Type header name(s)”</i>: <b> Age</b></li>
<li><i>“Whether to hold a portion of samples for test exclusively?”</i>: <b> Nope</b></li>
<li><i>“Save best estimator?”</i>: <b>Fitted best estimator or Detailed cv_results_ from nested CV</b></li>
</ul>

<font color="#800080" >
<p><b>Exercise</b></p>
<ol>
<li> The run will engender two outputs. Analyze the <i>tabular</i> output and ascertain the optimum number of estimators for the gradient boosting regressor.</li>
</ol>
</font>


<p align="justify"> The other output from the run of Hyperparameter search (zipped file) is the optimized model. Now, to predict the age, we shall execute this model, for probably improvised results. </p>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/hyperparameterSearchReRun.png">
</p>
</figure>
<br>

Next, we shall plot the results again and compare with the existing ones. (<i><b>Note:</b> The metric R2 is better when closer to 1.0</i>) .


<h3> Regression Plots </h3>

<br>
<figure>
<p align="center">
<img width="500" src="/assets/img/finalRegressionPlotStatus.png">
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/regressionActualPredictedFinal.png">
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/regressionResidualPredictedFinal.png">
</p>
</figure>
<br>


<br>
<figure>
<p align="left">
<img width="750" height="500" src="/assets/img/regressionScatterPlotFinal.png">
</p>
</figure>
<br>

<p align="justify">The interpretation for the former two plots has to be made visually, but the latter one highlights <b>RMSE</b> and <b>R2</b> values that are crispier than before. This is definitely a better version.</p>


<h2> References </h2>
<ol>
<li> Alireza Khanteymoori, Anup Kumar, Simon Bray, 2020 Regression in Machine Learning (Galaxy Training Materials). /training-material/topics/statistics/tutorials/regression_machinelearning/tutorial.html Online; accessed Fri Jul 31 2020  </li>
</ol>