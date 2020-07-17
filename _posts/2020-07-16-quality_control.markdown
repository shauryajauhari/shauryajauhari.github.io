---
layout: post
title: A primer on FASTQC and Cutadapt | Quality Control of Genomic Data in Galaxy
date: 2020-07-16 15:14:05 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: goodQuality.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [NGS, Seq-Data]
---

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


<h2> Visual Inspection of Results</h2>

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


<h3> Per Base Sequence Quality </h3>

<p> The sequence length inferred by the tool is 37. The following plot has the read-length defined in the x-axis and hence, each position for the base in the read. The y-axis represents the quality scores for each position, that are enlisted with box-plots (A fair description for box-plots is available <a href = "https://www.dummies.com/education/math/statistics/interpreting-box-plots/" > here </a>). A quality score is a metric for a base-call; <i> how confident is the sequencer is calling spade a spade</i>.</p>

<figure>
<p align="left">
  <img src="/assets/img/perBaseSequenceQuality.png" width="500" alt="" title="">
  <figcaption> <b>Figure 1.</b> Per Base Sequence Quality: A report from FASTQC </figcaption>
</p>
</figure>
<br>

<p>As seen above, the background of the graph is segemented into three distinct, yet intuitive, zones. The "green" zone is reminiscent of a good score (usually a score of 30 is considered an acceptable quantum). The "orange" and "red" zones depict average and poor qualities, respectively. It is also commonly noticed that the quality of the reads tapers at the end. This phenomena can be attributed to signal decay of phasing during a sequencing cycle. A better explanation can be seen <a href = "https://hbctraining.github.io/Intro-to-rnaseq-hpc-salmon/lessons/qc_fastqc_assessment.html" > here </a>.</p>


<h3> Per Sequence Quality Scores </h3>

<p>In contrast to the above plot, this graphic portrays the mean <a href = "https://www.phrap.com/phred/" > Phred Score </a>for the entire length of a read sequence, for all reads(x-axis), and showcases the number of reads with that score(y-axis). So, while Figure 1 examines a read individually, Figure 2 can be sourced to draw conclusions about the entire set of reads from a sequencing experiment.</p>


<figure>
<p align="left">
  <img src="/assets/img/perSequenceQualityScores.png" width="500" alt="" title="">
  <figcaption> <b>Figure 2.</b> Sequence Quality Scores: A report from FASTQC </figcaption>
</p>
</figure>
<br>


<h3> Per Base Sequence Content </h3>

<p>The following plot depicts the proportions of Adenine (A), Guanine (G), Thymine (T), and Cytosine (C) at each nucleotide position, across all reads in an input sequence. According to the <a href = "https://en.wikipedia.org/wiki/Chargaff%27s_rules" > Chargaff's rule </a>, the usual consequence is that all bases would be aggregately similar in number in a random read, as A always binds to T and G to C. In the current scenario, we find some jitter at the initial part of the read (5' side). This is majorly a technical bias, and can be dealt with by trimming an initial score of nucleotides from the start of the read.</p>


<figure>
<p align="left">
  <img src="/assets/img/perBaseSequenceContent.png" width="500" alt="" title="">
  <figcaption> <b>Figure 3.</b> Per Base Sequence Content: A report from FASTQC </figcaption>
</p>
</figure>
<br>


<h3> Per Sequence GC Content </h3>

<p>The multifaceted significance of the GC content in the genome is well known [1]. As remarked earlier, the theoretical adage is that the percentage of G and C bases shall be uniform for all reads. The following plot depicts the theoretical (blue) and the experimental (red) GC content distribution. The peak signifies the overall GC content in the underlying genome.</p>


<p><i>P.S. You would also note a warning icon for this and the previous analysis. This might mean some deviation in the expected results, but <b>not a failure</b>. Here, for example, the graph is slightly skewed on the left side and is narrowly higher than the theoretical normal.</i></p>


<figure>
<p align="left">
  <img src="/assets/img/perSequenceGC.png" width="500" alt="" title="">
  <figcaption> <b>Figure 4.</b> Per Sequence GC Content: A report from FASTQC </figcaption>
</p>
</figure>
<br>

<h2> Recasting the Reads </h2>

<p>Why do we need this? As reported in the section above, we need to rectify the probable abnormalities in the reads. Amongst others, it is required to:
<ol>
<li> Remove reads with low quality score and lengths. </li>
<li> Trim the front- and rear-fractions of the reads with disturbed nucleotide proportions. </li>
</ol></p>

