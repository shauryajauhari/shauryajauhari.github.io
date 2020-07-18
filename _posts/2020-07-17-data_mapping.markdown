---
layout: post
title: Mapping Data
date: 2020-07-17 17:22:19 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [ChIP-Seq, DNA Methylation]
---

<p> The mammoth data that deluges the bioinformatics domain can be sourced from the next-generation sequencing experiments. Often times, it is required to elucidate the source of the sequencing data. Although the species is known, we might still be interested to know which part of the genome is being represented by the reads. That will possibly enlighten us on say, the genes that are expressed in a particular phenotype. Broadly, mapping the sequenced reads to the <b><i>reference genome</i></b> is the process of <b><i>data mapping</i></b>.</p>

<p> Hypothetically, we need a <a href = "https://blast.ncbi.nlm.nih.gov/Blast.cgi" > BLAST analysis </a>, an endeavor of aligning each of millions of reads to a 3-million-nucleotide sequence. This will take some time. For the purposes of this tutorial, we shall use the <a href = "http://bowtie-bio.sourceforge.net/bowtie2/index.shtml" > Bowtie2 mapper </a> and the <a href = "https://igv.org/" > Integrative Genomics Viewer (IGV) </a> to explore the matadata for the read sequences.</p>

<h2>Loading Sequencing Data</h2>

<p> An impression for loading data to a local galaxy instance can be found in the initial part of this <a href = "https://shauryajauhari.github.io/quality_control/" > tutorial </a>. You could follow the for the following data. </p>

<ol>
<li> <i> https://zenodo.org/record/1324070/files/wt_H3K4me3_read1.fastq.gz </i> </li>
<li> <i> https://zenodo.org/record/1324070/files/wt_H3K4me3_read2.fastq.gz </i> </li>
</ol>

<p> As noted, the data could be manually downloaded from the website and then loaded to the galaxy instance, or the galaxy interface provides for the direct download as well.</p>