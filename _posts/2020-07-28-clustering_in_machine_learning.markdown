---
layout: post
title: Clustering in Machine Learning
date: 2020-07-28 14:42:52 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: khichdiClustered.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Machine Learning, Data Science]
---

<h2> Introduction </h2>

<p align="justify"> For an attentive audience, it is known that Machine Learning provides (broadly) for <i> clustering </i>, <i> classification </i>, and <i> regression </i> applications. In this module, we shall discover clustering, which is a form of <b> unsupervised learning </b>. For a fledged version of this tutorial, visit this <a href = "https://galaxyproject.github.io/training-material/topics/statistics/tutorials/clustering_machinelearning/tutorial.html" > page </a>.</p>

<h3> Unsupervised Learning </h3>

<p align="justify"> In crude terms, unsupervised learning means <i> learning from scratch </i>. Imagine a dump of <i> unstructured </i> data, with absolutely no clues of direction and symmetry. Although, the attributes of the data are known, it has been randomly spewed over an assembly. Intuitively, the first task is to sift the like ones together. It makes sense. We want to have similar data points together such that the member elements of these cohorts are closer in resemblance as compared to non-members. This is the essence of <i><b>clustering</b></i>. </p>

<p align="justify"> In India, a dish called <i> Khichdi </i> is fairly popular in the northern provinces. It is basically a mix of lentil and rice, served with yogurt and <i>ghee</i> (fat derived from milk). When it came for an intuition, I couldn't resist the urge to make a mention. If <i>Khichdi</i> could be deemed as raw abundance of data, the individual clumps of lentil and rice are two distinct clusters of this data. This is <i>information</i>; information is processed data. For establishing these clusters, we're choosing grains on the basis of their physical properties (color, shape, etc.). With experimental data, we shall adopt mathematical techniques that help underline these groupings.</p>


 <table style="width:80%" align="center">
  <tr>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/khichdiOne.jpg">
    <figcaption> <i>Mixture, representing unlabelled elements.</i> </figcaption>
    </p>
    </figure>
    </th>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/khichdiClustered.jpg">
    <figcaption> <i>Two clusters of lentil and rice.</i> </figcaption>
    </p>
    </figure>
    </th>
  </tr>
</table> 

<p><b> Clustering </b> aims to elucidate covert patterns in the unlabelled data and pull the alike closer into a <i>cluster</i>. Such clusters could be formed with the choice of certain <i> similarity measures </i>. There are several options available for such measures that we'll discuss hereafter.</p>


<h3> Clustering Algorithms </h3>

<p align="justify"> First things first. It is important to base your choice of algorithm on the <b> scale of data </b> at hand. It is common to have millions of data points you'd be working with and a typical algorithm shall compare each datum to the other. This engenders a runtime of <i>  O(n) <sup>2</sup> </i> in complexity notation, obviously bringing in heft to processing and turnaround time. (<i><b>Note:</b> A clustering method called <b> k-means </b> has a runtime complexity of O(n), meaning thereby that it scales linearly with n data points. This is comparatively efficient and we'll discuss that in a while.</i>) There is an array of clustering methods and each one has a master application [1], albeit, we shall focus on the following categories; gists of their definitions follow.</p>

<ul>
<li><b> Centroid-based </b></li>
<li><b> Density-based </b></li>
<li><b> Distribution-based </b></li>
<li><b> Hierarchical </b></li>
</ul>


<h4> Centroid-based Clustering </h4>

<p align="justify"> With a allusion to k-means in the previous paraphrase, it falls under this type of clustering technique. A centroid is purprotedly the <i> epicenter </i> of the data isolates. It is a score that is central to a cluster and holds the other members with it's weight and "gravity"; like the Sun in our solar system. (<i><b>Note:</b> A centroid might not necessarily be an actual data-point.</i>) </p>    


<h4> Density-based Clustering </h4>

<p align="justify"> Density-based clusters are <b> vicinal regions of high-density </b>, that are separated by objects of low-density. Basically, the overall data profile is assumed to have dense-regions(clusters) and sparse-regions(noise). Also, other algorithms work well with clusters having a regular,geometric shape; eg. circle, oval, etc. It is a distinct possibility that the real-world data isn't "pretty" enough. That is the starting point of methods like DBSCAN, that handle non-convex groupings and outliers/ noise relatively well. <b> Density-Based Spatial Clustering and Application with Noise (DBSCAN)(Ester et al. 1996) </b> is one such algorithm that we'll be implementing later in this tutorial. The graphic below shows convexed dense-cohorts for illustration, but you get the idea.</p>

