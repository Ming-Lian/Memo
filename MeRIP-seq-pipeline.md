<a name="content">目录</a>

[Analysis pipeline for MeRIP-seq](#title)
- [比对参考基因组](#map)
	- [Tophat](#tophat)
	- [HISAT2](#hisat2)
- [Peak calling](#peak)
	- [MACS2](#macs2)
	- [HOMER](#homer)





<a name="title"><h1>Analysis pipeline for MeRIP-seq</h1></a>
---
![](/m6A_seq.jpg "MeRIP-seq")

<p align="center"><h3>Schematic diagram of the MeRIP-seq protocol</h3></p>

由于MeRIP-seq数据分析的原理与过程和ChIP-seq十分相似，所以这里略过前面的质控，简单说明比对和peak calling步骤，具体内容可以参考[**ChIP-seq分析流程**](https://github.com/Ming-Lian/Memo/blob/master/ChIP-seq-pipeline.md)

<a name="map"><h3>比对参考基因组</h3></a>
在 ChIP-seq 中一般用 BWA 或者 Bowtie 进行完全比对就可以了，但是在 MeRIP-seq 中，由于分析的 RNA ，那么就存在**可变剪切**，对于存在可变剪切的 mapping 用 **Tophat** 或者 Tophat 的升级工具 **HISAT2** 更合适

<a name="tophat"><h4>Tophat</h4></a>

```
# build reference index
## <1> build genome index
$ bowtie2-build  hg19.fa hg19
## <2> build transcriptome index
$ tophat -p 8 -G hg19.gtf --transcriptome-index=Ref/hg19/hg19_trans/know hg19

# mapping
$ tophat -p 8 --transcriptome-index=Ref/hg19/hg19_trans/know -o outdir hg19 reads1_1.fastq reads1_2.fastq
```

> - -p Number of threads to use
> - -G Supply TopHat with a set of gene model annotations and/or known transcripts, as a GTF 2.2 or GFF3 formatted file. 
> - --transcriptome-index TopHat should be first run with the -G/--GTF option together with the --transcriptome-index option pointing to a directory and a name prefix which will indicate where the transcriptome data files will be stored. Then subsequent TopHat runs using the same --transcriptome-index option value will directly use the transcriptome data created in the first run (no -G option needed after the first run). 
> - -o Sets the name of the directory in which TopHat will write all of its output

<a name="hisat2"><h4>HISAT2</h4></a>

```
# build reference index
##  using the python scripts included in the HISAT2 package, extract splice-site and exon information from the gene
annotation fle
$ extract_splice_sites.py chrX_data/genes/chrX.gtf >chrX.ss
$ extract_exons.py chrX_data/genes/chrX.gtf >chrX.exon
##  build a HISAT2 index
$ hisat2-build --ss chrX.ss --exon chrX.exon chrX_data/genome/chrX.fa chrX_tran

# mapping
$ hisat2 -p 10 --dta -x chrX_tran -1 reads1_1.fastq -2 reads1_2.fastq | samtools sort -@ 8 -O bam -o reads1.sort.bam 1>map.log 2>&1
```
`Usage: hisat2 [options]* -x <ht2-idx> {-1 <m1> -2 <m2> | -U <r>} [-S <sam>]`
> - -p Number of threads to use
> - --dta reports alignments tailored for transcript assemblers
> - -x Hisat2 index
> - -1 The 1st input fastq file of paired-end reads
> - -2 The 2nd input fastq file of paired-end reads
> - -S File for SAM output (default: stdout)

<a name="peak"><h3>Peak calling</h3></a>

<a name="macs2"><h4>MACS2</h4></a>

参考ChIP-seq分析流程中的[peak calling](https://github.com/Ming-Lian/Memo/blob/master/ChIP-seq-pipeline.md#peak-calling)过程

<a name="homer"><h4>HOMER</h4></a>


参考资料：

(1) Zhang C, Chen Y, Sun B, et al. m(6)A modulates haematopoietic stem and progenitor cell specification[J]. Nature, 2017, 549(7671):273.

(2) Pertea M, Kim D, Pertea G, et al. Transcript-level expression analysis of RNA-seq experiments with HISAT, StringTie, and Ballgown[J]. Nature Protocols, 2016, 11(9):1650. 

(2) [ChIP-seq-pipeline](https://github.com/Ming-Lian/Memo/blob/master/ChIP-seq-pipeline.md)
