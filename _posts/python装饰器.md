---
title: python装饰器
tags: Python，装饰器
grammar_cjkRuby: true
---
### 装饰器
装饰器的形成过程：最简单的装饰器，一个参数的装饰器，万能参数
装饰器函数的作用：不想改变函数的调用方式，但是还是想在原来的函数前后添加功能。（在不修改原函数及其调用方式的情况下对原函数功能进行扩展）
timmer（）是装饰器函数，只是有个函数，有些装饰作用
语法糖：让代码更简单。更简洁，@timmer
``` python
import time
    
def timer(f): #装饰器函数
    def inner():
        start = time.time()
        ret=f() #被装饰的函数
        end=time.end()
        print(end-start)
    return ret
    return inner
@timmer #语法糖 @装饰器函数名,相当于调用func=timmer(func)
def func(): #紧挨着被装饰函数
    time.sheep(0.01)
    print("第一次用小书匠写博客，感觉还不错")
    
#func = timmer(func)
ret = func()
print(ret)
```

### 装饰器的原则
原则：开放封闭原则
开放：对扩展是开放的
封闭：对修改是封闭的
详细介绍：
> 1.对扩展是开放的
　　　　为什么要对扩展开放呢？
　　　　我们说，任何一个程序，不可能在设计之初就已经想好了所有的功能并且未来不做任何更新和修改。所以我们必须允许代码扩展、添加新功能。
　　2.对修改是封闭的
　　　　为什么要对修改封闭呢？
　　　　就像我们刚刚提到的，因为我们写的一个函数，很有可能已经交付给其他人使用了，如果这个时候我们对其进行了修改，很有可能影响其他已经在使用该函数的用户。
装饰器完美的遵循了这个开放封闭原则。

``` python
def outer():
    def iner():
    return "inner"
    inner()
outer()
```
###  传参的被装饰函数，装饰带参数的装饰器
``` python
import time
    
def timer(f): #装饰器函数
    def inner(a):
        start = time.time()
        ret=f(a) #被装饰的函数
        end=time.end()
        print(end-start)
    return ret
    return inner
    
@timmer 
#语法糖 @装饰器函数名,相当于调用func=timmer(func)

def func(a): #紧挨着被装饰函数
    time.sheep(0.01)
    print("第一次用小书匠写博客，感觉还不错",a)
    return "不错不错"
    
#func = timmer(func)
ret = func(1)
print(ret)
```
### 万能参数的装饰器

``` python
def wrapper(func):
	def inner(*argc,**kwargc) :
		ret = func(*argc,**kwargc)
		return ret
	return inner

@wrapper
def multi_args() :
	print(1,3,4,6,7,9)
@wrapper
def multi_args1(a,b) :
	print(a,b)
@wrapper
def multi_args2(list_num) :
	print(list_num)
multi_args()
multi_args1(3,5)
multi_args2([4,5,7,8,9,10])
```
输出的结果如下：
> 1 3 4 6 7 9
3 5
[4, 5, 7, 8, 9, 10]
### 两个有用的宏
1 函数名.__name__  查看字符串格式的函数名
2 函数名.__doc__    #document 查看函数的注释
``` python
from functools import wraps
def wrapper(func):  #func = holiday
    @wraps(func)
    def inner(*args,**kwargs):
        print('在被装饰的函数执行之前做的事')
        ret = func(*args,**kwargs)
        print('在被装饰的函数执行之后做的事')
        return ret
    return inner

@wrapper   #holiday = wrapper(holiday)
def holiday(day):
    '''这是一个放假通知'''
    print('全体放假%s天'%day)
    return '好开心'

print(holiday.__name__)
print(holiday.__doc__)
ret = holiday(3)   #inner
print(ret)
```
结果如下：

> holiday
这是一个放假通知
在被装饰的函数执行之前做的事
全体放假3天
在被装饰的函数执行之后做的事
好开心

![代码执行顺序详解](http://futuretechx.com/wp-content/uploads/2018/11/20181104212152.png)

### 装饰器的进阶
##### 1 带参数的装饰器
假如你有成千上万个函数使用了一个装饰器，现在你想把这些装饰器都取消掉，你要怎么做？一个一个的取消掉？ 没日没夜忙活3天。。。过两天你领导想通了，再让你加上。。。

``` python
import time
FLAGE = False
def timmer_out(flag):
    def timmer(func):
        def inner(*args,**kwargs):
            if flag:
                start = time.time()
                ret = func(*args,**kwargs)
                end = time.time()
                print(end-start)
                return ret
            else:
                ret = func(*args, **kwargs)
                return ret
        return inner
    return timmer
# timmer = timmer_out(FLAGE)
@timmer_out(FLAGE)    #wahaha = timmer(wahaha)
def wahaha():
    time.sleep(0.1)
    print('wahahahahahaha')

@timmer_out(True)
def erguotou():
    time.sleep(0.1)
    print('erguotoutoutou')

wahaha()
erguotou()
```
结果如下：

> wahahahahahaha
erguotoutoutou
0.10090804100036621

##### 多个装饰器装饰同一个函数

``` python
#多个装饰器装饰一个函数
def wrapper1(func):
    def inner1():
        print('wrapper1 ,before func')
        ret = func()
        print('wrapper1 ,after func')
        return ret
    return inner1

def wrapper2(func):
    def inner2():
        print('wrapper2 ,before func')
        ret = func()
        print('wrapper2 ,after func')
        return ret
    return inner2

def wrapper3(func):
    def inner3():
        print('wrapper3 ,before func')
        ret = func()
        print('wrapper3 ,after func')
        return ret
    return inner3

@wrapper3
@wrapper2
@wrapper1
def f():
    print('in f')
    return '哈哈哈'

print(f())
```
执行的结果如下：

> wrapper3 ,before func
wrapper2 ,before func
wrapper1 ,before func
in f
wrapper1 ,after func
wrapper2 ,after func
wrapper3 ,after func
哈哈哈

![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/20181104212226.png)

### 总结：
###### 装饰器的主要功能和装饰器的固定结构
装饰器的主要功能：
在不改变函数调用方式的基础上在函数的前、后添加功能。添加功能的这部分就在装饰器中

装饰器的固定格式：

``` python
def timer(func):
    def inner(*args,**kwargs):
        '''执行函数之前要做的'''
        re = func(*args,**kwargs)
        '''执行函数之后要做的'''
        return re
    return inner

from functools import wraps

def deco(func):
    @wraps(func) #加在最内层函数正上方
    def wrapper(*args,**kwargs):
        return func(*args,**kwargs)
    return wrapper
```
![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/20181104212236.png)