<br>
<figure>
<p align="center">
  <img src="/assets/img/clusteringDensityCentroid.jpg" width="500" alt="" title="">
</p>
</figure>
<br>

<h4> Distribution-based Clustering </h4>
<p align="justify"> As the name suggests, distribution-based clustering is implemented by bringing together in a cluster, those elements that align to properties of a statistical data distribution, eg. Normal (Gaussian), Chi-Squared, etc. The most popular algorithm in this type of technique is <b> Expectation-Maximization (EM) </b> clustering using <b> Gaussian Mixture Models (GMM) </b>. </p>

<h4> Hierarchical Clustering </h4>
<p align="justify"> This type of clustering underlines <i> clusters being part of other (super) clusters </i>. The graphic below depicts the same idea. In data analysis, a common pratice is to create a <a href = "https://en.wikipedia.org/wiki/Dendrogram" > <b>dendogram</b> </a> to represent hierarchical clusters. </p>

<br>
<figure>
<p align="center">
  <img src="/assets/img/hierarchicalClustering.jpg" width="500" alt="" title="">
</p>
</figure>
<br>

<p align="justify"> Also rudimentarily, there are a couple of distance measures that are generally employed to ascertain relative separation of clusters and member elements within a cluster. These are <a href = "https://en.wikipedia.org/wiki/Euclidean_distance" > <i><b> euclidean </b></i> </a> and <a href = "https://en.wiktionary.org/wiki/Manhattan_distance" > <i><b> manhattan </b></i> </a> distances. A euclidean distance, is essentially <i> the square root of the summation of squared differences between the coordinates between two points</i>. Generally found applications use euclidean distance as a clustering measure. </p>


<h2> Data </h2>

<p align="justify"> For the current session, we shall employ the acclaimed <a href = "https://en.wikipedia.org/wiki/Iris_flower_data_set" > <b> iris dataset </b></a>. Let us upload the following data to a novel Galaxy session.

<ul>
<li> <i> https://zenodo.org/record/3813447/files/iris.csv </i></li>
<li><i> https://zenodo.org/record/3813447/files/circles.csv </i></li>
<li><i> https://zenodo.org/record/3813447/files/moon.csv </i></li>
</ul>
</p>

Rename the datasets to <i>iris</i>, <i>circles</i> and <i>moon</i> respectively. Also, ensure that the datatype for the datasets is <i> comma-separated-value (csv) </i>.

<br>
<figure>
<p align="center">
  <img src="/assets/img/checkAttribute.png" width="240" height="500" alt="" title="">
</p>
</figure>
<br>

Our objective is to group the flowers into similar categories. To do that look for sklearn's repository for the same.

<h2> Tools' Execution </h2>

<h3> Hierarchical Clustering </h3>

<br>
<figure>
<p align="center">
  <img src="/assets/img/installNumericClustering.png" width="500" alt="" title="">
</p>
</figure>
<br>

Make the following choices.


    “Select the format of input data”: Tabular Format (tabular,txt)
        param-file “Data file with numeric values”: iris
        param-check “Does the dataset contain header”: Yes
        param-select “Choose how to select data by column”: All columns EXCLUDING some by column header name(s)
            param-text “Type header name(s)”: Species
        param-select “Clustering Algorithm”: Hierarchical Agglomerative Clustering
        In “Advanced options”
            param-text “Number of clusters”: 2
            param-select “Affinity”: Euclidean
            param-select “Linkage”: ward


After the successful run, rename the resulting dataset.

<br>
<figure>
<p align="center">
  <img src="/assets/img/renameHierarchicalClustering.png" width="230" height="500" alt="" title="">
</p>
</figure>
<br>

<p align="justify"> Next is the time to visualize the results. We shall use the <b> Scatterplot with ggplot2 </b> tool in the <b> ggplot2_point </b> repository to do this. Understandably, we will be able to see distinct clusters of data, i.e. different categories of flowers. Install and execute the tool with the following options. </p>


      “Input tabular dataset”: Hierarchical clustering
      “Column to plot on x-axis”: 1
      “Column to plot on y-axis”: 2
      “Plot title”: Hierarchical clustering in iris data
      “Label for x axis”: Sepal length
      “Label for y axis”: Sepal width
      In “Advanced Options”:

          “Data point options”: User defined point options
              “relative size of points”: 2.0
          “Plotting multiple groups”: Plot multiple groups of data on one plot
              “column differentiating the different groups”: 6
              “Color schemes to differentiate your groups”: Set 2 - predefined color pallete

      In “Output options”:

          param-text “width of output”: 7.0
          param-text “height of output”: 5.0
          param-text “dpi of output”: 175.0



