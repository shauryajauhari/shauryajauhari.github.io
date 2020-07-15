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


<h4> Per Base Sequence Quality </h4>

<p> The sequence length inferred by the tool is 37. The following plot has the read-length defined in the x-axis and hence, each position for the base in the read. The y-axis represents the quality scores for each position, that are enlisted with box-plots (A fair description for box-plots is available <a href = "https://www.dummies.com/education/math/statistics/interpreting-box-plots/" > here </a>). A quality score is a metric for a base-call; <i> how confident is the sequencer is calling spade a spade</i>.</p>

<figure>
<p align="left">
  <img src="/assets/img/perBaseSequenceQuality.png" width="500" alt="" title="">
  <figcaption> Figure 1. Per Base Sequence Quality: A report from FASTQC </figcaption>
</p>
</figure>
<br>

<p>As seen above, the background of the graph is segemented into three distinct, yet intuitive, zones. The "green" zone is reminiscent of a good score (usually a score of 30 is considered an acceptable quantum). The "orange" and "red" zones depict average and poor qualities, respectively. It is also commonly noticed that the quality of the reads tapers at the end. This phenomena can be attributed to signal decay of phasing during a sequencing cycle. A better explanation can be seen <a href = "https://hbctraining.github.io/Intro-to-rnaseq-hpc-salmon/lessons/qc_fastqc_assessment.html" > here </a>.</p>


<h4> Per Sequence Quality Scores </h4>

<p>In contrast to the above plot, this graphic portrays the mean <a href = "https://www.phrap.com/phred/" > Phred Score </a>for the entire length of a read sequence, for all reads(x-axis), and showcases the number of reads with that score(y-axis). So, while Figure 1 examines a read individually, Figure 2 can be sourced to draw conclusions about the entire set of reads from a sequencing experiment.</p>


<figure>
<p align="left">
  <img src="/assets/img/perSequenceQualityScores.png" width="500" alt="" title="">
  <figcaption> Figure 2. Sequence Quality Scores: A report from FASTQC </figcaption>
</p>
</figure>
<br>


<h4> Per Base Sequence Content </h4>

<p></p>


<figure>
<p align="left">
  <img src="/assets/img/perBaseSequenceContent.png" width="500" alt="" title="">
  <figcaption> Figure 3. Per Base Sequence Content: A report from FASTQC </figcaption>
</p>
</figure>
<br>


<h4> Per Sequence GC Content </h4>

<p></p>


<figure>
<p align="left">
  <img src="/assets/img/perSequenceGC.png" width="500" alt="" title="">
  <figcaption> Figure 4. Per Sequence GC Content: A report from FASTQC </figcaption>
</p>
</figure>
<br>











