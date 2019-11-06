---
title: 词云小demo
tags: jieba,wordcloud
grammar_cjkRuby: true
---
#### 一 什么是词云？
由词汇组成类似云的彩色图形。“词云”就是对网络文本中出现频率较高的“关键词”予以视觉上的突出，形成“关键词云层”或“关键词渲染”，从而过滤掉大量的文本信息，使浏览网页者只要一眼扫过文本就可以领略文本的主旨。
#### 二 有什么作用？
1、直观，高大上

2、可装逼，很潇洒

#### 三 准备工作

1、导入包——jieba和wordcloud

命令：pip install jieba

命令：pip install wordcloud

备注：对于pycharm等可采用各自的方法导入包

2、文本和图片的准备

文本：可爬取网上资料或某歌曲书籍等关键字，亦或是像我是自己手动输入文字并用tab隔开

图片：找自己喜欢的图片，这里我采用乔巴的图片作为背景，而且除了主要人物外，其他背景都为白色，显示效果较好。

采用的文本内容：

> paper going keep fighting happy Backpropagation/BP AI 
Technology Chine new year you tahnks hha
hmmm emmm yesterday sunday Batch Normalization/BN autoencoder 
ALL Data big math python abc Thanks for your  reminder, I’ll update resource dll to fix those issue.