Visualize the resulting image.

<br>
<figure>
<p align="center">
  <img src="/assets/img/scatterplotOutputIrisHierarchical.png" width="500" alt="" title="">
</p>
</figure>
<br>

<p align="justify"> There are three species listed in the dataset- <i><b> setosa </b></i>, <i><b> versicolor </b></i>, and <i><b> virginica  </b></i>. When you look at the clustering results, you'll see that all the setosa samples are grouped in one cluster and two other species (versicolor and virginica) are grouped in another one. There are two clusters in the figure, and it becomes obvious that versicolor and virginica are more similar to each other, being marked in the same cluster (0: green). (<i><b> Note: </b> 0 and 1 are cluster labels </i>.) </p>


<h3> K-means Clustering </h3>


<p align="justify"> K-means clustering is a way of partitioning data into 'k' clusters, where k is a defined by the user, aprori. Each of the k-clusters is represented by a central value that is the mean of the data points within that cluster. More information can be found <a href = "https://docs.microsoft.com/en-us/azure/machine-learning/studio-module-reference/k-means-clustering" > here </a>.</p>


Moving ahead, we're going to execute the same protocol as above, now with k-means clustering algorithm. Make the following choices with the <i> Numeric Clustering </i> tool again.

    Select the format of input data”: Tabular Format (tabular,txt)

        param-file “Data file with numeric values”: iris
        param-check “Does the dataset contain header”: Yes
        param-select “Choose how to select data by column”: All columns EXCLUDING some by column header name(s)
            param-text “Type header name(s)”: Species
        param-select “Clustering Algorithm”: KMeans
        In “Advanced options”
            param-text “Number of clusters”: 2


<p align="justify"> For convenience, we'll rename the results as <i> k-means clustering </i>. Next, same as before, we'll plot the resulting data table with ggplot2. </p>

The paramter readings are as under.

    “Input tabular dataset”: k-means clustering
    “Column to plot on x-axis”: 1
    “Column to plot on y-axis”: 2
    “Plot title”: K-means clustering in iris data
    “Label for x axis”: Sepal length
    “Label for y axis”: Sepal width
    In “Advanced Options”:

        “Data point options”: User defined point options
            “relative size of points”: 2.0
        “Plotting multiple groups”: Plot multiple groups of data on one plot
            “column differentiating the different groups”: 6
            “Color schemes to differentiate your groups”: Set 2 - predefined color pallete

    In “Output options”:

        param-text “width of output”: 7.0
        param-text “height of output”: 5.0
        param-text “dpi of output”: 175.0


<br>
<figure>
<p align="center">
  <img src="/assets/img/scatterplotOutputIrisKmeans.png" width="500" alt="" title="">
</p>
</figure>
<br>


<font color="#800080" >
<p><b>Exercise</b></p>
<ol>
<li> How to find optimum value for <i>k</i> in k-means clustering? </li> 
<li> What is the difference between k-means and hierarchical clustering? </li>
</ol>
</font>

<h3> DBSCAN Clustering </h3>

Executing the tool.

    Select the format of input data”: Tabular Format (tabular,txt)

        param-file “Data file with numeric values”: iris
        param-check “Does the dataset contain header”: Yes
        param-select “Choose how to select data by column”: All columns EXCLUDING some by column header name(s)
            param-text “Type header name(s)”: Species
        param-select “Clustering Algorithm”: DBSCAN


Visualizing results.

    “Input tabular dataset”: DBSCAN clustering
    “Column to plot on x-axis”: 1
    “Column to plot on y-axis”: 2
    “Plot title”: DBSCAN clustering in iris data
    “Label for x axis”: Sepal length
    “Label for y axis”: Sepal width
    In “Advanced Options”:

        “Data point options”: User defined point options
            “relative size of points”: 2.0
        “Plotting multiple groups”: Plot multiple groups of data on one plot
            “column differentiating the different groups”: 6
            “Color schemes to differentiate your groups”: Set 2 - predefined color pallete

    In “Output options”:

        param-text “width of output”: 7.0
        param-text “height of output”: 5.0
        param-text “dpi of output”: 175.0


<br>
<figure>
<p align="center">
  <img src="/assets/img/scatterplotOutputIrisDBSCAN.png" width="500" alt="" title="">
</p>
</figure>
<br>

<p align="justify"> We see that unlike k-means and hierarchical clustering, DBSCAN was able to find all three species. We had pre-specified the number of clusters in the former two executions. </p>

All results together, for perspective.

