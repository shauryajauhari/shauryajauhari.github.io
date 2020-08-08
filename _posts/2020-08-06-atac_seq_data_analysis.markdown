---
layout: post
title: ATAC-Seq Data Analysis
date: 2020-08-06 20:31:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Bioinformatics, Epigenetics]
---


<h2> Introduction </h2>

<p align="justify"> To understand <b>A</b>ssay for <b>T</b>ransposase-<b>A</b>ccessible <b>C</b>hromatin using <b>seq</b>uencing (ATAC-Seq), let us take a moment to explore the spatial organization of the genome. The genome (circa 1.8 meters in length) is squished and squeezed inside a 6 micrometer (µm) nucleus. This follows that there is no chance that the DNA would stay linear in terms of layout. It will exhibit folds, twists, turns, and intersections (<i> What a messy piece of road; I would never want to drive over it! </i>). Imagine taking a length of loose cotton thread and fitting it in your trouser pocket. You'll know what I mean. </p>

<p align="justify"> With such a scenario, the interactions between distant genomic sections are bound to happen as they come in close contact. It is neither a predicament nor inadvertent, rather a programmed mechanism that is peculiar to each cell type. That is why a nerve cell functions differently than a muscle cell. The bottom line is that even though the genome is same throughout,the interactome is different for disparate cells, and hence the diversity in function and phenotype. This has been the key driver of the single-cell studies [1].</p>

<p align="justify"> It is clear that the landscape of the genome, seemingly random, is immaculately structured inside the nucleus. Then there are domains, subdomains, compartments, etc. [2], details of which are beyond the scope of this primer. But, let's get back to ATAC-Seq. Intuitively, the compaction of the DNA is on the utmost importance and there are several phases over which this mechanism is laid. At the base-level, the DNA is wrapped around the histone proteins (this fraction of DNA accounts for ~147 bases, called the nucleosome), and is only accessible when set free from the tangle. Broadly, strings of such wraps constitute a <i>chromatin</i> and the role of ATAC-Seq is to study accessibility of chromatin and hence examine regulators of gene expression. A fair description about this technology could be found <a href = "https://informatics.fas.harvard.edu/atac-seq-guidelines.html" > here </a>. ATAC-Seq is a preferred methodology when compared to the contemporaries as <a href = "https://en.wikipedia.org/wiki/FAIRE-Seq" > FAIRE-Seq </a> and <a href = "https://en.wikipedia.org/wiki/DNase-Seq" > DNase-Seq </a>, for its efficiency.</p>

<p align="justify"> The data is from a human cell line of purified CD4+ T cells, called GM12878 [3]. The original dataset had 2 x 200 million reads and would be too big to process in a training session, so we downsampled the original dataset to 200,000 randomly selected reads. We also added about 200,000 reads pairs that will map to chromosome 22 to have a good profile on this chromosome, similar to what you might get with a typical ATAC-Seq sample (2 x 20 million reads in original FASTQ). Furthermore, we want to compare the predicted open chromatin regions to the known binding sites of <a href = "https://en.wikipedia.org/wiki/CTCF" > CTCF </a>. It is used as a positive control for assessing if the ATAC-Seq experiment is good quality. Good ATAC-Seq data would have accessible regions both within and outside of TSS, for example, at some CTCF binding sites. For that reason, we will download binding sites of CTCF identified by ChIP in the same cell line from ENCODE (ENCSR000AKB, dataset ENCFF933NTR). </p>


<h2> Assimilating Data and Metadata</h2>

<p align="justify"> As a norm, we will create a new History (session) for this data analysis module. Further, we load the data from the following web-links. </p>

<ul>
<li><i> https://zenodo.org/record/3862793/files/ENCFF933NTR.bed.gz </i></li>
<li><i> https://zenodo.org/record/3862793/files/SRR891268_chr22_enriched_R1.fastq.gz </i></li>
<li><i> https://zenodo.org/record/3862793/files/SRR891268_chr22_enriched_R2.fastq.gz </i></li>
</ul>


<br>
<p align="center">
  <img width="200" height="300" src="/assets/img/atacSeqLoadData.png">
</p>
<br>


<p align="justify"> With the data successfully imported into Galaxy, we add a tag called <b>#SRR891268_R1</b> to the R1 file and a tag called <b>#SRR891268_R2</b> to the R2 file. Also, check that the datatype of the 2 FASTQ files is <b>fastqsanger.gz</b> and the peak file (ENCFF933NTR.bed.gz) is <b>encodepeak</b>. The procedures are illustrated below. </p>

<br>
<p align="center">
  <img width="250" height="300" src="/assets/img/atacSeqEditTag.png">
</p>
<br>

<br>
<p align="center">
  <img width="700" src="/assets/img/atacSeqChangeDatatype.png">
</p>
<br>

<p align="justify"> Next, we will obtain gene annotation (hg38) for chromosome 22 genes (names of transcripts and genomic positions) using the <a href = "https://genome.ucsc.edu/cgi-bin/hgTables" > UCSC Table Browser </a>. This step could be explicitly carried out and the results are imported to the <a href = "https://usegalaxy.org/" > Main Galaxy </a>. The results can eventually be imported to the local Galaxy. </p>

<br>
<p align="center">
  <img width="700" src="/assets/img/tableBrowserOptions1.png">
</p>
<br>

<br>
<p align="center">
  <img width="400" src="/assets/img/tableBrowserOptions2.png">
</p>
<br>

<br>
<p align="center">
  <img width="200" height="400" src="/assets/img/ucscTableBrowserProgress.png">
</p>
<br>


<p align="justify"> This table contains all the information but is <b>not in a BED format</b>. To transform it into BED format we will cut out the required columns and rearrange. We will use the <b>Cut</b> which is a default tool available in Galaxy. The following parameters must be used.</p>


<ul>
<li><i>“Cut columns”</i>: <b>c3,c5,c6,c13,c12,c4</b></li>
<li><i>“Delimited by”</i>: <b>Tab</b></li>
<li><i>“From”</i>: <b>UCSC Main on Human: wgEncodeGencodeBasicV31 (chr22:1-50,818,468)</b></li>
</ul>

<br>
<p align="center">
  <img width="600" src="/assets/img/cutOptions.png">
</p>
<br>

Examine the result for accuracy and rename as <b>chr22 genes</b>, and change the datatype to <b>bed</b>. Recall that we are particularly interested in Chromosome 22. 

<h2> Quality Control </h2>




<h2> References </h2>
<ol>
<li> Zheng, H., Xie, W. The role of 3D genome organization in development and cell differentiation. Nat Rev Mol Cell Biol 20, 535–550 (2019). https://doi.org/10.1038/s41580-019-0132-4 </li>
<li> Rowley, M. J., & Corces, V. G. (2018). Organizational principles of 3D genome architecture. Nature reviews. Genetics, 19(12), 789–800. https://doi.org/10.1038/s41576-018-0060-8  </li>
<li> Buenrostro, J. D., P. G. Giresi, L. C. Zaba, H. Y. Chang, and W. J. Greenleaf, 2013 Transposition of native chromatin for fast and sensitive epigenomic profiling of open chromatin, DNA-binding proteins and nucleosome position. Nature Methods 10: 1213–1218. 10.1038/nmeth.2688 </li>
<li> Lucille Delisle, Maria Doyle, Florian Heyl, 2020 ATAC-Seq data analysis (Galaxy Training Materials). /training-material/topics/epigenetics/tutorials/atac-seq/tutorial.html Online; accessed Sat Aug 08 2020 </li>
<li> Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012 </li>
</ol>