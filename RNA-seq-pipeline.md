 <a name="content">目录</a>
 - [1.数据下载](#download)
 - [2. 解压与双端配对](#unzip-pairs)
 	- [解压](#unzip)
 	- [双端配对](#pairs)
 - [3. 质控与质量编辑](#qc-process)
 	- [质控](#qc)
 	- [质量编辑](#process)
 - [4. 过滤细菌库](#filt-baclib)
 	- [与细菌库比对](#filt-map)
 	- [过滤出mapping上细菌库的序列](#filt-bac)
 	- [过滤掉mapping上细菌库的序列](#remove-bac)
 - [5. 饱和度分析](#saturation)
 	- [按照比例](#percent)
 	- [按照测序深度](#depth)
 - [6. 比对参考转录组](#map)
 - [7. 转录本拼接](#assembly)
 - [8. 样本间转录本合并](#merge)
 - [9. 表达量计算并以ballgown格式输出](#count)
 - [10. 差异表达分析，用R包ballgown](#diff-analysis)
 
 # 转录组数据分析流程 #

日期：2017-12-3

作者：连明



<a name="download"><h3>1.数据下载</h3></a>

```
wget -c --ftp-password=*** --ftp-user=**** -P $wd/Path/ <ip.adress>
```

<a name="unzip-pairs"><h3>2. 解压与双端配对</h3></a>

<a name="unzip"><h4>解压</h4></a>

```
if [ ! -f $wd/$cleandata_dir/${1}_Clean_Data1.fq ]
then
	gzip -dc $wd/$cleandata_dir/${1}_Clean_Data1.fq.gz 1>$wd/$cleandata_dir/${1}_Clean_Data1.fq 2>$wd/$cleandata_dir/${1}_unzip.log
	echo "[unzip&pairs-mate] Finish unzip ${1}_1"
else
	echo "[unzip&pairs-mate] ${1}_1 has been unziped"
fi
```



<a name="pairs"><h4>双端配对</h4></a>

```
fq1_line=`wc -l $wd/$cleandata_dir/${1}_Clean_Data1.fq | perl -ane 'chomp;print "$F[0]"'`
fq2_line=`wc -l $wd/$cleandata_dir/${1}_Clean_Data2.fq | perl -ane 'chomp;print "$F[0]"'`
mate_str=""
if [ $fq1_line -ne $fq2_line ]
then
	echo "[unzip&pairs-mate] fq1 not match fq2, now processing pairs-mate"
	mate_str="mate."
	if [ ! -f $wd/$cleandata_dir/${1}_Clean_Data1.mate.fq ]&&[ ! -f $wd/$cleandata_dir/${1}_Clean_Data2.mate.fq ]
	then
		perl $wd/perlscript/ pairs_mate.pl $wd/$cleandata_dir/${1}_Clean_Data1.fq $wd/$cleandata_dir/${1}_Clean_Data2.fq $wd/$cleandata_dir/${1}_Clean_Data1.mate.fq $wd/$cleandata_dir/${1}_Clean_Data2.mate.fq
	else
		echo "[unzip&pairs-mate] pairs-mate has been processed"
	fi
fi
```
双端配对所用的perl脚本**pairs_mate.pl**保存路径为`/share/disk5/lianm/perlscript/pairs_mate.pl`

[返回目录](#content)

<a name="qc-process"><h3>3. 质控与质量编辑</h3></a>

<a name="qc"><h4>质控</h4></a>

```
fastqc -t num_threads -o out_dir -noextract file1.fq.gz .. fileN.fq.gz
```

<a name="process"><h4>质量编辑</h4></a>

```
perl piplineForQC.pl adp_qual -p -a adapt_seq -f RC-5_1.fastq -r RC-5_2.fastq -o output_prefix
```
QC所用的perl脚本**piplineForQC.pl**保存路径为`/share/disk5/lianm/perlscript/piplineForQC.pl`

[返回目录](#content)

<a name="filt-baclib"><h3>4. 过滤细菌库</h3></a>

<a name="filt-map"><h4>与细菌库比对（进行单端mapping)</h4></a>

```
bwa aln -t 10 -f $wd/$map_dir/${1}_BacLib_1.sai $wd/Ref/NCBI_bacteria/referance.fasta $wd/$cleandata_dir/${1}_Clean_Data1.${mate_str}fq 1>$wd/$map_dir/${1}_BacLib_1.sai.log 2>&1
echo "[filt] Finish searching SA coordinate for ${1}_Clean_Data1.${mate_str}fq"
bwa aln -t 10 -f $wd/$map_dir/${1}_BacLib_2.sai $wd/Ref/NCBI_bacteria/referance.fasta $wd/$cleandata_dir/${1}_Clean_Data2.${mate_str}fq 1>$wd/$map_dir/${1}_BacLib_2.sai.log 2>&1
echo "[filt] Finish searching SA coordinate for ${1}_Clean_Data2.${mate_str}fq"
bwa samse -f $wd/$map_dir/${1}_BacLib_1.sam $wd/Ref/NCBI_bacteria/referance.fasta $wd/$map_dir/${1}_BacLib_1.sai $wd/$cleandata_dir/${1}_Clean_Data1.${mate_str}fq 1>$wd/$map_dir/${1}_BacLib_1.sam.log 2>&1
echo "[filt] Finish single-end mapping for ${1}_Clean_Data1.${mate_str}fq"
bwa samse -f $wd/$map_dir/${1}_BacLib_2.sam $wd/Ref/NCBI_bacteria/referance.fasta $wd/$map_dir/${1}_BacLib_2.sai $wd/$cleandata_dir/${1}_Clean_Data2.${mate_str}fq 1>$wd/$map_dir/${1}_BacLib_2.sam.log 2>&1
echo "[filt] Finish single-end mapping for ${1}_Clean_Data2.${mate_str}fq"
```

<a name="filt-bac"><h4>过滤*出*mapping上细菌库的序列</h4></a>

```
perl -ane 'chomp;next if (/^\@/);if ($F[2] ne "*"){print "$_\n"}' $wd/$map_dir/${1}_BacLib_1.sam >$wd/$map_dir/${1}_BacLib_1.sam.filt
perl -ane 'chomp;next if (/^\@/);if ($F[2] ne "*"){print "$_\n"}' $wd/$map_dir/${1}_BacLib_2.sam >$wd/$map_dir/${1}_BacLib_2.sam.filt
```
<a name="remove-bac"><h4>过滤*掉*mapping上细菌库的序列</h4></a>
```
perl $wd/perlscript/sel_seq_for_Hiseq3000.pl $wd/$map_dir/${1}_BacLib_1.sam.filt $wd/$map_dir/${1}_BacLib_2.sam.filt $wd/$cleandata_dir/${1}_Clean_Data1.${mate_str}fq $wd/$cleandata_dir/${1}_Clean_Data2.${mate_str}fq \
$wd/$cleandata_dir/${1}_Clean_Data1.filtBacLib.fq $wd/$cleandata_dir/${1}_Clean_Data2.filtBacLib.fq 
echo "[filt] Finish filt bac contaminate"
```

[返回目录](#content)

<a name="saturation"><h3>5. 饱和度分析</h3></a>

```
bwa aln -t 10 -f $wd/$map_dir/cds_${sample}_1.sai $wd/$ref_cds $wd/$cleandata_dir/${sample}_Clean_Data1.filtBacLib.fq 1>$wd/$map_dir/cds_${sample}_1.sai.log 2>&1
echo "[saturation] Finish search SA coordinate for ${sample}_Clean_Data1.filtBacLib.fq"
bwa aln -t 10 -f $wd/$map_dir/cds_${sample}_2.sai $wd/$ref_cds $wd/$cleandata_dir/${sample}_Clean_Data2.filtBacLib.fq 1>$wd/$map_dir/cds_${sample}_2.sai.log 2>&1
echo "[saturation] Finish search SA coordinate for ${sample}_Clean_Data2.filtBacLib.fq"
bwa sampe -f $wd/$map_dir/cds_${sample}.sam $wd/$ref_cds $wd/$map_dir/cds_${sample}_1.sai \
	$wd/$map_dir/cds_${sample}_2.sai $wd/$cleandata_dir/${sample}_Clean_Data1.filtBacLib.fq $wd/$cleandata_dir/${sample}_Clean_Data2.filtBacLib.fq 1>$wd/$map_dir/cds_${sample}.sam.log 2>&1
echo "[saturation] Finish pair-end mapping for $sample"
```

<a name="percent"><h4>按照比例</h4></a>

```
for i in 5 10 15 20 30 40 50 60 70 80 90
do
	export i
	perl -ne 'chomp;next if (/^\@/);if (rand()<0.01*$ENV{"i"}){print "$_\n";}' $wd/$map_dir/cds_${sample}.sam | cut -f 3 | sort | uniq | wc -l >>$wd/$satu_dir/stat/${sample}.txt
	echo "[saturation] Analyse saturation for $sample: ${i}%"
done 
rm $wd/$map_dir/cds_${sample}_[12].sa[im]
rm $wd/$map_dir/cds_${sample}.sam
```

<a name="depth"><h4>按照测序深度（一个外显子组大小为50M）</h4></a>

```
total_reads=`perl -ne 'chomp;next if (/^\@/);print "$_\n"' $wd/$map_dir/cds_${sample}.sam | wc -l | perl -ane 'chomp;print "$F[0]"'`
export total_reads
exome_length=50000000
reads_length=150
depth1_reads=$[$exome_length/$reads_length]
export depth1_reads
max_depth=$[$total_reads*$reads_length/$exome_length]
if [ -f $wd/$satu_dir/stat/${sample}_depth.txt ]
then
	rm $wd/$satu_dir/stat/${sample}_depth.txt
fi
for ((i=5;i<=max_depth;i+=5))
do
	current_depth=$i
	export current_depth
	echo -ne "$current_depth\t" >>$wd/$satu_dir/stat/${sample}_depth.txt
	perl -ne 'chomp;next if (/^\@/);if (rand()<($ENV{"current_depth"}*$ENV{"depth1_reads"}/$ENV{"total_reads"})){print "$_\n";}' $wd/$map_dir/cds_${sample}.sam | cut -f 3 | sort | uniq | wc -l >>$wd/$satu_dir/stat/${sample}_depth.txt
	echo "[saturation] Analyse saturation for $sample: ${current_depth}X"
done
```

[返回目录](#content)

<a name="map"><h3>6. 比对参考转录组</h3></a>

```
hisat2 -p 10 --dta -x $wd/Ref/hg19/grch37_tran/genome_tran -1 $wd/$cleandata_dir/${1}_Clean_Data1.filtBacLib.fq -2 $wd/$cleandata_dir/${1}_Clean_Data2.filtBacLib.fq -S $wd/$map_dir/${1}_filtBacLib.sam 1>$wd/$map_dir/${1}_filtBacLib_map.log 2>&1
echo "[map] Finish mapping for $1"
samtools sort -@ 16 -o $wd/$map_dir/${1}_filtBacLib.bam $wd/$map_dir/${1}_filtBacLib.sam
rm $wd/$map_dir/${1}_filtBacLib.sam #及时删除临时文件
```


<a name="assembly"><h3>7. 转录本拼接</h3></a>
```
stringtie -p 16 -G $wd/Ref/hg19/grch37_tran/Homo_sapiens.GRCh37.75.gtf -o $wd/$cleandata_pDir/Asm/${i}_filtBacLib.gtf -l $i $wd/$cleandata_pDir/Map/${i}_filtBacLib.bam 1>$wd/$cleandata_pDir/Asm/${i}_filtBacLib.log 2>&1
```


<a name="merge"><h3>8. 样本间转录本合并</h3></a>
```
stringtie --merge -p 16 -G $wd/Ref/hg19/grch37_tran/Homo_sapiens.GRCh37.75.gtf -o $wd/$cleandata_pDir/Asm/merge.gtf $wd/$cleandata_pDir/Asm/mergelist.txt 1>$wd/$cleandata_pDir/Asm/merge.log 2>&1
```


<a name="count"><h3>9. 表达量计算并以ballgown格式输出</h3></a>
```
stringtie -e -B -p 16 -G $wd/$cleandata_pDir/Asm/merge.gtf -o $wd/$cleandata_pDir/Expression/$i/${i}_filtBacLib.gtf $wd/$cleandata_pDir/Map/${i}_filtBacLib.bam 1>$wd/$cleandata_pDir/Expression/$i/${i}_filtBacLib_quant.log 2>&1
```

[返回目录](#content)

<a name="diff-analysis"><h3>10. 差异表达分析，用R包ballgown</h3></a>
- 载入R包
```
require(ballgown)
require(dplyr)
require(genefilter)
setwd("/share/disk5/lianm")
```
- 载入stringtie输出的表达数据，并设置表型信息（即分组信息）
```
bg_Z1Z4<-ballgown(dataDir="SingleCell_process/Cleandata/Expression",samplePattern=“Z[14]T",meas="FPKM")
pData(bg_Z1Z4)<-data.frame(id=sampleNames(bg_Z1Z4),group=c(rep(1,num_group1),rep(0,num_group2)))
```
- 过滤低丰度的基因
```
bg_Z1Z4_filt<-subset(bg_Z1Z4,"rowVars(texpr(bg_Z1Z4))>1",genomesubset=T)
```
- 差异表达基因分析
```
result_genes<-stattest(bg_Z1Z4_filt,feature="gene",covariate="group",getFC=T)
result_genes<-data.frame(geneNames=geneNames(bg_Z1Z4_filt)[match(result_genes$id,geneIDs(bg_Z1Z4_filt))],geneIDs=geneIDs(bg_Z1Z4_filt)[match(result_genes$id,geneIDs(bg_Z1Z4_filt))],result_genes)
result_genes_sort<-arrange(result_genes,pval)
write.csv(result_genes_sort,file=paste("SingleCell_process/Cleandata/Expression/",name_group1,"_VS_",name_group2,"_geneDiff_results.csv",sep=""),row.names=F)
```
> 分组设置对差异表达分析的影响：
> - FC = group_1/group_0，所以分组标签互换后FC会变为原来的倒数

- 差异转录本分析
```
result_trans<-stattest(bg_Z1Z4_filt,feature="transcript",covariate="group",getFC=T)
result_trans<-data.frame(geneNames=geneNames(bg_Z1Z4_filt),geneIDs=geneIDs(bg_Z1Z4_filt),result_trans)
result_trans_sort<-arrange(result_transs,pval)
write.csv(result_trans_sort,file=paste("SingleCell_process/Cleandata/Expression/",name_group1,"_VS_",name_group2,"_transDiff_results.csv",sep=""),row.names=F)
```