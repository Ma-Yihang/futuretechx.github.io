---
title: python常用模块之时间模块
tags: python全栈开发,时间模块
grammar_cjkRuby: true
---
上次的博客link:[enter description here](http://futuretechx.com/python-collections/)接着上次的继续学习：
#### 时间模块
和时间有关系的我们就要用到时间模块。在使用模块之前，应该首先导入这个模块。

``` python
#常用方法
1.time.sleep(secs) #(线程)推迟指定的时间运行。单位为秒。
2.time.time() #获取当前时间戳
```
**表示时间的三种方式**

在Python中，通常有这三种方式来表示时间：时间戳、元组(struct_time)、格式化的时间字符串：
(1)时间戳(timestamp) ：通常来说，时间戳表示的是从1970年1月1日00:00:00开始按秒计算的偏移量。我们运行“type(time.time())”，返回的是float类型。
(2)格式化的时间字符串(Format String)： ‘1999-12-06’
> %y 两位数的年份表示（00-99）
%Y 四位数的年份表示（000-9999）
%m 月份（01-12）
%d 月内中的一天（0-31）
%H 24小时制小时数（0-23）
%I 12小时制小时数（01-12）
%M 分钟数（00=59）
%S 秒（00-59）
%a 本地简化星期名称
%A 本地完整星期名称
%b 本地简化的月份名称
%B 本地完整的月份名称
%c 本地相应的日期表示和时间表示
%j 年内的一天（001-366）
%p 本地A.M.或P.M.的等价符
%U 一年中的星期数（00-53）星期天为星期的开始
%w 星期（0-6），星期天为星期的开始
%W 一年中的星期数（00-53）星期一为星期的开始
%x 本地相应的日期表示
%X 本地相应的时间表示
%Z 当前时区的名称
%% %号本身

``` python
print(time.strftime("%Y-%m-%d %a %H:%M:%S"))  #year month day HOUR MINUTE SECOND
print(time.strftime("%Y/%m/%d %H:%M:%S"))  #year month day HOUR MINUTE SECOND
print(time.strftime("%m-%d %H:%M:%S"))  #year month day HOUR MINUTE SECOND
print(time.strftime("%H:%M:%S"))  #year month day HOUR MINUTE SECOND
print(time.strftime("%H:%M"))  #year month day HOUR MINUTE SECOND
OutPut:
2018-12-01 Sat 22:12:32
2018/12/01 22:12:32
12-01 22:12:32
22:12:32
22:12
```
(3)元组(struct_time) ：struct_time元组共有9个元素共九个元素:(年，月，日，时，分，秒，一年中第几周，一年中第几天等）

| 索引（Index） | 属性（Attribute） | 值（Values） |
| ------------- | ----------------- | ------------ |
|   0            |   tm_yea(年)           |   比如2011           |
|       1        |   tm_mon（月）           | 1 - 12             |
|       2        |    tm_mday（日）            |	1 - 31              |
|       3        |     tm_hour（时）              | 0 - 23             |
|       4        |    tm_min（分）               | 0 - 59              |
|       5      |      tm_sec（秒）             |  	0 - 60            |
|        6       |    tm_wday（weekday）               | 0 - 6（0表示周一 ）            |
|        7       |   	tm_yday（一年中的第几天）                | 	1 - 366             |
|         8     |  tm_isdst（是否是夏令时）                 |  默认为0            |

``` python
struct_time = time.localtime()
print(struct_time)
print(struct_time.tm_year)
Output:
time.struct_time(tm_year=2018, tm_mon=12, tm_mday=1, tm_hour=22, tm_min=12, tm_sec=32, tm_wday=5, tm_yday=335, tm_isdst=0)
2018
```
 首先，我们先导入time模块，来认识一下python中表示时间的几种格式：
 

``` python
#导入时间模块
>>>import time

#时间戳
>>>time.time()
1543672628.0404546

#时间字符串
>>>time.strftime("%Y-%m-%d %X")
2018-12-01 21:57:08
>>>time.strftime("%Y-%m-%d %H-%M-%S")
2018-12-01 21-57-08'

#时间元组:localtime将一个时间戳转换为当前时区的struct_time
time.localtime()
time.struct_time(tm_year=2017, tm_mon=7, tm_mday=24,
　　　　　　　　　　tm_hour=13, tm_min=59, tm_sec=37, 
                 tm_wday=0, tm_yday=205, tm_isdst=0)
```
小结：时间戳是计算机能够识别的时间；时间字符串是人能够看懂的时间；元组则是用来操作时间的
**几种格式之间的转换**
![几种格式之间的转换](http://futuretechx.com/wp-content/uploads/2018/12/827651-20170724144151992-1508626640.png)

``` python
#时间戳-->结构化时间
#time.gmtime(时间戳)    #UTC时间，与英国伦敦当地时间一致
#time.localtime(时间戳) #当地时间。例如我们现在在北京执行这个方法：与UTC时间相差8小时，UTC时间+8小时 = 北京时间 
>>>time.gmtime(1500000000)
time.struct_time(tm_year=2017, tm_mon=7, tm_mday=14, tm_hour=2, tm_min=40, tm_sec=0, tm_wday=4, tm_yday=195, tm_isdst=0)
>>>time.localtime(1500000000)
time.struct_time(tm_year=2017, tm_mon=7, tm_mday=14, tm_hour=10, tm_min=40, tm_sec=0, tm_wday=4, tm_yday=195, tm_isdst=0)

#结构化时间-->时间戳　
#time.mktime(结构化时间)
>>>time_tuple = time.localtime(1500000000)
>>>time.mktime(time_tuple)
1500000000.0
```

``` python
#结构化时间-->字符串时间
#time.strftime("格式定义","结构化时间")  结构化时间参数若不传，则显示当前时间
>>>time.strftime("%Y-%m-%d %X")
'2018-12-01 22:22:39'
>>>time.strftime("%Y-%m-%d",time.localtime(1500000000))
'2017-07-14'

#字符串时间-->结构化时间
#time.strptime(时间字符串,字符串对应格式)
>>>time.strptime("2017-03-16","%Y-%m-%d")
time.struct_time(tm_year=2017, tm_mon=3, tm_mday=16, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=3, tm_yday=75, tm_isdst=-1)
>>>time.strptime("07/24/2017","%m/%d/%Y")
time.struct_time(tm_year=2017, tm_mon=7, tm_mday=24, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=0, tm_yday=205, tm_isdst=-1)
```
![enter description here](http://futuretechx.com/wp-content/uploads/2018/12/827651-20170724144235883-1963884021.png)

``` python
#结构化时间 --> %a %b %d %H:%M:%S %Y串
#time.asctime(结构化时间) 如果不传参数，直接返回当前时间的格式化串
>>>time.asctime(time.localtime(1500000000))
'Fri Jul 14 10:40:00 2017'
>>>time.asctime()
'Mon Jul 24 15:18:33 2017'

#时间戳 --> %a %b %d %H:%M:%S %Y串
#time.ctime(时间戳)  如果不传参数，直接返回当前时间的格式化串
>>>time.ctime()
'Mon Jul 24 15:19:07 2017'
>>>time.ctime(1500000000)
'Fri Jul 14 10:40:00 2017' 
```
一个小例子：计算时间差

``` python
import time
true_time=time.mktime(time.strptime('2017-09-11 08:30:00','%Y-%m-%d %H:%M:%S'))
time_now=time.mktime(time.strptime('2017-09-12 11:00:00','%Y-%m-%d %H:%M:%S'))
dif_time=time_now-true_time
struct_time=time.gmtime(dif_time)
print('过去了%d年%d月%d天%d小时%d分钟%d秒'%(struct_time.tm_year-1970,struct_time.tm_mon-1,
                                       struct_time.tm_mday-1,struct_time.tm_hour,
                                       struct_time.tm_min,struct_time.tm_sec))
Output:
过去了0年0月1天2小时30分钟0秒
```

