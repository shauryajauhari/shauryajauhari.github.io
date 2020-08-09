---
layout: post
title: ATAC-Seq Data Analysis
date: 2020-08-06 20:31:21 +0230
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: atacSeqIntro.jpg # Add image post (optional)
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


<p align="justify"> With the data successfully imported into Galaxy, we add a tag called <b>#SRR891268_R1</b> to the R1 file and a tag called <b>#SRR891268_R2</b> to the R2 file. (<b>Note: Tags</b> are extremely useful in flagging components that are part of a result from a tool. This could potentially be a <i>life-saver</i> when it comes to lengthy workflows, where it is hard to be track of, say, input data that was imported in the beginning of the pipeline). Also, check that the datatype of the 2 FASTQ files is <b>fastqsanger.gz</b> and the peak file (ENCFF933NTR.bed.gz) is <b>encodepeak</b>. The procedures are illustrated below. </p>

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
  <img width="225" height="400" src="/assets/img/ucscTableBrowserProgress.png">
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

<p align="justify"> As a foremost standard measure, a quality check ensures that the data is potent to delivery acceptable results. We shall now perform a run of <a href ="https://shauryajauhari.github.io/quality_control/" > <b>FASTQC</b> </a>, to examine the grade of reads and presence of <a href = "https://www.syntezza.com/product/nextera-adapters/" > adapter sequences</a>. Before the run, let us rename the files for convenience. Also, we could choose either of the files or both, by selecting <i>single-file</i> or <i>multiple-files</i> mode, respectively. </p>

<font color="#800080" >
<p><b>Exercise</b></p>
<ol>
<li> Examine the FASTQC results. </li>
</ol>
</font>

<h2> Trimming Reads </h2>

<p align="justify"> To trim the adapters we provide the Nextera adapter sequences to <a href = "https://cutadapt.readthedocs.io/" > <b>Cutadapt</b> </a> tool. The forward and reverse adapters are slightly different. We will also trim low quality bases at the ends of the reads (quality less than 20). We will only keep reads that are at least 20 bases long. We remove short reads (< 20bp) as they are not useful, they will either be thrown out by the mapping or may interfere with our results at the end. The following values to options shall be instantiated. </p>

<ul>
<li><i>“Single-end or Paired-end reads?”</i>: <b>Paired-end</b></li>
<li><i>“FASTQ/A file #1”</i>: <b>SRR891268_chr22_enriched_R1.fastq</b></li>
<li><i>“FASTQ/A file #2”</i>: <b>SRR891268_chr22_enriched_R2.fastq</b></li>
- In “Read 1 Options”:<br>
- In “3’ (End) Adapters”:<br>
- “Insert 3’ (End) Adapters”<br>
<li><i>“Source”</i>: <b> Enter custom sequence </b></li>
<li><i>“Enter custom 3’ adapter name (Optional if Multiple output is ‘No’)”</i>: <b> Nextera R1</b></li>
<li><i>“Enter custom 3’ adapter sequence”</i>: <b> CTGTCTCTTATACACATCTCCGAGCCCACGAGAC</b></li>
- In “Read 2 Options”:
- In “3’ (End) Adapters”:
- “Insert 3’ (End) Adapters”
<li><i>“Source”</i>: <b> Enter custom sequence</b></li>
<li><i>“Enter custom 3’ adapter name (Optional)”</i>: <b> Nextera R2</b></li>
<li><i>“Enter custom 3’ adapter sequence”</i>: <b> CTGTCTCTTATACACATCTGACGCTGCCGACGA</b></li>
- In “Filter Options”:
<li><i>“Minimum length”</i>: <b> 20</b></li>
- In “Read Modification Options”:
<li><i>“Quality cutoff”</i>: <b> 20</b></li>
- In “Output Options”:
<li><i>“Report”</i>: <b> Yes</b></li>
</ul>

We get approximately 14% reads with adapters.

<br>
<p align="center">
  <img width="400" src="/assets/img/cutadaptResult.png">