<p>To accomplish these tasks, we shall employ <a href = "https://cutadapt.readthedocs.io/en/stable/" > Cutadapt</a>. This tool will allow us to remove <a href = "https://en.wikipedia.org/wiki/Adapter_(genetics)" > adapter sequences </a> in the reads, as well as implement other quality control measures. The results from <i>Cutadapt</i> are fairly comprehensive and easily interpretable.</p>

<p>Before proceeding, we'll have to install this tool in our galaxy instance. To do that please follow the protocol, as enlisted <a href = "http://shauryajauhari.github.io/installing_tools_in_galaxy/" > here </a>. Surely, galaxy will have no initial reference for the tool.</p>

<figure>
<p align="left">
  <img src="/assets/img/notFound.png" width="500" alt="" title="">
</p>
</figure>
<br>

Meanwhile ...

<figure>
<p align="left">
  <img src="/assets/img/meanwhile.png" width="500" alt="" title="">
</p>
</figure>
<br>

Done.

<figure>
<p align="left">
  <img src="/assets/img/done.png" width="500" alt="" title="">
</p>
</figure>
<br>

<p>Let us now execute Cutadapt with the following parameters:
<ul>
<li> <i>Single-end or Paired-end</i>: Single-end </li>
<li> <i>Minimum length</i>: 20 (Filter Options)</li>
<li> <i>Quality cutoff</i>: 20 (Read Modification Options)</li>
<li> <i>Report</i>: Yes (Output Options)</li>
</ul>
</p>


<p>When finished, download and check the results. </p>
<p align="left">
  <img width="500" src="/assets/img/cutadaptDone.png">
</p>
<br>


<p> The results show that the data has been pre-normalized and there were no adaptor sequences found (they were already trimmed). There are about 0.3% reads that were filtered that didn't abide by the quality index of 20.</p>

<p>When finished, download and check the results. </p>
<p align="left">
  <img width="700" src="/assets/img/cutadaptReport.png">
</p>
<br>


<span style="color:#800080" >
<p><b>Exercise</b></p>
<ol>
<li> Run Fastqc on the filtered data and examine the results. </li>
</ol>
</span>

<p> For illustration purposes, single-end data is a <i>not-so-bad</i> choice. Practically though, we are often confronted with the paired-end data. For both ends of a read sequence, a single-end data means that the sequence has been derived unidirectionally. Contrarily, for paired-end data, that sequence is derived bi-directionally. More condifence can be realized while working with paired-end data. We would encounter file names ending like _1 and _2 for sequence files for the same segment.</p>

<p align="center">
  <img width="700" src="/assets/img/singleEndpairedEnd.png">
</p>
<br>

<p> To work with the paired-end data, let us download the other file from the <a href= "https://zenodo.org/record/61771/files/GSM461178_untreat_paired_subset_2.fastq" > source </a>. As before, rename this file to <i>reads_2</i> for consistency and re-run the FASTQC for this data now. </p>

<span style="color:#800080" >
<p><b>Exercise</b></p>
<ol>
<li> Execute Fastqc on <i> reads_2 </i> and compare the results with those of <i>reads_1</i>. </li>
</ol>
</span>


<p> Now we shall re-run the Cutadapt tool with the paired-end reads, i.e. <i>reads_1</i> and <i>reads_2</i>. Following the similar strategy for parameters as above, for the single-end reads, the only difference will be that we shall select 'Paired-end', that will automatically bring up the option to select two files. </p>

<p align="center">
  <img width="700" src="/assets/img/pairedEndCutadapt.png">
</p>
<br>

The results are as follows:


<p align="center">
  <img width="700" src="/assets/img/cutadaptPairedEndReport.png">
</p>
<br>

<span style="color:#800080" >
<p><b>Exercise</b></p>
<ol>
<li> Compare the overall results of Cutadapt with those of <i>reads_1</i>. </li>
<li> Execute Cutadapt on the FASTQC output data for paired-end reads and analyze the results.</li>
</ol>
</span>


<h1> References </h1>

<ol>
<li> Marie Sémon, Dominique Mouchiroud, Laurent Duret, Relationship between gene expression and GC-content in mammals: statistical significance and biological relevance, Human Molecular Genetics, Volume 14, Issue 3, 1 February 2005, Pages 421–427, https://doi.org/10.1093/hmg/ddi038 </li>
</ol>