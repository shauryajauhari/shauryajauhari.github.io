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

<p> DNA Methylation is essentially a epigenetic mechanism to orchestrate genes' expression in a cell. As the name suggests, it refers to the addition of a methyl (CH<sub>3</sub>) group to DNA nucleotides. This effect has various renditions and could be attributed to the normal or a tweaked phenotype. The most venerable methylation phenomena is the covalent addition of the methyl group at the 5-carbon of the cytosine ring resulting in 5-methylcytosine (5-mC), effectively inhibiting transcription. Contrarily, there is <i> DNA demethylation </i> that is the removal of methyl group from the DNA. This process too has some pertinent effects. A brief perusal of the topic could be found <a href= "https://github.com/rajnijauhari/Mora_Lab_Data/blob/master/Methylation_ppt.pptx" > here </a>. In the current exercise, we shall be handling bisulphite sequencing data. <a href = "https://en.wikipedia.org/wiki/Bisulfite_sequencing" > <b>Bisulphite sequencing</b> </a> is the treatment of DNA before the routine sequencing tasks. </p>


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

<ul>
<li><i>Load reference genome:</i> <b> Local cache </b></li>
<li><i>Using reference genome: </i> <b> hg38</b></li>
<li><i>sorted_alignments.bam:</i> <b>the computed bam file of step 4 of the bwameth alignment.</b></li>
<li><i>What do you want to do?:</i> <b>Extract methylation metrics from an alignment file in BAM/CRAN format.</b></li>
<li><i>Merge per-Cytosine metrics from CpG and CHG contexts into per-CPG or per-CHG metrics :</i> <b>Yes</b></li>
<li><i>Extract fractional methylation (only) at each position. This is mutually exclusive with --counts, --logit, and --methylKit :</i> <b>Yes</b></li>
<li><i>All other options use the default value.</i></li>
</ul>

<p> Finally, we have a <i>bedgraph</i> file that we can visualize. </p>

<br>
<p align="center">
  <img width="200" height="250" src="/assets/img/pileomethOutputForPlot.png">
</p>
<br>

<h2> Visualization </h2>

<p align="justify"> Here, we are going to visualize methylation profiles around all <i> Transcription Start-Sites (TSS)</i> of our data. (<b>Note:</b> DNA methylation at gene promoters usually represses the gene functioning). Please be watchful that the previous output might not be reflected as the input to the next tool we're going to use. To ensure it does, change the attributes of the file to match- first, the datatype being <b>bedgraph</b>, and second, the database/ build being <b> Human Dec. 2013 (GRCh38/hg38) (hg38) </b>. To proceed install the tool <b> Wig/BedGraph-to-bigWig converter </b> from the repository <b> ucsc-wigtobigwig </b> and convert the <i>bedgraph</i> format to <i>bigwig</i>. </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/changeAttributes.png">
</p>
<br>

<p align="justify"> Next, we shall load the file <i>CpGIslands.bed</i> from the <a href= "https://zenodo.org/record/557099"> source </a> and install <b> deeptools_compute_matrix </b> and <b> deeptools_plot_profile </b>. Use the following values for parameters and leave the rest as default. <b><i>(P.S. The indexing of files might be inconsistent, as shown in the screenshots, as local and main Galaxy instances were used interchangeably as per accessibility.)</i></b> </p>

<br>
<p align="center">
  <img width="500" src="/assets/img/computeMatrixOptions.png">
</p>
<br>

Next, 

<br>
<p align="center">
  <img width="500" src="/assets/img/plotProfileOptions.png">
</p>
<br>


The final output looks like this. Note that the buffer regions of 1Kb on either side of the TSS can be manipulated as per the requirement.

<br>
<p align="center">
  <img width="500" src="/assets/img/plotProfileOutput.png">
</p>
<br>

<br>
<font color="#800080" >
<p><b>Exercise</b></p>
<ol>
<li> There are several other <i>bedgraph</i> files available <a href= "https://zenodo.org/record/557099"> here </a>. Choose anyone and repeat the same protocol of visualization. Analyze the results. </li> 
</ol>
</font>


<h2> Differentially Methylated Regions </h2>

<p align="justify"> Another flavor of this analysis, and arguably more purposeful, is the elicitation of differentially methylated regions, that could possibly map the variegated methylation states. For the same, we shall use the tool <b> metilene </b>. More information on the tool is available <a href = "https://www.bioinf.uni-leipzig.de/Software/metilene/" > here </a>.</p>

<p> Install the said tool from the <a href = " https://toolshed.g2.bx.psu.edu/" > tool shed </a>, download the following files from the repository mentioned previously, and upload them to the local Galaxy instance.
<ul>
<li> <i> NB1_CpG.meth.bedGraph </i> </li>
<li> <i> NB2_CpG.meth.bedGraph </i> </li>
<li> <i> BT198_CpG.meth.bedGraph </i> </li>
</ul>
</p>

<p align="justify"><i> <b>Note:</b> Make sure that these files have appropriate datatypes, else the tool will not recognize them. </i></p>

<br>
<p align="center">
  <img width="900" src="/assets/img/metileneOptions.png">
</p>
<br>


<h2> References </h2>
<ol>
<li> Lin, I.-H., D.-T. Chen, Y.-F. Chang, Y.-L. Lee, C.-H. Su et al., 2015 Hierarchical Clustering of Breast Cancer Methylomes Revealed Differentially Methylated and Expressed Breast Cancer Genes (O. El-Maarri, Ed.). PLOS ONE 10: e0118453. 10.1371/journal.pone.0118453 </li>
<li> Joachim Wolff, Devon Ryan, 2020 DNA Methylation data analysis (Galaxy Training Materials). /training-material/topics/epigenetics/tutorials/methylation-seq/tutorial.html Online; accessed Tue Jul 28 2020 </li>
<li> Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012 </li>
</ol>