</p>
<br>


<p align="justify"> With the filtered reads, we run FASTQC again and analyze the results. It is to be noticed that the adapter content is completely removed from the reads. </p>



<h2> Mapping Reads to Reference Genome </h2>

<p align="justify"> <a href = "https://shauryajauhari.github.io/data_mapping/" > Mapping reads </a> to the reference genome aids to determine the genomic regions where the reads align. We shall now be using <a href = "http://bowtie-bio.sourceforge.net/bowtie2/index.shtml" > <b>Bowtie2</b> </a> with the following options.</p>

<ul>
<li><i>“Is this single or paired library”</i>: <b>Paired-end</b></li>
<li><i>“FASTQ/A file #1”</i>: <b>select the output of Cutadapt tool “Read 1 Output”</b></li>
<li><i>“FASTQ/A file #2”</i>: <b>select the output of Cutadapt tool “Read 2 Output”</b></li>
<li><i>“Do you want to set paired-end options?”</i>: <b>Yes</b></li>
<li><i>“Set the maximum fragment length for valid paired-end alignments”</i>: <b> 1000</b></li>
<li><i>“Allow mate dovetailing”</i>: <b> Yes</b></li>
<li><i>“Will you select a reference genome from your history or use a built-in index?”</i>: <b> Use a built-in genome index</b></li>
<li><i>“Select reference genome”: Human (Homo sapiens)</i>: <b> hg38 Canonical</b></li>
<li><i>“Select analysis mode”</i>: <b> 1: Default setting only</b></li>
<li><i>“Do you want to use presets?”</i>: <b> Very sensitive end-to-end (--very-sensitive)</b></li>
<li><i>“Save the bowtie2 mapping statistics to the history”</i>: <b> Yes</b></li>
</ul>

<p align="justify"> (<i>P.S. For justifications of the above choices, please visit the original tutorial; see [5]).</i> Also note that Bowtie2 considers a read as multi-mapped even if the second hit has a much lower quality than the first one. Another reason is that we have reads that map to the mitochondrial genome. The mitochondrial genome has a lot of regions with similar sequence. </p>

<br>
<p align="center">
  <img width="600" src="/assets/img/atacSeqBowtie2Results.png">
</p>
<br>


<h2> Filtering Mapped Reads </h2>

<p align="justify"> The vulnerability of ATAQ-Seq to the mitochondrial genome is high, because the mitochondrial genome is deprived of nucleosomes [4]. So, a wise choice is to remove these reads, alongwith reads with low quality and the ones that are not properly paired. For the same purpose, we use the tool <b>Filter</b> from the repository <b>bamtools_filter</b>, and mark the options as represented in the following screenshot.</p>

<br>
<p align="center">
  <img width="700" src="/assets/img/atacSeqFilterOptions.png">
</p>
<br>

<p align="justify"> You'll notice the size difference in the input (27.9 MB) and output (15.1 MB) BAM files from the tool. (<i><b>Note:</b> The tool <b>Samtools idxstats</b> could be used on the output of Bowtie2 tool (BAM file), to tabulate the number of reads that map to a paritcular chromosome</i>).</p>


<h2> Filter Duplicate Reads </h2>

<p align="justify"> Fundamentally, <a href = "https://www.ncbi.nlm.nih.gov/probe/docs/techpcr/" > Polymerase Chain Reaction (PCR) </a> has been designed to replicate DNA segments, and that could engender duplicacy in the pool of reads. This redundancy depicts different reads mapping exactly to the same genomic region. Such PCR duplicates are to be removed using <b>MarkDuplicates</b> tool, from the <b>picard</b> repository. </p>

Use the following parameters.

<ul>
<li><i>“Select SAM/BAM dataset or dataset collection”</i>: <b>Select the output of Filter tool “BAM”</b></li>
<li><i>“If true do not write duplicates to the output file instead of writing them with appropriate flags set”</i>: <b> Yes</b></li>
</ul>

