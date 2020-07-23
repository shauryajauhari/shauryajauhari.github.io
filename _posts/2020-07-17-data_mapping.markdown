---
layout: post
title: Mapping Data
date: 2020-07-17 17:22:19 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: compass.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [ChIP-Seq, DNA Methylation]
---

<p> The mammoth data that deluges the bioinformatics domain could be majorly attributed to the next-generation sequencing experiments. Often times, it is required to elucidate the genomic source of the sequencing data. Although the species is known, we might still be interested to know which part of the genome is being represented by the sequenced reads. That will possibly enlighten us on say, the genes that are expressed in a particular phenotype. Broadly, mapping the reads to the <b><i>reference genome</i></b> is the process of <b><i>data mapping</i></b>.</p>

<p> Hypothetically, we need a <a href = "https://blast.ncbi.nlm.nih.gov/Blast.cgi" > BLAST analysis </a>, an endeavor of aligning each of millions of reads to a 3-million-nucleotide sequence. This will take some time. For the purposes of this tutorial, we shall use the <a href = "http://bowtie-bio.sourceforge.net/bowtie2/index.shtml" > Bowtie2 mapper </a> and the <a href = "https://igv.org/" > Integrative Genomics Viewer (IGV) </a> to explore the matadata for the read sequences.</p>

<p> For this tutorial, let us create a new session(history) and follow the steps below. </p>

<p align="center">
  <img width="500" src="/assets/img/mvHistory.png">
</p>
<br>

<h2>Loading Sequencing Data</h2>

<p> An impression for loading data to a local galaxy instance can be found in the initial part of this <a href = "https://shauryajauhari.github.io/quality_control/" > tutorial </a>. You could follow the for the following data. </p>

<ol>
<li> <i> https://zenodo.org/record/1324070/files/wt_H3K4me3_read1.fastq.gz </i> </li>
<li> <i> https://zenodo.org/record/1324070/files/wt_H3K4me3_read2.fastq.gz </i> </li>
</ol>

<p> As noted, the data could be manually downloaded from the website and then loaded to the galaxy instance, or the galaxy interface provides for the direct download as well. After the files, have been loaded we shall rename these paired-end files, again, as <i> reads_1 </i> and <i> reads_2 </i>. This is the kind of data we would usually get, directly from a sequencing facility, and might be prone to standard errors of quality. Anew, the aforementined <a href = "https://shauryajauhari.github.io/quality_control/" > tutorial </a> can be referred for rectifying quality issues. We won't get into the ways of mitigating quality setbacks, and join back here right after. </p>

<p> Your History Panel should probably look like this by now. </p>

<p align="center">
  <img width="200" height="200" src="/assets/img/historyPanel.png">
</p>
<br>

<span style="color:#800080" >
<p><b>Exercise</b></p>
<ol>
<li> Run quality control measures as illustrated in the other tutorial on the paried-end reads. </li>
</ol>
</span>


<h2>Mapping data to the <i><b>Reference Genome</b></i></h2>

<p>Let us begin by reflecting on the meaning of a <i>Reference Genome</i>. It is a sequence of nucleotides (bases/ base-pairs) that acts as a template for a representative species. Every individual will have a unique genopme assembly, and so a reference genome is usually a <i>chimera</i>; henceforth it does not accord to a single organism. As the sequencing technologies advance and we further in precision and lower costs, we are tempted to sequence more individuals from a speices to enhance our biological understanding as well. This engenders us having different versions of genomes, eg. hg19, hg38 versions of the Homo sapiens, etc.</p>

<p> For using <i>Bowtie2</i>, the first step will be to install it into the galaxy instance. Let us again go back to the tutorial enlisted <a href = "http://shauryajauhari.github.io/installing_tools_in_galaxy/" > here </a> and do that first. </p>

<p> When the data and tool have been setup, we commence with the execution with the following paramaters.
<ul>
<li> <i>Paired-end</i>: Specifying both input files </li>
<li> <i>“Do you want to set paired-end options?”</i>: No </li>
<li> <i>“Will you select a reference genome from your history or use a built-in index?”</i>: Use a built-in genome index</li>
<li> <i>“Select reference genome”</i>: Mouse (Mus musculus): mm10</li>
<li> <i>“Select analysis mode”:</i> Default setting only</li>
<li> <i>“Save the bowtie2 mapping statistics to the history”</i>: Yes</li>
</ul>
</p>

<p> Before anything though, we are confronted with a problem. The reference genome is not available in the local galaxy.</p>