<table style="width:100%" align="center">
  <tr>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/scatterplotOutputIrisHierarchical.png">
    </p>
    </figure>
    </th>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/scatterplotOutputIrisKmeans.png">
    </p>
    </figure>
    </th>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/scatterplotOutputIrisDBSCAN.png">
    </p>
    </figure>
    </th>
  </tr>
</table> 

<br>
<font color="#800080" >
<p><b>Exercise</b></p>
<ol>
<li> There is a concept of a <a href = "https://en.wikipedia.org/wiki/Silhouette_(clustering)" > <b>silhouette coefficient</b> </a> to evaluate the clustering results. Can you explore the veracity of these results? </li> 
</ol>
</font>


<h2> Applying Clustering on Multiple Datasets </h2>
<h3> Data Visualization </h3>

<p align="justify">Just like before, the regression analysis can be scaled to multiple datasets taken simultaneously. Let us include the "moon" and "circles" datasets (imported before) for this module. </p>

<br>
<figure>
<p align="center">
  <img src="/assets/img/multipleDatasetsScatterPlot.png" width="500" alt="" title="">
</p>
</figure>
<br>

<table style="width:80%" align="center">
  <tr>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/moonScatterPlot.png">
    <figcaption> <i>Scatter plot for <b>moon</b> dataset.</i> </figcaption>
    </p>
    </figure>
    </th>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/circlesScatterPlot.png">
    <figcaption> <i>Scatter plot for <b>circles</b> dataset.</i> </figcaption>
    </p>
    </figure>
    </th>
  </tr>
</table> 


<h3> Cluster Data Visualization </h3>

<p align="justify"> We'l resort back to the <b>Numeric clustering</b> tool and process the algorithm with the parameters defined in the following screenshot. </p>

<br>
<figure>
<p align="center">
  <img src="/assets/img/numericClusteringMultipleDatasets.png" width="700" alt="" title="">
</p>
</figure>
<br>

Again, we visualize these results.

<ul>
<li><i>“Input tabular dataset”</i> : <b>Numeric Clustering on circles</b> and <b>Numerical Clustering on moon</b> as <i>multiple datasets</i></li>
<li><i>“Column to plot on x-axis”</i> : <b>1</b></li>
<li><i>“Column to plot on y-axis”</i> : <b>2</b></li>
<li><i>“Plot title”</i> : <b>Hierarchical clustering</b></li>
<li><i>“Label for x axis”</i> : <b>X</b></li>
<li><i>“Label for y axis”</i> : <b>Y</b></li>
- In “Advanced Options”:
<li><i>“Data point options”</i> : <b>User defined point options</b></li>
<li><i>“relative size of points”</i> : <b>2.0</b></li>
<li><i>“Plotting multiple groups”</i> : <b>Plot multiple groups of data on one plot</b></li>
<li><i>“column differentiating the different groups”</i> : <b>3</b></li>
<li><i>“Color schemes to differentiate your groups”</i> : <b>Set 2 - predefined color pallete</b></li>
- In “Output options”:
<li><i>“width of output”</i> : <b>7.0</b></li>
<li><i>“height of output”</i> : <b>5.0</b></li>
<li><i>“dpi of output”</i> : <b>175.0</b></li>
</ul>

<table style="width:80%" align="center">
  <tr>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/moonScatterPlotFinal.png">
    <figcaption> <i>Scatter plot for <b>moon</b> dataset.</i> </figcaption>
    </p>
    </figure>
    </th>
    <th>
    <figure>
    <p align="center">
    <img width="500" height= "200" src="/assets/img/circlesScatterPlotFinal.png">
    <figcaption> <i>Scatter plot for <b>circles</b> dataset.</i> </figcaption>
    </p>
    </figure>
    </th>
  </tr>
</table> 

<br>
<font color="#800080" >
<p><b>Exercise</b></p>
<ol>
<li> You can apply the other two algorithms (k-means and DBSCAN) to moon and circles datasets in the same way as explained above. In the k-means algorithm, please use <b>k=2</b> and for the DBSCAN algorithm, the parameters should not be the default ones as used earlier. They should be set as follows: 
<ul>
<li> for the circles dataset (<b>maximum neighborhood distance=0.2</b> and <b>minimal core point density=5</b>), and </li> 
<li> for the moon dataset (<b>maximum neighborhood distance=0.3</b> and <b>minimal core point density=4</b>). </li>
</ul>
</li> 
</ol>
</font>


<h2> References </h2>
<ol>
<li> Xu, D., Tian, Y. A Comprehensive Survey of Clustering Algorithms. Ann. Data. Sci. 2, 165–193 (2015). https://doi.org/10.1007/s40745-015-0040-1 </li>

</ol>