<p align="justify"> The second parameter marked as "Yes" is the one that actually deletes the duplicates. If otherwise, the duplicates are only flagged. </p>

<br>
<p align="center">
  <img width="700" src="/assets/img/markDuplicatesResult.png">
</p>
<br>

<h2> Check Insert Sizes </h2>

<p align="justify">Next, we are going to check the <i>insert size</i>, i.e. <b>distance between paired-end reads (R1 and R2)</b>. This tells us the size of the DNA fragment, the read pairs came from. The fragment length distribution of a sample gives a very good indication of the quality of the ATAC-Seq. We shall be using <b>CollectInsertSizeMetrics</b> from the repository, <b>picard</b>. </p>

Try the following choices for paramaters. 

<ul>
<li><i>“Select SAM/BAM dataset or dataset collection”</i>: <b>Select the output of MarkDuplicates tool “BAM output”</b></li>
<li><i>“Load reference genome from”</i>: <b> Local cache</b></li>
<li><i>“Using reference genome”</i>: <b> Human Dec. 2013 (GRCh38/hg38) (hg38)</b></li>
</ul>

<br>
<figure>
<p align="left">
<img width="750" height="700" src="/assets/img/fragmentSizeDistribution.png">
<figcaption> <p align="justify"> <b>Figure 1: Fragment Size Distribution</b> <i> Simple put, a transposase is an enzyme that plucks the DNA and moves it to a different place. The above graphic shows, in descending order, the length of DNA fragments from an ATAC-Seq experiment. This implies that distribution of DNA lengths that are nucleosome-free, between two histone-wraps, between three histone-wraps, and so on (from right to left). </i></p> </figcaption>
</p>
</figure>
<br>


<p align="justify"> <b>Note:</b> The legends in the aforementioned graphic, <b>FR</b> stands for forward reverse orientation of the read pairs, meaning, your reads are oriented as -> <- so the first read is on the forward and the second on the reverse strand. <b>RF</b> stands for reverse forward oriented, i.e., <- ->.  </p>


<h2> Peak Calling </h2>

<p align="justify"> In this module, we commence with the post-processing of the samples. The first stage is <i>peak-calling</i> ; peaks are distinguished piles of reads. It is very important at this point that we center the reads on the 5’ extremity (read start site) as this is where Tn5 (the transposase) cuts. You want your peaks around the nucleosomes and not directly on the nucleosome. For this task, we shall be using <a href = "https://github.com/macs3-project/MACS" > <b>MACS2</b> </a>, from the repository <b>macs2</b>. The first requirement, however, is to convert BAM file to a BED file. Use <b>bedtools BAM to BED converter</b> from the repository <b>bedtools</b>. </p>

<br>
<p align="center">
<img width="600" src="/assets/img/bedtoolsBAMtoBED.png">
</p>
<br>

Now, we execute MACS2 callpeak with the following options:

<ul>
<li><i>“Are you pooling Treatment Files?”</i>: <b> No</b></li>
<li><i>“Do you have a Control File?”</i>: <b> No</b></li>
<li><i>“Format of Input Files”</i>: <b> Single-end BED</b></li>
<li><i>“Effective genome size”</i>: <b> H. sapiens (2.7e9)</b></li>
<li><i>“Build Model”</i>: <b> Do not build the shifting model (--nomodel)</b></li>
<li><i>“Set extension size”</i>: <b> 100</b></li>
<li><i>“Set shift size”</i>: <b> -50</b></li>
- “Additional Outputs”:
<li><b>Check Peaks as tabular file</b></li>
<li><b>Check Peak summits</b></li>
<li><b>Check Scores in bedGraph files</b></li>
- In “Advanced Options”:
<li><i>“Composite broad regions”</i>: <b> No broad regions</b></li>
<li><i>“Use a more sophisticated signal processing approach to find subpeak summits in each enriched peak region”</i>: <b> Yes</b></li>
<li><i>“How many duplicate tags at the exact same location are allowed?”</i>: <b> all</b></li>
</ul>
<br>

