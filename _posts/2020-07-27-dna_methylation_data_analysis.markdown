---
layout: post
title: DNA Methylation Data Analysis
date: 2020-07-27 12:01:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: dnaMethylation.jpg # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Epigenetics]
---


<h2> Introduction </h2>

<p> DNA Methylation is essentially a epigenetic mechanism to orchestrate genes' expression in a cell. As the name suggests, it refers to the addition of a methyl (CH<sub>3</sub>) group to DNA nucleotides. This effect has various renditions and could be attributed to the normal or a tweaked phenotype. The most venerable methylation phenomena is the covalent addition of the methyl group at the 5-carbon of the cytosine ring resulting in 5-methylcytosine (5-mC), effectively inhibiting transcription. Contrarily, there is <i> DNA demethylation </i> that is the removal of methyl group from the DNA. This process too has some pertinent effects. A bried perusal of the topic could be found <a href= "https://github.com/rajnijauhari/Mora_Lab_Data/blob/master/Methylation_ppt.pptx" > here </a>. In the current exercise, we shall be handling bisulphite sequencing data. <a href = "https://en.wikipedia.org/wiki/Bisulfite_sequencing" > <b>Bisulphite sequencing</b> </a> is the treatment of DNA before the routine sequencing tasks. </p>


<br>
<figure>
<p align="center">
  <img width="500" src="/assets/img/bss.png">
</p>
<figcaption> <i>Credit: http://www.nxt-dx.com/epigenetics/bisulfite-sequencing/</i> </figcaption>
</figure>
<br>



<h2> Data </h2>

<p> This exercise is based on the study bt Lin et al. 2015 [1], the data for which is available <a href = "https://zenodo.org/record/557099#.Xx-kYR1S_ow" > here </a>. In consideration to the time for this workshop, the data will be a subset of the original data. But we get the due essence of the overall analysis. </p>

<h2> Tools </h2>

<p> We shall be ascertaining the quality of the data with <b>FASTQC</b>. A reckoner for the same is available <a href = "https://shauryajauhari.github.io/quality_control/" > here </a>. We shall also be using the <a href = "https://github.com/brentp/bwa-meth" > <b> bwameth </b> </a> for mapping the bisulphite-sequencing data against the reference genome. Further we shall use <b> MethylDackel </b>('pileometh' formerly) to elaborate on the methylation status. Also, a tutorial for installation of tools in Galaxy can be found <a href = "https://shauryajauhari.github.io/installing_tools_in_galaxy/" > here </a>. </p> 


<p> Let us download the files <i> subset_1.fastq </i> and <i> subset_2.fastq </i> from the link provided above and remove the file extension via renaming. </p>

<font color="#800080" >
<p><b>Exercise</b></p>
<ol>
<li> Run FASTQC on both the reads and examine the quality parameters. </li>
</ol>
</font>

<p> Next, we move towards aligning these paired-end reads to the reference genome. In this case we need to load the <i> Homo sapiens </i> genome version <b> hg38 </b>. Although, the genomes can be added to the local instance of the Galaxy (See <a href = "https://shauryajauhari.github.io/data_mapping/" > example </a>), should it require due to network or processing caveats, there is always an option to manually download the <a href = "http://hgdownload.cse.ucsc.edu/goldenPath/hg38/bigZips/" > sequence file </a> for the genome and add to the history, for further alignment processing. For a change of flavor, let us try the latter. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/bwamethRun.png">
</p>
<br>

<p align="justify"> Since the genome is manually added to the history, the indicies are not available. The <i>bwameth</i> run will go an extra mile to build indicies first and then complete the alignment task. This certainly takes longer than expected. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/bwamethOut.png">
</p>
<br>

<p align="justify"> After the successful execution, an alignment file (BAM) is delivered. We would surely like to explore the methylation features. MethylDackel comes to our rescue here.</p>

Select the options as below, leaving other parameters as-is, and execute the tool.

<br>
<p align="center">
  <img width="500" src="/assets/img/pileomethOptions.png">
</p>
<br>

<i>P.S. The alignment file has been renamed to "aligned_subset.bam" and re-loaded to the Galaxy instance. </i>
<p> The output will be four distinct plots that will depict CpG methylation percentage along the read length. Let us pick up one for the "Original Bottom Strand" for contemplation. </p>


<br>
<p align="center">
  <img width="200" height= "600" src="/assets/img/pileomethOutput.png">
</p>
<br>

<p> The figure shows almost symmetrical curves, with a slight pronounced jitter at the edges. If it is a concern, one could plan on trimming the ends of the reads considering appropriate positions. </p>


<br>
<p align="center">
  <img width="500" src="/assets/img/bottomStrandPlot.png">
</p>
<br>

<p> For plotting methylation levels, we will use <i> MethylDackel </i> again with the following input parameters. </p>


    Choose at the first option Load reference genome from the value: Local cache and for Using reference genome the value: hg38.
    Select for the option sorted_alignments.bam the computed bam file of step 4 of the bwameth alignment.
    Use for What do you want to do? the value Extract methylation metrics from an alignment file in BAM/CRAN format.
    Choose Yes for the option Merge per-Cytosine metrics from CpG and CHG contexts into per-CPG or per-CHG metrics.
    Set the parameter Extract fractional methylation (only) at each position. This is mutually exclusive with --counts, --logit, and --methylKit to Yes.
    All other options use the default value.


<p> Finally, we have a <i>bedgraph</i> file that we can visualize. </p>

<br>
<p align="center">
  <img width="200" height="250" src="/assets/img/pileomethOutputForPlot.png">
</p>
<br>

<h2> Visualization </h2>



<h2> References </h2>
<ol>
<li> Lin, I.-H., D.-T. Chen, Y.-F. Chang, Y.-L. Lee, C.-H. Su et al., 2015 Hierarchical Clustering of Breast Cancer Methylomes Revealed Differentially Methylated and Expressed Breast Cancer Genes (O. El-Maarri, Ed.). PLOS ONE 10: e0118453. 10.1371/journal.pone.0118453 </li>
<li> Joachim Wolff, Devon Ryan, 2020 DNA Methylation data analysis (Galaxy Training Materials). /training-material/topics/epigenetics/tutorials/methylation-seq/tutorial.html Online; accessed Tue Jul 28 2020 </li>
<li> Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012 </li>
</ol>