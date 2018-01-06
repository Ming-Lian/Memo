目录
- [1. 原理](#principle)
- [2. 应用](#app)



# BWT算法学习笔记

![](/bwt.jpg "Burrows–Wheeler_transform")

**BWT算法的基本过程。(a)数据转换；(b)精确定位子字符串；(c)解码。**


<a name="principle"><h3>1. 原理</h3></a>
首先，什么是BWT，可以参考博客：http://www.cnblogs.com/xudong-bupt/p/3763814.html ，讲得非常好，这里就不重复造轮子了。

![](http://www.bio-info-trainee.com/wp-content/uploads/2015/03/BWT%E7%AE%97%E6%B3%95%E8%AF%A6%E8%A7%A3%E4%B9%8B%E4%B8%80%E5%BB%BA%E7%AB%8B%E7%B4%A2%E5%BC%95348.png)
<a name="app"><h3>2. 应用</h3></a>
BWT算法有三个应用：
> - 字符串无损压缩
> - 根据压缩回溯还原原字符串
> - 子字符串的精确定位

在生物信息学中，尤其是在NGS的生物信息学应用中对应为：
> - 建立基因组索引
> - 根据基因组索引还原原基因组（这个应用很少见）
> - reads的mapping到参考基因组

![](/FM-table.png)

要想使用BWT算法，需要保存对原始字符串BWT转换后的必要信息：
> - L列的完整信息
> - F列中字符c（原字符串中的某一个字符）的其实位置（行号）
> - L列中i行对应的字符c在L列中出现的次数

这些信息可以以两个向量来存储
> - 向量F，F（字符c，起始位置）
> - 向量L，L（字符c，字符c出现的次数）


参考资料：

(1)[自己动手写bowtie第一讲](http://www.bio-info-trainee.com/409.html)

(2)[BWT (Burrows–Wheeler_transform)数据转换算法](http://www.cnblogs.com/xudong-bupt/p/3763814.html)

(3)[BWT数据压缩算法](http://emily2ly.iteye.com/blog/742869)
