---
layout: post
title: Clustering in Machine Learning
date: 2020-07-28 14:42:52 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Machine Learning, Data Science]
---

<h2> Introduction </h2>

<p align="justify"> For an attentive audience, it is known that Machine Learning provides (broadly) for <i> clustering </i>, <i> classification </i>, and <i> regression </i> applications. In this module, we shall discover clustering, which is a form of <b> unsupervised learning </b>. </p>

<h3> Unsupervised Learning </h3>

<p align="justify"> In crude terms, unsupervised learning means <i> learning from scratch </i>. Imagine a dump of <i> unstructured </i> data, with absolutely no clues of direction and symmetry. Although, the attributes of the data are known, it has been randomly spewed over an assembly. Intuitively, the first task is to sift the like ones together. It makes sense. We want to have similar data points together such that the member elements of these cohorts are closer in resemblance as compared to non-members. This is the essence of <i><b>clustering</b></i>. </p>

<p align="justify"> In India, a dish called <i> Khichdi </i> is fairly popular in the northern provinces. It is basically a mix of lentil and rice, served with yogurt and <i>ghee</i> (fat derived from milk). When it came for an intuition, I couldn't resist the urge to make a mention. If <i>Khichdi</i> could be deemed as raw abundance of data, the individual clumps of lentil and rice are two distinct clusters of this data. This is <i>information</i>; information is processed data. For establishing these clusters, we're choosing grains on the basis of their physical properties (color, shape, etc.). With experimental data, we shall adopt mathematical techniques that help underline these groupings.</p>

<p><b> Clustering </b> aims to elucidate covert patterns in the unlabelled data and pull the alike closer into a <i>cluster</i>. Such clusters could be formed with the choice of certain <i> similarity measures </i>. There are several options available for such measures that we'll discuss hereafter.</p>


<h3> Clustering Algorithms </h3>

<p align="justify"> First things first. It is important to base your choice of algorithm on the <b> scale of data </b> at hand. It is common to have millions of data points you'd be working with and a typical algorithm shall compare each datum to the other. This engenders a runtime of <i>  O(n) <sup>2</sup> </i> in complexity notation, obviously bringing in heft to processing and turnaround time. (<i><b>Note:</b> A clustering method called <b> k-means </b> has a runtime complexity of O(n), meaning thereby that it scales linearly with n data points. This is comparatively efficient and we'll discuss that in a while.</i>) There is an array of clustering methods and each one has a master application [1], albeit, we shall focus on the following categories. </p>

<ul>
<li> Centroid-based </li>
<li> Density-based </li>
<li> Distribution-based </li>
<li> Hierarchical </li>
</ul>


<h4> Centroid-based Clustering </h4>

<p align="justify"> With a allusion to k-means in the previous paraphrase, it falls under this type of clustering technique. A centroid is purprotedly the <i> epicenter </i> of the data isolates. It is a score that is central to a cluster and holds the other members with it's weight and "gravity"; like the Sun in our solar system. (<i><b>Note:</b> A centroid might not necessarily be an actual data-point.</i>) </p>    

<h2> References </h2>
<ol>
<li> Xu, D., Tian, Y. A Comprehensive Survey of Clustering Algorithms. Ann. Data. Sci. 2, 165–193 (2015). https://doi.org/10.1007/s40745-015-0040-1 </li>

</ol>