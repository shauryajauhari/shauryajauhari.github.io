---
layout: post
title: Sensitivity and Specificity
date: 2020-06-20 09:21:09 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: sensitivity.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Statistics, Data Science]
---

<p>There is certain hysteria associated with <b><i>sensitivty</i></b> and <b><i>specificity</i></b> in the domain of Machine Learning and Data Science. Contrarily, though the idea is pretty straightforward if one has a reasonable understanding about <i>hypothesis testing</i> and <i>statistics</i>.</p>
<p>When we are dealing with a classification problem with a binomial outcome, <i>i.e.</i> disease or not, rich or poor, fail or pass, etc., we have a notion of a positive class and a negative class. This notion is completely arbitrary and solely depends on the problem at hand. For exemplifying, let us assume that a problem has "Pass" as a positive class and "Fail" as a negative class; <i> big surprise !</i></p>
<p> With the aforementioned background, our definition for sensitivity is a metric that quantifies a method's efficacy to label an instance as "Pass". A method could be a novel one, projected for a comparitive analysis with other methods, an underlying theory that defines a label based on some features/ variables, or even a proposed hypothesis that given a set of attributes (say marks in several subjects, here) a candidate is declared "Pass" or "Fail". Mathematically, sensitivity is defined as the ratio of <b>True Positives</b> and the <b>Total Positives</b>.</p> 

<p><i><b>Sensitivity = True Positives &frasl; Total Positives</b></i></p>
<p><b>OR</b> </p>
<p><i><b>Sensitivity &equiv;True Positives &frasl; (True Positives + False Positives)</b></i></p>


<p> Specificity, on the other hand, determines a method's capability of highlighting the negative classes. If "Pass" is considered a positive label, then definitely "Fail" is a negative class.</p> 

<p><i><b>Specificity = True Negatives &frasl; Total Negatives</b></i></p>
<p><b>OR</b> </p>
<p><i><b>Specificity &equiv;True Negatives &frasl; (True Negatives + False Negatives)</b></i></p>

<p>A <i>confusion matrix</i> is often a ready-reckoner for these values, as illustrated below.</p>

<p align="center">
  <img width="300" height="150" src="/assets/img/confusionMatrix.png">
</p>

<p>Ideally, we expect high values of both sensitivity and specificity. Another metric that encompasses these two parameters, so as to engender a grander view of a tool's performance is <b>Area Under Curve (AUC)</b> of <b>Reciever Operator Charactersitic (ROC) curve</b>. So, greater the area, the better it is.</p>

<p align="center">
  <img width="350" height="300" src="/assets/img/roc.png">
</p>


