<a name="content"><h4>目录</h4></a>

- [Analysis pipeline for ChIP-seq](#analysis-pipeline-for-chip-seq)
    - [1. 参考基因组的准备](#prepare-ref)
    - [2. 建立参考基因组索引](#build-index)
    - [3. ChIP-seq数据获取](#get-data)
      - [SRA](#sra)
        - [数据下载](#download)
        - [格式转换](#format-trans)
      - [ENA](#ena)
    - [4. 质控](#QC)
    - [5. 比对参考基因组](#map)
    - [6. Peak calling](#peak-calling)
    	- [Peak calling 原理探究](#peak-principle)
    - [7. 可视化](#view)
      - [Viewing the peaks in IGV](#igv)
      - [Vizualisation with deeptools](#deeptools)
    - [8.Peaks注释](#peak-anno)
    	- [用基因组注释文件GFF/GTF注释peaks](#gff)
    	- [用R包ChIPpeakAnno注释peaks](#r-peaks)
    - [9. Motif 分析](#motif)



# Analysis pipeline for ChIP-seq 

Author：连明

12/24/2017 4:43 :25 PM 

![ChIP](https://assets.illumina.com/content/dam/illumina-marketing/images/techniques/web-graphic-enriched-dna-binding-sites-insets.jpg  "ChIP-seq")
<a name="prepare-ref"><h3>1. 参考基因组的准备</h3></a>

参考基因组可以从以下两个途径获取：

1. [**UCSC**](http://genome.ucsc.edu/): `Download` -> `Mouse genome` -> `Full datasets` -> `chromFa.tar.gz`

得到的是一个由多个染色体fasta文件组成的压缩文件，解压后需要合并成一个fasta文件，命令：
```
tar zxvf chromFa.tar.gz && cat *.fa >mm10.fa
```
2. [**ENSEMBL**](http://www.ensembl.org/index.html):`Download` -> `Download data via FTP` -> `FTP site` -> `../Homo_sapiens.GRCh38.dna.primary_assembly.fa.gz`

[返回目录](#content)

<a name="build-index"><h3>2. 建立参考基因组索引</h3></a>

```
bowtie2-build ~/Ref/mm10/mm10.fa ~/Ref/mm10/mm10 1>Ref/mm10/mm10.bwt_index.log 2>&1
```

[返回目录](#content)

<a name="get-data"><h3>3. ChIP-seq数据获取</h3></a>

可以从**SRA**上下载，也可以从**ENA**上下载。

<a name="sra"><h3>SRA</h3></a>
从SRA上下载的数据是用特定的压缩方法得到的压缩文件格式`sra`，下载后需要进行格式转换

<a name="download"><h4>数据下载</h4></a>

下载数据先要根据数据的`GEO id`到NCBI上获取该数据所对应的`SRP id`(sra project id)，然后根据`SRP id`到FTP上下载，例如如果已知数据的`GEO id`为<font color="red">GSE42466</font>,从NCBI的GEO数据库上找到它的`SRP id`为<font color="red">SRP017311</font>，则FTP地址为

ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByStudy/sra/SRP/**SRP017**/**SRP017311**/**SRR620$i**/**SRR620\$i.sra**

可以写一个循环来下载该数据集：
```
for ((i=204;i<=209;i++));
do
wget ftp://ftp-trace.ncbi.nlm.nih.gov/sra/sra-instant/reads/ByStudy/sra/SRP/SRP017/SRP017311/SRR620$i/SRR620$i.sra;
done
```
<a name="format-trans"><h4>格式转换</h4></a>

SRA格式有6~9倍的压缩了，比zip格式压缩的2~3倍高多了。将SRA格式转换为fastq格式，这里需要用到NCBI开发的**sratoolkit**中的**fastq-dump**命令
```
fastq-dump --split-3 -O ChIP_seq/ SRR***.sra 
```
`--split-3`参数可以将PE的sra文件解压后的fastq文件拆分成\*_1.fastq和*_2.fastq，由于本示例数据集是SE测序，不会进行拆分
#### ENA
从GEO数据可搜索中获得其所对应的SRA id，在EBI中直接搜索该id，然后就可以直接下载fastq文件了

[返回目录](#content)

<a name="QC"><h3>4. 质控</h3></a>

用`fastqc`查看质量
```
ls *.fastq | xargs fastqc -t 10 -o ChIP_seq/ 
```
用`cutadapt`进行QC，如果还没有安装cutadapt，可以通过以下方式安装：
```
conda install -c bioconda cutadapt
```
```
1. Single end
cutadapt  -a ADAPTER -q 20,20 -m 20 -o outfile_QC.fastq infile.fastq
2. Paired end
cutadapt  -a ADAPTER -A ADAPTER -q 20,20 -m 20 -o outfile_QC_1.fastq -p outfile_QC_2.fastq infile_1.fastq infile_2.fastq
```
> - -a ADAPTER          3' adapter to be removed
> - -A ADAPTER          3' adapter to be removed from second read in a pair.
> - -q [5'CUTOFF,]3'CUTOFF 
> - -m LENGTH           Discard reads shorter than LENGTH. Default: 0

可以写一个循环来处理：
```
ls *.fastq | while read i;
do 
i=`basename $i .fastq`;
cutadapt -q 20,20 -m 20 -o ChIP_seq/${i}_QC.fastq ChIP_seq/${i}.fastq;
done
```
[返回目录](#content)

<a name="map"><h3>5. 比对参考基因组</h3></a>

```
ls ChIP_seq/Rawdata/*QC.fastq | while read i;
do
i=`basename $i _QC.fastq`；
echo $i;
bowtie2 -p 10 --local -x Ref/mm10/mm10 -U ChIP_seq/Rawdata/${i}_QC.fastq | samtools sort -@ 8 -O bam -o ChIP_seq/Map/${i}.sorted.bam;
done 1>ChIP_seq/Map/map.log 2>&1
```

比对的统计信息保存在`map.log`中

bowtie2 参数
> - -p threads
> - --local local alignment
> - -x reference genome index
> - -U Files with unpaired reads

samtools 参数
> - -@ threads
> - -O Specify output format (SAM, BAM, CRAM)
> - -o Write final output to FILE rather than standard output

[返回目录](#content)

<a name="peak-calling"><h3>6. Peak calling</h3></a>

目前可用的peak calling工具很多，详见：http://wodaklab.org/nextgen/data/peakfinders.html
这一步我们使用`MACS2`，这是一个用python2.7写的工具，安装方法为：
> 下载安装anaconda2

```
wget -c -P basic_tool/ https://repo.continuum.io/archive/Anaconda2-5.0.1-Linux-x86_64.sh
sh Anaconda2-5.0.1-Linux-x86_64.sh
echo 'export PATH=../anaconda2/bin:$PATH' >>~/.bashrc
```

> 下载安装MACS2

```
1. 用源码安装
wget -c -P biosoft/ https://pypi.python.org/packages/9f/99/a8ac96b357f6b0a6f559fe0f5a81bcae12b98579551620ce07c5183aee2c/MACS2-2.1.1.20160309.tar.gz
cd biosoft  && tar zxvf MACS2-2.1.1.20160309.tar.gz
cd MACS2-2.1.1.20160309 && python setup.py install
echo 'export PATH=../MACS2-2.1.1.20160309/bin:$PATH' >>~/.bashrc
2. 用bioconda安装
conda install -c bioconda macs2
```

安装成功后就可以直接使用MACS2进行peak calling了，命令：

```
#  MACS首先的工作是要确定一个模型，这个模型最关键的参数就是峰宽d，这个d就是bw(band width)，而它的一半就是shiftsize，具体可以参阅后文提到的原理部分
macs2 callpeak -c controlFile.bam -t treatmentFile.bam -m 10 30 -p pvalue -f BAM -g gsize -B -n filename.preffix --outdir ChIP_seq/CallPeak 2>ChIP_seq/CallPeak/filename.macs2.log
```

> - -c Control file
> - -t Treatment file
> - -m Select the regions within MFOLD range of high-confidence enrichment ratio against background to build model.
> - -g Effective genome size. shortcuts:'hs' for human (2.7e9), 'mm' for mouse(1.87e9), 'ce' for C. elegans (9e7) and 'dm' for fruitfly (1.2e8).
> - -p P value cutoff
> - -f File format
> - -B Output a file in BEDGRAPH format to visualize the peak profiles in a genome browser. There will be one file for the treatment, and one for the control.

如果要进行循环处理，可以先准备一个如下格式的文本文件：

|Treatment SRA id | Treatment SRA name | Control SRA id | Control SRA name |
|:---------------:|:------------------:|:--------------:|:----------------:|


命令：

```
nohup cat ChIP_seq/CallPeak/ChIP_seq.pairs | while read i;
do
treat_id=`echo $i|perl -ane 'chomp;print $F[0]'`;
treat_name=`echo $i|perl -ane 'chomp;print $F[1]'`;
control_id=`echo $i|perl -ane 'chomp;print $F[2]'`;
control_name=`echo $i|perl -ane 'chomp;print $F[3]'`;
macs2 callpeak -c ChIP_seq/Map/${control_id}.sorted.bam -t ChIP_seq/Map/${treat_id}.sorted.bam -m 10 30 -p 1e-5 -f BAM -g mm -B -n $treat_name --outdir ChIP_seq/CallPeak/ 2>ChIP_seq/CallPeak/${treat_name}.macs2.log;
done &
```
<a name="peak-principle"><h4>Peak Calling 原理探究</h4></a>

具体**统计学原理**可以看这篇博客文章：https://www.plob.org/article/7227.html
具体**peak calling原理**可以看这篇文章：https://www.plob.org/article/3760.html
以下两张图很好的描述了peaks calling的过程：
(1) **Building a signal profile**
![](https://upload.plob.ybzhao.com/wp-content/uploads/2012/09/5573BC7503EC32571E73BCE99799CCF60A6F3905049E_410_646.png "Building a signal profile")
(2) **Peak calling**
![](https://upload.plob.ybzhao.com/wp-content/uploads/2012/09/C59D9143E91CA6ED15485810F18A63E69198D68D7D8E_500_649.jpg "Peak calling")

也许看看在peaks calling分析早期，别人是怎么做的，对它的原理的理解会有启发：[八年前的ChIP-seq怎么找peak](https://mp.weixin.qq.com/s/8IkYvALnMiqLRBmtKeehjw)

[返回目录](#content)

<a name="view"><h3>7. 可视化</h3></a>

<a name="igv"><h3>Viewing the peaks in IGV</h3></a>

在peak call步骤中，当给`macs2 callpeak`添加参数`-B`时会输出两个个**bedgraph**文件，其中保存着peak profile,分别为control和treat的peak profile，可以在genome browser上可视化peaks，可选择的genome browser：
> - **Interactive Genome Viewer ([IGV](http://software.broadinstitute.org/software/igv/))** 本地安装运行，避免了数据传输
> - **UCSC genome browser** 在线工具，必须有可用的参考基因组


<a name="deeptools"><h3>Vizualisation with deeptools</h3></a>

将bam文件转换成bw（[bigWig](http://genome.ucsc.edu/FAQ/FAQformat.html#format6.1))文件，需要用到[deeptools](http://deeptools.readthedocs.io/en/latest/)，这是一个用python编写的工具:

```
ls ChIP_seq/Map/*.bam | while read i;
do
sample=`basename $i .bam`;
samtools rmdup -s ChIP_seq/Map/${sample}.bam ChIP_seq/Map/${sample}.nodup.bam; # Remove the duplicated reads
samtools index -@ 10 ChIP_seq/Map/${sample}.nodup.bam ChIP_seq/Map/${sample}.nodup.bai; # Index the BAM file
bamCoverage -b ChIP_seq/Map/${sample}.nodup.bam -o ChIP_seq/Map/${sample}.bw;
done
```

bamCoverage 参数
> - -b BAM file
> -  --outFileFormat Output file type. Either "bigwig" or "bedgraph" (default: bigwig)
> - -o Output file name

得到的bw文件可用用IGV进行可视化

可以对每个sample分别画基因的TSS附近的profile和heatmap图，也可以整合所有的chipseq的bam文件，画基因的TSS附近的profile和heatmap图。首先要下载mm10基因组refseq注释数据，可以从ucsc的`table browser`上下载

```
computeMatrix reference-point -p 10 --referencePoint TSS -b 2000 -a 2000 -S ../*bw -R ~/annotation/CHIPseq/mm10/ucsc.refseq.bed --skipZeros -o tmp4.mat.gz
plotHeatmap -m tmp4.mat.gz -out tmp4.merge.png
plotProfile --dpi 720 -m tmp4.mat.gz -out tmp4.profile.pdf --plotFileFormat pdf --perGroup
plotHeatmap --dpi 720 -m tmp4.mat.gz -out tmp4.merge.pdf --plotFileFormat pdf
```

computeMatrix reference-point 参数
> - --referencePoint {TSS,TES,center}
> - -b Distance upstream of the reference-point selected
> - -a Distance downstream of the reference-point selected
> - -R Reference annotation file
> - -S bigWig file(**s**) containing the scores to be plotted
> - --skipZeros Whether regions with only scores of zero should be included or not
> - -out File name to save the gzipped matrix file needed by the "plotHeatmap" and "plotProfile" tools
> - --outFileSortedRegions BED file File name in which the regions are saved after skiping zeros or min/max threshold values

plotHeatmap 参数
> - -m Matrix file from the computeMatrix tool
> - -out File name to save the image to

plotProfile 参数
> - --dpi Set the DPI to save the figure. (default: 200)
> - -m  Matrix file from the computeMatrix tool
> - -out File name to save the image to.The file ending will be used to determine the image format. The available options are: "png", "eps", "pdf" and "svg", e.g., MyHeatmap.png.
> - --plotFileFormat 

![](http://mmbiz.qpic.cn/mmbiz_jpg/cZNhZQ6j4ww4xlWzDIUrCmKLrfHQI9r0tWbnocKg04ttR6K90wCfC5oekoOicxeqgp25JaocFdPfWyjm8hqrGTQ/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1 "peaks profile")

![](http://mmbiz.qpic.cn/mmbiz_jpg/cZNhZQ6j4ww4xlWzDIUrCmKLrfHQI9r00NyScMMuD7NpOKulFtfWNfZTSXF0ibjaMCPSmqf5aHPbBwxQVdMQSFg/640?wx_fmt=jpeg&wxfrom=5&wx_lazy=1 "peaks heatmap")

[返回目录](#content)

<a name="peak-anno"><h3>8.Peaks注释</h3></a>

经过前面的ChIP-seq测序数据处理的常规分析，我们已经成功的把测序仪下机数据变成了BED格式的peaks记录文件。所谓的peaks注释，就是想看看该peaks在基因组的哪一个区段，看看它们在各种基因组区域(基因上下游，5',3'端UTR，启动子，内含子，外显子，基因间区域，microRNA区域)分布情况，但是一般的peaks都有近万个，所以需要批量注释，如果脚本学的好，自己下载参考基因组的GFF注释文件，完全可以自己写一个。

- <a name="gff"><h4>用基因组注释文件GFF/GTF注释peaks</h4></a>

下载参考基因组的GFF注释文件，下载地址：ftp://ftp.ensembl.org/pub/release-91/gff3/mus_musculus/Mus_musculus.GRCm38.91.gff3.gz

使用BEDTools’ intersectBed注释peaks

```
bedtools intersect -wa -wb -a peaks.bed -b mm10.gff3 >ChIP_seq/CallPeak/peaks.anno.bed
```
> - -wa Write the original entry in A for each overlap
> - -wb Write the original entry in B for each overlap. Useful for knowing what A overlaps
> - -a BAM/BED/GFF/VCF file “A”
> - -b One or more BAM/BED/GFF/VCF file(s) “B”

注意：peaks.bed 和 mm10.gff3 的第一列的染色体写法是否一致，是`[1-22]|[XY]`还是`chr[1-22]|[XY]` ？如果不一致需要先统一：

```
# 将 chr[1-22]|[XY] 改成 [1-22]|[XY]
perl -ane 'chomp;$chr=substr($F[0],3,2);print "$F[0]\t$F[1]\t$F[2]\t$F[3]\t$F[4]\n" peaks.bed >peaks.convert.bed
```

查看peaks注释结果

```
cut -f8 peaks.anno.bed | sort | uniq -c

# 统计结果如下

#  30459 biological_region
#  2344 CDS
#    10 C_gene_segment
# 70534 chromosome
#  6181 exon
#   291 five_prime_UTR
# 27836 gene
#     2 gene_segment
# 22244 lnc_RNA
#     5 miRNA
# 76036 mRNA
#     5 ncRNA
#  4212 ncRNA_gene
#   491 pseudogene
#   401 pseudogenic_transcript
#     3 rRNA
#     2 snoRNA
#     3 snRNA
#  1546 three_prime_UTR
#   192 transcript
#     6 V_gene_segment
```

- <a name="r-peaks"><h4>用R包ChIPpeakAnno注释peaks</h4></a>

这里我们使用一个bioconductor包**ChIPpeakAnno**来做CHIP-seq的peaks注释，下面的包自带的示例：

```
#这个包使用起来非常简单，只需要把我们做好的peaks文件(GSM1278641XuMUTrep1BAF155_MUT.peaks.bed等等)
#用toGRanges或者import读进去，成一个GRanges对象即可

# 比较两个peaks文件的overlap
library(ChIPpeakAnno)
bed <- system.file("extdata", "MACS_output.bed", package="ChIPpeakAnno")
gr1 <- toGRanges(bed, format="BED", header=FALSE)
## one can also try import from rtracklayer
library(rtracklayer)
gr1.import <- import(bed, format="BED")
identical(start(gr1), start(gr1.import))
gr1[1:2]
gr1.import[1:2] #note the name slot is different from gr1
gff <- system.file("extdata", "GFF_peaks.gff", package="ChIPpeakAnno")
gr2 <- toGRanges(gff, format="GFF", header=FALSE, skip=3)
ol <- findOverlapsOfPeaks(gr1, gr2)
makeVennDiagram(ol)

# peaks注释
data(TSS.human.GRCh37) ## 主要是借助于这个GRanges对象来做注释，也可以用getAnnotation来获取其它GRanges对象来做注释
## featureType ： TSS, miRNA, Exon, 5'UTR, 3'UTR, transcript or Exon plus UTR
peaks=MUT_rep1_peaks
macs.anno <- annotatePeakInBatch(peaks, AnnotationData=TSS.human.GRCh37,
	output="overlapping", maxgap=5000L)
```

可以查看peaks都出现在基因结构的哪些位置上：

```
require(TxDb.Hsapiens.UCSC.hg19.knownGene)
aCR<-assignChromosomeRegion(peaks, nucleotideLevel=FALSE,
	precedence=c("Promoters", "immediateDownstream",
	"fiveUTRs", "threeUTRs",
	"Exons", "Introns"),
	TxDb=TxDb.Hsapiens.UCSC.hg19.knownGene)
barplot(aCR$percentage)
```

得到的结果类似下图
![](http://mmbiz.qpic.cn/mmbiz_png/cZNhZQ6j4wyIzYfgNaW0scLL1RqniaTLyWtjk1CLsaGfwgpnd3ch50AqKkdVPufK1Pic47EfyFDyv0coeWia5qjQg/640?wx_fmt=png&wxfrom=5&wx_lazy=1)

peaks注释也可以选择网页版工具：
> - [ChIPseek](http://chipseek.cgu.edu.tw/)
> - [GREAT](http://bejerano.stanford.edu/great/public/html/)

[返回目录](#content)

<a name="motif"><h3>9. Motif 分析</h3></a>

目前知名的motif搜寻工具可以参阅文献：https://biologydirect.biomedcentral.com/articles/10.1186/1745-6150-9-4

进行Motif分析，首先需要获取peaks区域所对应的序列，可以用`bedtools`进行序列提取

```
bedtools getfasta -fi input.fasta -bed input.bed -fo output.fasta
```

然后可以用[**RSAT**](http://www.rsat.eu/)（Regulatory Sequence Analysis Tools）来搜索motif: `NGS ChIP-seq` -> `peak-motifs`，设置合适的参数，然后在线运行

[返回目录](#content)




---
参考资料：

(1) [Hands-on introduction to ChIP-seq analysis - VIB Training](http://www.biologie.ens.fr/~mthomas/other/chip-seq-training/)

(2) [ChIP-seq实战分析 ](https://mp.weixin.qq.com/s/_A0rHldzEgVk7bgwt457qQ)

(3) [一篇文章学会ChIP-seq分析（上） ](https://mp.weixin.qq.com/s?__biz=MzAxMDkxODM1Ng==&mid=2247484370&idx=1&sn=3e29df3b621076bd1d33a8ec157858e5&chksm=9b484369ac3fca7f57ae2982917d671ca87d44d12c27abc5db8ecfc272a32f627fc11f8ca181&scene=21#wechat_redirect)

(4) [一篇文章学会ChIP-seq分析（下） ](https://mp.weixin.qq.com/s?__biz=MzAxMDkxODM1Ng==&mid=2247484372&idx=1&sn=30ad9c4c54f3967000af059eb7a38ace&chksm=9b48436fac3fca79dfcd6eb34cd18c7a7e4cca1564be198fe4b5f90460c467b28f4998761685&scene=21#wechat_redirect)
