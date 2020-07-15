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

<p> Before delving into the epigenetic data analysis, let us cover the basics of <b><a href= "https://galaxyproject.github.io/training-material/topics/sequence-analysis/tutorials/quality-control/tutorial.html#inspect-a-raw-sequence-file"> Quality Control </a></b> and <b><a href = "https://galaxyproject.github.io/training-material/topics/sequence-analysis/tutorials/mapping/tutorial.html" > Data Mapping </a></b>. These pipelines are available from the official <b><a href= "https://galaxyproject.github.io/training-material/" > Galaxy Training service </a></b>, yet we are going to overview them swiftly here.</p>

<h2> Quality Control </h2>

<p> Before anything though, we must execute the galaxy instance and create a session; then load the file to examine. Please refer to <b><a href= "https://rpubs.com/shauryajauhari/introGalaxy" > Introduction To Galaxy </a> </b> for details. </p>
<p>We shall commence by assigning an appropriate name for our analysis session. This can be achieved via renaming the "unnamed history".</p>
<br>
<p align="left">
  <img width="300" height="150" src="/assets/img/renameHistory.png">
</p>
<br>
<p>Thereafter, we shall load the data into this newly created session. There could be disparate approaches to loading the data. It could either be loaded from the local host system by browsing the file from the disk, or alternatively it could be sourced from 

<p align="left">
  <img width="500" height="300" src="/assets/img/fileSourcing.png">
</p>
<br>

<p align="left">
  <img width="500" height="300" src="/assets/img/dataLoading.png">
</p>
<br>




<p>When the data has been successfully loaded into the session's library (history), a green ambience could be realized in the file listing.</p>


<p align="left">
  <img width="500" height="300" src="/assets/img/successfullyLoaded.png">
</p>
<br>

<p align="left">
  <img width="500" height="300" src="/assets/img/allSet.png">
</p>
<br>

<p> Next, we rename the file for convenience to facilitate downstream analysis. </p>

<p align="left">
  <img width="500" height="300" src="/assets/img/renameFile.png">
</p>
<br>

<p><i> P.S. Due to network issues, the data was manually downloaded from the source and uploaded to galaxy instance. </i></p>


<p>We can have a cursory glance at the data.</p>
<p align="left">
  <img width="500" height="300" src="/assets/img/dataGlance.png">
</p>
<br>

<p>For more details on the format, please visit details <a href = "https://en.wikipedia.org/wiki/FASTQ_format" > here </a>. </p>


 <p>After looking at the data file, the next step is to install an appropriate tool. For our case, we shall implement <b><a href = "https://www.bioinformatics.babraham.ac.uk/projects/fastqc/" > FASTQC </a></b> for summarizing the read quality of the fastq file, and analyze other statistics. For a quick look on installing a tool in the local distribution of galaxy, please follow the link <a href = "http://shauryajauhari.github.io/installing_tools_in_galaxy/" > here </a>.</p>


<p> When the tool is successfully installed, it can be traced with a local search.</p>
<p align="left">
  <img width="500" src="/assets/img/fastqcTraced.png">
</p>
<br>

<p>On selecting the tool, the interface opens in the main panel of galaxy and the user is presented with a choice to select data for application. Before execution, we can choose the associated parameters just as we would specify in the command line. For now, we shall stick to the defaults.</p>

<p align="left">
  <img width="500" src="/assets/img/beforeExecution.png">
</p>
<br>

<p>When the job is submitted, the intermediary progress is denoted by an <i>bisque</i> tone in the right panel where the task has been highlighted. On completion, it turns to smooth green. </p>

<p align="left">
  <img width="500" src="/assets/img/jobSubmitted.png">
</p>
<br>


<p align="left">
  <img width="500" src="/assets/img/jobDone.png">
</p>
<br>

<h3> Results </h3>

<p> The results are available as raw data (text file) and a formatted HTML visualization file. While both the formats can be downloaded, via the specific icon link, the former could be visualized in the galaxy interface. The latter has to be explicitly opened in a web-browser to peruse.</p>

<p align="left">
  <img width="500" src="/assets/img/rawDataResults.png">
</p>
<br>


<p align="left">
  <img width="500" src="/assets/img/downloadHTML.png">
</p>
<br>

<p> An archive file will be available for download, expanding which we get access to the result data. The HTML results file holds summary plots from FASTQC. Let us review a few of them here.</p><br>


<h4>Per Base Sequence Quality  </h4>

<p align="left">
  <img width="500" src="/assets/img/perBaseSequenceQuality.png">
</p>
<br>







