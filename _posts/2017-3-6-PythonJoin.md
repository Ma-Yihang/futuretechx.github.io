---
title: Python join() 方法与os.path.join()的区别
tags: python,Join,os.path.join
grammar_mindmap: true
renderNumberedHeading: true
---
今天工作中用到python的join方法，有点分不太清楚join() 方法与os.path.join()的区别，查了下，写个例子记录下，发现python的有些功能挺强大的，写了几行代码就搞定了，要是用c/C++,估计要多写很多行代码。

### 函数作用：
join() ：将序列、字符串 、元组等中的元素以指定的字符连接生成一个新的字符串。
os.path.join() ： 将多个路径组合后返回
### join()方法说明：
join()方法 
语法：
str.join(sequence)
参数说明：
str：指定的字符，即分隔符
sequence：需要连接的元素

``` python
#字符串序列

seq = ("apple", "banana", "pear")

str = ""
print(str.join(seq))
#applebananapear

str = " "
print(str.join(seq))
#apple banana pear

str = "-"
print(str.join(seq))
#apple-banana-pear
```
输出结果：

> applebananapear
apple banana pear
apple-banana-pear

### os.path.join() 函数说明
os.path.join() 函数
语法：
os.path.join(path1[,path2[,……]])

``` python
import os
path_root = 'D:\Study'
dirs = os.listdir(path_root)

# 输出所有文件和文件夹
for file in dirs:
    path = os.path.join(path_root,file)
    path_test = os.path.join(path,'test')
    #print(path)
    print(path_test)
```
结果如下：

> D:\Study\365天英语口语大全--商贸口语 MP3\test
D:\Study\BaiduNetdisk-6.2.4.exe\test
D:\Study\BaiduNetdiskDownload\test
D:\Study\Blog\test
D:\Study\Desktop_backgroundPicture_bing-master\test
D:\Study\Desktop_backgroundPicture_bing-master.zip\test
D:\Study\HornilStylePix2.0.1.0Setup.exe\test
D:\Study\PowerShell+进阶教程.pdf\test
D:\Study\Python\test
D:\Study\TerPict12522846.tmp\test
D:\Study\TerPict8657560.tmp\test
D:\Study\vs_professional.exe\test
D:\Study\vs_professional_2012.exe\test
D:\Study\数学题源探析经典1000题解分析\test
D:\Study\数学题源探析经典1000题解分析.zip\test
D:\Study\汤数学高等数学基础讲义.pdf\test
D:\Study\汤高数基础课程笔记(手写版).pdf\test