<p align="justify"> Also, add a tag called <b>#MACS2_cov</b> to the output called <i>MACS2 callpeak …(Bedgraph Treatment)</i>. </p>


<h2> Visualization of Coverage </h2>

<h3> Convert to Bigwig </h3>

<p align="justify">To make the output file valid for downstream use, we first convert it to <a href="https://software.broadinstitute.org/software/igv/bigwig" > bigwig </a> format. We use the tool <b>Wig/BedGraph-to-bigWig converter</b>. </p>

<br>
<p align="center">
<img width="600" src="/assets/img/bedgraphToBigwigOptions.png">
</p>
<br>

Rename the output file to <i>MACS bigwig</i>.

<h3> Sort CTCF Peaks </h3>

<p align="justify"> We can use several exploratory tools to visualize specific genomic regions; a genome browser like <a href = "http://software.broadinstitute.org/software/igv/" > IGV </a> or <a href = "https://genome.ucsc.edu/" > UCSC Browser </a>, or choose <a href = "https://github.com/deeptools/pyGenomeTracks" > pyGenomeTracks </a> to make graphics. In the module, we employ <b>pyGenomeTracks</b>. <b> The pyGenomeTracks tool needs all BED files sorted </b>, thus we sort the CTCF (our protein of interest, that binds to the open chromatin) peaks. </p>

<br>
<p align="center">
<img width="600" src="/assets/img/bedtoolsSortbedOptions.png">
</p>
<br>

<h3> Create heatmap of coverage at TSS with deepTools </h3>

<h4> computeMatrix </h4>
 
 The output of this function is a pre-requisite to the <i>plotHeatmap</i> function. It delivers a matrix with features to plot.

 Input the following values of parameters in <i><b>computeMatrix</b></i>.

<ul>
- In “Select regions”:
<li>- “Select regions”</li>
<li><i>“Regions to plot”</i> : <b>chr22 genes</b></li>
<li><i>“Sample order matters”</i> : <b>No</b></li>
<li><i>“Score file”</i> : <b>MACS2 bigwig</b></li>
<li><i>“computeMatrix has two main output options”</i> : <b>reference-point</b></li>
<li><i>“The reference point for the plotting”</i> : <b>beginning of region (e.g. TSS)</b></li>
<li><i>“Show advanced output settings”</i> : <b>no</b></li>
<li><i>“Show advanced options”</i> : <b>yes</b></li>
<li><i>“Convert missing values to 0?”</i> : <b>yes</b></li>
</ul>



<h4> plotProfile </h4>

<p align="justify"> This visualization gives the mean coverage around the TSS. </p>

<br>
<p align="center">
<img width="600" src="/assets/img/atacSeqPlotProfileOptions.png">
</p>
<br>

<br>
<p align="center">
<img width="600" src="/assets/img/atacSeqPlotProfileResult.png">
</p>
<br>


<h4> plotHeatmap </h4>

<p align="justify"> This function scales the output of the <i>plotProfile</i> with a heatmap. Each line will be a transcript (instances from <i>chr22 genes</i>). The coverage will be summarized with a color code from red (no coverage) to blue (maximum coverage). All TSS will be aligned in the middle of the figure and only the 2 kb around the TSS will be displayed. Another plot, on top of the heatmap, will show the <b>mean signal at the TSS</b>. </p>

<br>
<p align="center">
<img width="600" src="/assets/img/atacSeqPlotHeatmapResult.png">
</p>
<br>


<h3> Visualise Regions with pyGenomeTracks </h3>

Load the tool and instantiate the following constraints.