采用的图片：
![enter description here](http://futuretechx.com/wp-content/uploads/2019/01/ciyun.jpg)

#### 四 代码如下：

``` python
# coding: utf-8
import jieba
from wordcloud import WordCloud,STOPWORDS
from scipy.misc import imread # 处理图像的函数
import matplotlib.pyplot as plt
# 读取文本文件
text = open('t1.txt', 'r').read()
# 对文本进行分词
cut_text = ''.join(jieba.cut(text))#cut分词，然后将分开的词用空格连接
# 读取图片
color_mask = imread('ciyun.jpg')
# 生成词云
cloud = WordCloud(# 这里是导入字体，因为我是采用英文的，所有不导入也并不影响，若是中文的或者有其他的字符需要自己选择合适的字体包
 background_color="white",
 mask=color_mask,
 max_words=2000,
 max_font_size=80)
word_cloud = cloud.generate(cut_text)
cloud.to_file('ss.png')#保存文件
#使用plt显示图片
plt.axis('off')#不显示坐标轴
#显示图片
plt.imshow(word_cloud)
plt.show()
```
#### 五 效果如下：
![效果图](http://futuretechx.com/wp-content/uploads/2019/01/效果图.png)
#### 六 解析
6.1 jieba（结巴）是一个强大的分词库，完美支持中文分词，本文对其基本用法做一个简要总结。
6.1.2 基本分词函数与用法
jieba.cut 以及 jieba.cut_for_search 返回的结构都是一个可迭代的 generator，可以使用 for 循环来获得分词后得到的每一个词语(unicode)
jieba.cut 方法接受三个输入参数:
 - 需要分词的字符串 
 - cut_all 参数用来控制是否采用全模式 (精准模式和全模式，默认是精准模式)
 - HMM 参数用来控制是否使用 HMM 模型

jieba.cut_for_search （搜索引擎模式）方法接受两个参数
- 需要分词的字符串
- 是否使用 HMM 模型。
该方法适合用于搜索引擎构建倒排索引的分词，粒度比较细

``` python
import jieba

list0 = jieba.cut('小明硕士毕业于中国科学院计算所，后在哈佛大学深造', cut_all=True)
print('全模式', list(list0))
# ['小', '明', '硕士', '毕业', '于', '中国', '中国科学院', '科学', '科学院', '学院', '计算', '计算所', '', '', '后', '在', '哈佛', '哈佛大学', '大学', '深造']
list1 = jieba.cut('小明硕士毕业于中国科学院计算所，后在哈佛大学深造', cut_all=False)
print('精准模式', list(list1))
# ['小明', '硕士', '毕业', '于', '中国科学院', '计算所', '，', '后', '在', '哈佛大学', '深造']
list2 = jieba.cut_for_search('小明硕士毕业于中国科学院计算所，后在哈佛大学深造')
print('搜索引擎模式', list(list2))
# ['小明', '硕士', '毕业', '于', '中国', '科学', '学院', '科学院', '中国科学院', '计算', '计算所', '，', '后', '在', '哈佛', '大学', '哈佛大学', '深造']
```
更详细的用法参考：https://www.cnblogs.com/felixwang2/p/8660259.html，https://www.cnblogs.com/jiayongji/p/7119080.html
6.2 wordcloud(词云)库
下面来介绍一下wordcloud包的基本用法。

``` python
class wordcloud.WordCloud(font_path=None, width=400, height=200, margin=2, ranks_only=None, prefer_horizontal=0.9,mask=None, scale=1, color_func=None, max_words=200, min_font_size=4, stopwords=None, random_state=None,background_color='black', max_font_size=None, font_step=1, mode='RGB', relative_scaling=0.5, regexp=None, collocations=True,colormap=None, normalize_plurals=True)
```
这是wordcloud的所有参数，下面具体介绍一下各个参数:

``` python
font_path : string //字体路径，需要展现什么字体就把该字体路径+后缀名写上，如：font_path = '黑体.ttf'

width : int (default=400) //输出的画布宽度，默认为400像素

height : int (default=200) //输出的画布高度，默认为200像素

prefer_horizontal : float (default=0.90) //词语水平方向排版出现的频率，默认 0.9 （所以词语垂直方向排版出现频率为 0.1 ）

mask : nd-array or None (default=None) //如果参数为空，则使用二维遮罩绘制词云。如果 mask 非空，设置的宽高值将被忽略，遮罩形状被 mask 取代。除全白（#FFFFFF）的部分将不会绘制，其余部分会用于绘制词云。如：bg_pic = imread('读取一张图片.png')，背景图片的画布一定要设置为白色（#FFFFFF），然后显示的形状为不是白色的其他颜色。可以用ps工具将自己要显示的形状复制到一个纯白色的画布上再保存，就ok了。

scale : float (default=1) //按照比例进行放大画布，如设置为1.5，则长和宽都是原来画布的1.5倍。

min_font_size : int (default=4) //显示的最小的字体大小

font_step : int (default=1) //字体步长，如果步长大于1，会加快运算但是可能导致结果出现较大的误差。

max_words : number (default=200) //要显示的词的最大个数

stopwords : set of strings or None //设置需要屏蔽的词，如果为空，则使用内置的STOPWORDS

background_color : color value (default=”black”) //背景颜色，如background_color='white',背景颜色为白色。

max_font_size : int or None (default=None) //显示的最大的字体大小

mode : string (default=”RGB”) //当参数为“RGBA”并且background_color不为空时，背景为透明。

relative_scaling : float (default=.5) //词频和字体大小的关联性

color_func : callable, default=None //生成新颜色的函数，如果为空，则使用 self.color_func

regexp : string or None (optional) //使用正则表达式分隔输入的文本

collocations : bool, default=True //是否包括两个词的搭配

colormap : string or matplotlib colormap, default=”viridis” //给每个单词随机分配颜色，若指定color_func，则忽略该方法。

fit_words(frequencies)  //根据词频生成词云
generate(text)  //根据文本生成词云
generate_from_frequencies(frequencies[, ...])   //根据词频生成词云
generate_from_text(text)    //根据文本生成词云
process_text(text)  //将长文本分词并去除屏蔽词（此处指英语，中文分词还是需要自己用别的库先行实现，使用上面的 fit_words(frequencies) ）
recolor([random_state, color_func, colormap])   //对现有输出重新着色。重新上色会比重新生成整个词云快很多。
to_array()  //转化为 numpy array
to_file(filename)   //输出到文件
原文：https://blog.csdn.net/u010309756/article/details/67637930 
```
