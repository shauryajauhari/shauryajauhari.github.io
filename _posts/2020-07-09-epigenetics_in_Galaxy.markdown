---
layout: post
title: Epigenetics in Galaxy
date: 2020-07-09 12:44:05 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: methylationOutput.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [ChIP-Seq, DNA Methylation]
---

<p> We are dealing with sequencing data, and the magnitude of data is so immersive that the efforts in analysis are very tedious and sophisticated. It is always better to make conscious choices of tools and their respective paramters, at every stage, as this may weed off any prospective errors.</p>

<p> Before delving into the epigenetic data analysis, let us cover the basics of <b>[Quality Control](https://galaxyproject.github.io/training-material/topics/sequence-analysis/tutorials/quality-control/tutorial.html#inspect-a-raw-sequence-file)</b> and <b>[Data Mapping](https://galaxyproject.github.io/training-material/topics/sequence-analysis/tutorials/mapping/tutorial.html)</b>. These pipelines are available from the official <b>[Galaxy Training service](https://galaxyproject.github.io/training-material/)</b>, yet we are going to cover them swiftly here.</p>

## Quality Control

<p> Before anything though, we must execute the galaxy instance and create a session; then load the file to examine. Please refer to <b>[Introduction To Galaxy](https://rpubs.com/shauryajauhari/introGalaxy)</b> for details. </p>
<p>We shall commence by assigning an appropriate name for our analysis session. This can be achieved via renaming the "unnamed history".</p>
<br>
<p align="center">
  <img width="300" height="150" src="/assets/img/renameHistory.png">
</p>
<br>
<p>Thereafter, we shall load the data into this newly created session. There could be disparate approaches to loading the data. It could either be loaded from the local host system by browsing the file from the disk, or alternatively it could be sourced from 

<p align="center">
  <img width="500" height="300" src="/assets/img/fileSourcing.png">
</p>
<br>

<p align="center">
  <img width="500" height="300" src="/assets/img/dataLoading.png">
</p>
<br>


## Mapping

