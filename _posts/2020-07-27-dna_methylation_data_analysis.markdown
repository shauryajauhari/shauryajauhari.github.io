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

<p> DNA Methylation is essentially a epigenetic mechanism to orchestrate genes' expression in a cell. As the name suggests, it refers to the addition of a methyl (CH<sub>3</sub>) group to DNA nucleotides. This effect has various renditions and could be attributed to the normal or a tweaked phenotype. The most venerable methylation phenomena is the covalent addition of the methyl group at the 5-carbon of the cytosine ring resulting in 5-methylcytosine (5-mC), effectively inhibiting transcription. Contrarily, there is <i> DNA demethylation </i> that is the removal of methyl group from the DNA. This process too has some pertinent effects. A bried perusal of the topic could be found <a href= "https://github.com/rajnijauhari/Mora_Lab_Data/blob/master/Methylation_ppt.pptx" > here </a>.</p>



<h2> Data </h2>

<p> This exercise is based on the study bt Lin et al. 2015 [1], the data for which is available <a href = "https://zenodo.org/record/557099#.Xx-kYR1S_ow" > here </a>. In consideration to the time for this workshop, the data will be a subset of the original data. But we will get the due essence of the overall analysis. </p>

<h2> Tools </h2>

<p> We shall be ascertaining the quality of the data with <b>FASTQC</b>. </p>



<p> We will download the files <i> subset_1.fastq </i> and <i> subset_2.fastq </i> from the link provided above. </p>

<h2> References </h2>
<ol>
<li> Lin, I.-H., D.-T. Chen, Y.-F. Chang, Y.-L. Lee, C.-H. Su et al., 2015 Hierarchical Clustering of Breast Cancer Methylomes Revealed Differentially Methylated and Expressed Breast Cancer Genes (O. El-Maarri, Ed.). PLOS ONE 10: e0118453. 10.1371/journal.pone.0118453 </li>
<li> Joachim Wolff, Devon Ryan, 2020 DNA Methylation data analysis (Galaxy Training Materials). /training-material/topics/epigenetics/tutorials/methylation-seq/tutorial.html Online; accessed Tue Jul 28 2020 </li>
<li> Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012 </li>
</ol>