<ul>
<li><i>“Region of the genome to limit the operation”</i>: <b>chr22:37,193,000-37,252,000</b></li>
- In “Include tracks in your plot”:
<li>“1. Include tracks in your plot”</li>
<li><i>“Choose style of the track”</i>: <b> Bigwig track</b></li>
<li><i>“Plot title”</i>: <b> Coverage from MACS2 (extended +/-50bp)</b></li>
<li><i>“Track file bigwig format”</i>: <b> MACS2 bigwig.</b></li>
<li><i>“Color of track”</i>: <b> Select the color of your choice</b></li>
<li><i>“Minimum value”</i>: <b> 0</b></li>
<li><i>“height”</i>: <b> 5</b></li>
<li><i>“Show visualization of data range”</i>: <b> Yes</b></li>
<br>
- “Insert Include tracks in your plot”
<li><i>“Choose style of the track”</i>: <b> NarrowPeak track</b></li>
<li><i>“Plot title”</i>: <b> Peaks from MACS2 (extended +/-50bp)</b></li>
<li><i>“Track file bed format”</i>: <b> MACS2 callpeak(narrow Peaks)</b></li>
<li><i>“Color of track”</i>: <b> Select the color of your choice</b></li>
<li><i>“display to use”</i>: <b> box: Draw a box</b></li>
<li><i>“Plot labels (name, p-val, q-val)”</i>: <b> No</b></li>
<br>
- “Insert Include tracks in your plot”
<li><i>“Choose style of the track”</i>: <b> Gene track / Bed track</b></li>
<li><i>“Plot title”</i>: <b> Genes</b></li>
<li><i>“Track file bed format”</i>: <b> chr22 genes</b></li>
<li><i>“Color of track”</i>: <b> Select the color of your choice</b></li>
<li><i>“height”</i>: <b> 5</b></li>
<li><i>“Put all labels inside the plotted region”</i>: <b> Yes</b></li>
<li><i>“Allow to put labels in the right margin”</i>: <b> Yes</b></li>
<br>        
- “Insert Include tracks in your plot”
<li><i>“Choose style of the track”</i>: <b> NarrowPeak track</b></li>
<li><i>“Plot title”</i>: <b> CTCF peaks</b></li>
<li><i>“Track file bed format”</i>: <b> Select the dataset bedtools SortBED of ENCFF933NTR.bed</b></li>
<li><i>“Color of track”</i>: <b> Select the color of your choice</b></li>
<li><i>“display to use”</i>: <b> box: Draw a box</b></li>
<li><i>“Plot labels (name, p-val, q-val)”</i>: <b> No</b></li>
</ul>

We realize something like this.

<br>
<p align="center">
<img width="900" src="/assets/img/atacSeqMACSpyGenomeTracks.png">
</p>
<br>

<h2> References </h2>
<ol>
<li> Zheng, H., Xie, W. The role of 3D genome organization in development and cell differentiation. Nat Rev Mol Cell Biol 20, 535–550 (2019). https://doi.org/10.1038/s41580-019-0132-4 </li>
<li> Rowley, M. J., & Corces, V. G. (2018). Organizational principles of 3D genome architecture. Nature reviews. Genetics, 19(12), 789–800. https://doi.org/10.1038/s41576-018-0060-8  </li>
<li> Buenrostro, J. D., P. G. Giresi, L. C. Zaba, H. Y. Chang, and W. J. Greenleaf, 2013 Transposition of native chromatin for fast and sensitive epigenomic profiling of open chromatin, DNA-binding proteins and nucleosome position. Nature Methods 10: 1213–1218. 10.1038/nmeth.2688 </li>
<li> Taanman, J.-W. (1999). The mitochondrial genome: structure, transcription, translation and replication. Biochimica et Biophysica Acta (BBA) - Bioenergetics, 1410(2), 103–123. https://doi.org/https://doi.org/10.1016/S0005-2728(98)00161-3 </li>
<li> Lucille Delisle, Maria Doyle, Florian Heyl, 2020 ATAC-Seq data analysis (Galaxy Training Materials). /training-material/topics/epigenetics/tutorials/atac-seq/tutorial.html Online; accessed Sat Aug 08 2020 </li>
<li> Batut et al., 2018 Community-Driven Data Analysis Training for Biology Cell Systems 10.1016/j.cels.2018.05.012 </li>
</ol>