<p align="center">
  <img width="500" src="/assets/img/dataError.png">
</p>
<br>

<p> Why so? Because the forked version of the galaxy does not contain the "actual" data or tools, as these are completely left to the discretion of the user and so are not feasible to be accompanied with every instance of galaxy due to requirement and memory aspects. However, these can be made available by following certain protocols. </p>
<p> There is an option of the <a href = "https://wiki.galaxyproject.org/Admin/UseGalaxyRsync" > <i>rsync</i> utility </a> that allows a user to download data from the <a href = "https://usegalaxy.org/" > Main Galaxy </a>, however, a more recommended and contemporary way to load a reference genome into a local instance of galaxy, is to use <a href = "https://wiki.galaxyproject.org/Admin/Tools/DataManagers" > <b>Data Managers</b> </a>. These can be installed, just like any other tool, through an administrator profile. We'll focus on using data managers in this exercise. </p>

<p>There is also a possibility of manually uploading a genome file (.fa, .fasta), and then recalling it from session history to be used as the purported reference genome. There are two problems, albeit. First, it is not comforting to manually load reference genome and build indices for every tool that we want to use. It is just too time consuming and un-professional. We want a reference genome to be available to every tool and not just the current one. Also, an uploaded file is unique to a history. Second, the tools take a little extra time to process the external, reference genome file, as opposed to the ones that are already "build-in". Consider akin to this scenario the mobile apps that are automatically off-loaded from the system due to seldom usage. This aids memory management. Now, if you want them again, the system will download them back easily with "cached" indices. This is far efficient than installing the new ones.</p>

<p align="center">
  <img width="500" src="/assets/img/searchDataManagers.png">
</p>
<br>

<p> A particular data manager, <b><i>data_manager_fetch_genome_dbkeys_all_fasta</i></b>, is required to load genome into the local instance of galaxy. <i> P.S. You can seek this workshop <a href = "https://github.com/gvlproject/dagobah-training/blob/master/sessions/05-reference-genomes/ex1-reference-genomes.md" > page </a> for details. Also, bear in mind that the order of installation of the data managers is advised by the technical team of Galaxy. They recommend - retrieve fasta, index for samtools, index for picard, and then index for any other tools-in-use. Each step must be allowed to complete before proceeding. </i></p>

<p align="center">
  <img width="500" src="/assets/img/fetchGenomeDataManager.png">
</p>
<br>

<p> After successful installation, you can browse <b>Local Data</b> under <b>Admin</b> option of galaxy, and reach out to the installed data manager. Upon selecting, you'll have the option to select preloaded <i>dbkeys</i>. These can be traced in the <i>~/tool-data/shared/ucsc/builds.txt</i> file.</p>


<p align="center">
  <img width="500" src="/assets/img/adminLocalData.png">
</p>
<br>


<p align="center">
  <img width="500" src="/assets/img/dataManagerLink.png">
</p>
<br>

<p> The mouse genome version "mm10" is sourced from the UCSC. Select appropriate paramaters, as under. </p> 

<p>
<ul>
<li> <i>"DBKEY to assign to data": Type in <b>mm10</b> and select the known build from the search list results </i> </li>
<li> <i>"Choose the source for the reference genome": <b>UCSC</b> </i> </li>
<li> <i>"UCSC's DBKEY for source FASTA": <b>mm10</b></i> </li>
<li> <i><b>Leave the rest at default</b></i> </li>
</ul>
</p>

<br>
<p align="center">
  <img width="500" src="/assets/img/loadingMM10.png">
</p>
<br>


<p> We have the reference genome now, but still we won't be able to use it. The next step is to create specific indices for the prospective tools that we wish to deploy inside the native environment of the galaxy, so that the genome that we have installed can be referenced. Again, we shall install several other <i>data managers</i>, in the order as below.</p>

<p>
<ol>
<li> SAM indexer (Search term: <i> <b> data_manager_sam_fasta_index_builder </b> </i>) </li>
<li> Picard indexer (Search term: <i> <b> data_manager_picard_index_builder </b> </i>) </li>
<li> 2bit (twoBit) indexer (Search term: <i> <b> data_manager_twobit_builder </b> </i>) </li>
</ol>
</p>


<p> These were generic indices. Now for our scenario, we would like to have the bowtie2-indexer installed. It's search term for the tool shed is <i><b> data_manager_bowtie2_index_builder </b></i>. Let's examine if that worked. </p>



