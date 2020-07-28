---
layout: post
title: Interval-Wise Testing for Omics Data
date: 2020-07-26 10:20:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: genomCov.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics]
---

<h2> Preface </h2>
<p> IWTomics (Cremona et al. 2018) implements the Interval-Wise Testing (IWT; Pini and Vantini 2017) for omics data. The protocol infers differences in the "omics" data between two-sets of genomic regions and doesn't even require manipulating them for comparative scale.</p>

<p> The data used in this exercise is of endogeneous retroviruses in mouse. The agenda is to compare the recombination hotspots in the flanking regions of fixed ETn versus the control regions. Apart from the two region-sets, the dataset also contains a feature “Recombination hotspots content”. More details about the dataset can be viewed in the formal tutorial [1]. </p>

<h2> Tools In-Use </h2>

The following tools are needed to be installed.

<ol>
<li> <b> IWTomics Load </b> tool from the <b> iwtomics_loadandplot </b> repository.</li>
</ol>

<h2> Loading Data </h2>

<p> Let us commence by loading data into a new session. There are two region-sets, a feature file, and two header files, in that order.</p>

<ol>
<li> <b> Fixed ETn regions </b><i> https://zenodo.org/record/1288429/files/ETn_fixed.bed </i> </li>
<li> <b> Control regions </b><i> https://zenodo.org/record/1288429/files/Control.bed </i> </li>
<li> <b> Recombination Hotspots </b><i> https://zenodo.org/record/1288429/files/Recombination_hotspots.txt </i> </li>
<li> <b> Regions' header </b><i> https://zenodo.org/record/1288429/files/regions_header.tabular </i> </li>
<li> <b> Features' header </b><i> https://zenodo.org/record/1288429/files/features_header.tabular </i> </li>
</ol>

<p><i> P.S. The "Features' header" file is a txt file and might not be workable. We shall choose to edit attribues for that file. It is a general scenario in data handling, as most of the data is in the form of tables (tabular) and if supplied as a text file, is not interpreted appropriately by the method. To change the txt file to a tabular format, Galaxy provides for a built-in, data-type conversion facility; one can choose the "Edit attributes" (Pencil icon) for the file and proceed as follows. Also, <b> this example is not the part of this workflow </b>; though the file <b> features_header.tabular </b> can be dealt in a similar fashion after downloading from the source.</i> </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/problemStatement.png">
</p>
<br>

<p> Look for the new data-type. All major data formats are supported by Galaxy. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/changeDataType.png">
</p>
<br>

<br>
<p align="center">
  <img width="500" src="/assets/img/newDataType.png">
</p>
<br>


If everything goes well, you have the original file with a changed profile.

<br>
<p align="center">
  <img width="500" src="/assets/img/dataTypeChangeClick.png">
</p>
<br>

<br>
<p align="center">
  <img width="500" src="/assets/img/dataTypeChangeDone.png">
</p>
<br>

<p> With the file attribute changed, we can now move further with executing the tool. The remaining options set to default, we shall indicate the following input paramaters. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/IWTomicsInput.png">
</p>
<br>


<h2> References </h2>

<ol>
<li> Marzia A Cremona, Fabio Cumbo, 2020 Interval-Wise Testing for omics data (Galaxy Training Materials). /training-material/topics/statistics/tutorials/iwtomics/tutorial.html Online; accessed Mon Jul 27 2020  </li>
</ol>