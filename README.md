# compress

目录
[TOC]


## 开源产品介绍（微服务基础设施<font color="red">QQ交流群：191958521</font>）
+ 配置中心(mconf)

1. GITHUB：https://github.com/yu120/mconf
2. 码云：https://git.oschina.net/yu120/mconf

+ 微核心(micro)

1. GITHUB：https://github.com/yu120/micro
2. 码云：https://git.oschina.net/yu120/micro

+ 微服务神经元(neural)

1. GITHUB：https://github.com/yu120/neural
2. 码云：https://git.oschina.net/yu120/neural

+ 微序列(sequence)

1. https://git.oschina.net/yu120/sequence


### 1 前言
基于gzip、deflate、lz4、snappy、lzo等算法实现数据压缩，主要用于RPC通讯数据的压缩！

### 2 压缩方案
+ Bzip2

bzip2是Julian Seward开发并按照自由软件／开源软件协议发布的数据压缩算法及程序。Seward在1996年7月第一次公开发布了bzip2 0.15版，在随后几年中这个压缩工具稳定性得到改善并且日渐流行，Seward在2000年晚些时候发布了1.0版。bzip2比传统的gzip的压缩效率更高，但是它的压缩速度较慢。

+ Deflater

DEFLATE是同时使用了LZ77算法与哈夫曼编码（Huffman Coding）的一个无损数据压缩算法，DEFLATE压缩与解压的源代码可以在自由、通用的压缩库zlib上找到，zlib官网：http://www.zlib.net/ 
jdk中对zlib压缩库提供了支持，压缩类Deflater和解压类Inflater，Deflater和Inflater都提供了native方法。

+ Gzip

gzip的实现算法还是deflate，只是在deflate格式上增加了文件头和文件尾，同样jdk也对gzip提供了支持，分别是GZIPOutputStream和GZIPInputStream类，同样可以发现GZIPOutputStream是继承于DeflaterOutputStream的，GZIPInputStream继承于InflaterInputStream，并且可以在源码中发现writeHeader和writeTrailer方法。

+ Lz4

LZ4是一种无损数据压缩算法，着重于压缩和解压缩速度。

+ Lzo

LZO是致力于解压速度的一种数据压缩算法，LZO是Lempel-Ziv-Oberhumer的缩写，这个算法是无损算法。

+ Snappy

Snappy（以前称Zippy）是Google基于LZ77的思路用C++语言编写的快速数据压缩与解压程序库，并在2011年开源。它的目标并非最大压缩率或与其他压缩程序库的兼容性，而是非常高的速度和合理的压缩率。

### 3 性能对比
env:JDK:1.7/CPU:4C/Compress Times：2000times<br>


<table>
<tr><td>Format</td><td>Size Before(byte)</td><td>Size After(byte)</td><td>Compress Expend(ms)</td><td>UnCompress Expend(ms)</td><td>MAX CPU(%)</td></tr>
<tr><td>bzip2</td><td>35984</td><td>8677</td><td>11591</td><td>2362</td><td>29.5</td></tr>
<tr><td>gzip</td><td>35984</td><td>8804</td><td>2179</td><td>389</td><td>26.5</td></tr>
<tr><td>deflate</td><td>35984</td><td>9704</td><td>680</td><td>344</td><td>20.5</td></tr>
<tr><td>lzo</td><td>35984</td><td>13069</td><td>581</td><td>230</td><td>22</td></tr>
<tr><td>lz4</td><td>35984</td><td>16355</td><td>327</td><td>147</td><td>12.6</td></tr>
<tr><td>snappy</td><td>35984</td><td>13602</td><td>424</td><td>88</td><td>11</td></tr>
</table>
