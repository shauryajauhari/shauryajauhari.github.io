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

<p> As noted, the data could be manually downloaded from the website and then loaded to the galaxy instance, or the galaxy interface provides for the direct download as well. After the files, have been loaded we shall rename these paired-end files, again, as <i> reads_1 </i> and <i> reads_2 </i>. This is the kind of data we would usually get, directly from a sequencing facility, and might be prone to standard errors of quality. Anew, the aforementined <a href = "https://shauryajauhari.github.io/quality_control/" > tutorial </a> can be referred for rectifying quality issues. We won't get into the ways of mitigating quality setbacks, and join back here right after. </p>


<span style="color:#800080" >
<p><b>Exercise</b></p>
<ol>
<li> Run quality control measures as illustrated in the other tutorial on the paried-end reads. </li>
</ol>
</span>


<h2>Mapping data to the <i>Reference Genome</i></h2>

<p>Let us begin by the answering the meaning of a Reference Genome. It is a sequence of nucleotides (bases/ base-pairs) that acts as a template for a representative species. Every individual will have a unique genopme assembly, and so a reference genome is usually a <i>chimera</i>; henceforth it does not accord to a single organism. As the sequencing technologies advance and we further in precision and lower costs, we are tempted to sequence more individuals from a speices to enhance our biological understanding as well. This engenders us having different versions of genomes, eg. hg19, hg38 versions of the Homo sapiens, etc.</p>

<p> For using <i>Bowtie2<i>, the first step will be to install it into the galaxy instance. Let us again go back to the tutorial enlisted <a href = "http://shauryajauhari.github.io/installing_tools_in_galaxy/" > here </a> and do that first. </p>

