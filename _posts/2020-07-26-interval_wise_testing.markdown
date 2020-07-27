---
layout: post
title: Interval-Wise Testing for Omics Data
date: 2020-07-26 10:20:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics]
---

<h2> Preface </h2>
<p> IWTomics (Cremona et al. 2018) implements the Interval-Wise Testing (IWT; Pini and Vantini 2017) for omics data. The protocol infers differences in the "omics" data between two-sets of genomic regions and doesn't even require manipulating them for comparative scale.</p>

<p> The data used in this exercise is of endogeneous retroviruses in mouse. The agenda is to compare the recombination hotspots in the flanking regions of fixed ETn versus the control regions. Apart from the two region-sets, the dataset also contains a feature “Recombination hotspots content”. More details about the dataset can be viewed in the formal tutorial [1]. </p>


<h2> Loading Data </h2>

<p> Let us commence by loading data into a new session. There are two region-sets, a feature file, and two header files, in that order.</p>

<ol>
<li> <b> Fixed ETn regions </b><i> https://zenodo.org/record/1288429/files/ETn_fixed.bed </i> </li>
<li> <b> Control regions </b><i> https://zenodo.org/record/1288429/files/Control.bed </i> </li>
<li> <b> Recombination Hotspots </b><i> https://zenodo.org/record/1288429/files/Recombination_hotspots.txt </i> </li>
<li> <b> Regions' header </b><i> https://zenodo.org/record/1288429/files/regions_header.tabular </i> </li>
<li> <b> Features' header </b><i> https://zenodo.org/record/1288429/files/features_header.tabular </i> </li>
</ol>

P.S. The "Features' header" file is corrupt at the source and might not be workable.







<h2> References </h2>

<ol>
<li> Marzia A Cremona, Fabio Cumbo, 2020 Interval-Wise Testing for omics data (Galaxy Training Materials). /training-material/topics/statistics/tutorials/iwtomics/tutorial.html Online; accessed Mon Jul 27 2020  </li>
</ol>