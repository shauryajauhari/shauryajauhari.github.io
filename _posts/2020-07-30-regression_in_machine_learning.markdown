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

<p align="justify"> Regression is a technique, extensively used in Machine Learning domain for <b> predicition of continuous values </b>, as an assignment to the target variable, given a series of independent variables. The model learns the input values from an instance (data-row), for each variable/ feature. A line/ curve (regression line) is then attempted to fit the data that is reminiscent of the overall data scatter/ distribution. There are several flavors to regression technique, eg. linear regression (fitting straight line to the data, with a dependent/ target variable and an independent variable ), multiple regression (series of independent variables and a dependent variable), etc. As can be inferred from the salutation graphic, the better model is the one that is able to accomodate every data point with minimum error, i.e. <b> the true value is as close possible to the predicted value </b>. </p>


<p align="justify"> The case study we use in this exercise is that of <i> age prediction </i>. A <a href = "https://www.sciencedirect.com/science/article/pii/S1872497317301643?via%3Dihub" > study </a> is referred where the DNA methylation profiles were analyzed to predict age of the individuals. This is premised over the dogma that the methylation patterns are dynamic and variable to the age. The CpG sites with the highest correlation to age are selected as the biomarkers (and therefore features for building a regression model). </p>

<h2> References </h2>
<ol>
<li> Alireza Khanteymoori, Anup Kumar, Simon Bray, 2020 Regression in Machine Learning (Galaxy Training Materials). /training-material/topics/statistics/tutorials/regression_machinelearning/tutorial.html Online; accessed Fri Jul 31 2020  </li>
</ol>