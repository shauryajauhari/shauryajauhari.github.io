---
layout: post
title: Multiple Aligned Reads
date: 2018-07-25 13:32:20 +0300
description: You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. # Add post description (optional)
img: multipleReads.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Genomics]
---
This has been a burning issue with high throughput genomic data analysts and enthusiasts. I wouldn’t parse through the verticals and draw a comparative performance graph corresponding to variegated tools to carry out the aforementioned functioning; rather precisely serve THE protocol for one.

Bowtie has been the bread-n-butter alignment tool in practice. Ummm…let’s cut to the chase here. Follow these steps.
<ol>
<li> Align your reads to the reference genome (fasta sequence) sans -a option and including — no-discordant. What -a does is that it uniquely lists all reads that have aligned; even multiple times. In addition, we also don’t want non-discordant reads, i.e. to say that we have only concordant reads.</li>
<li> Next step is to frisk the resultant SAM file to filter the reads with “XS:i” tag. This tag is the hallmark of reads that have aligned to more than one loci in the reference genome. While every record in the SAM file will have a “AS:i” tag, not all will have the former.</li>
<li> Now you can employ awk command in UNIX, to filter $1 (read id) and $10 (read sequence) from the SAM file. To move an extra mile for the paired-end data, you can have even rows representing read 1 and odd representing read 2. You must have the same count in both cases. The ‘samtools flagstat’ and ‘bowtie summary’ also cross-validate your concern.</li>
<li> Voila, there you have it. These are your multiple aligned reads. </li>
</ol>

More on that later. See you around.
