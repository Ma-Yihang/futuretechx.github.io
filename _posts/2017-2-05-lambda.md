---
title: python 匿名函数和递归函数
tags: python全栈开发，匿名函数，递归函数
grammar_cjkRuby: true
---
##### 匿名函数
lambda函数也叫匿名函数，即函数没有具体的名称。是为了解决一些功能很简单需求而设计的一句话函数。如下：

``` python
#这段代码
def calc(n):
    return n**n
print(calc(10))
 
#换成匿名函数
calc = lambda n:n**n
print(calc(10))
```
![lambda语法](http://futuretechx.com/wp-content/uploads/2018/10/827651-20170802172131708-1006906954.png)
上面是我们对calc这个匿名函数的分析，下面给出了一个关于匿名函数格式的说明

> 函数名 = lambda 参数 ：返回值
> 
> #参数可以有多个，用逗号隔开
> #匿名函数不管逻辑多复杂，只能写一行，且逻辑执行结束后的内容就是返回值
> #返回值和正常的函数一样可以是任意数据类型

我们可以看出，匿名函数并不是真的不能有名字。
匿名函数的调用和正常的调用也没有什么分别。 就是 函数名(参数) 就可以了，那匿名函数有什么好处呢？

> 1 使用Python写一些执行脚本时，使用lambda可以省去定义函数的过程，让代码更加精简。
> 2 对于一些抽象的，不会别的地方再复用的函数，有时候给函数起个名字也是个难题，使用lambda不需要考虑命名的问题。
> 3 使用lambda在某些时候让代码更容易理解。

lambda函数主要和其他函数结合使用，比如下面的例子：

``` python
#有这样一个字典，怎样取得一个字典中对于的值最大的键，我们都知道max(dict)默认得到的是键的最大值（按ascii）
dic={'k1':10,'k2':100,'k3':30}
print(max(dic))
print(dic[max(dic,key=lambda k:dic[k])])

Output:
k3
100
```
一下是max的源码：
``` python
def max(*args, key=None): # known special case of max
    """
    max(iterable, *[, default=obj, key=func]) -> value
    max(arg1, arg2, *args, *[, key=func]) -> value
    
    With a single iterable argument, return its biggest item. The
    default keyword-only argument specifies an object to return if
    the provided iterable is empty.
    With two or more arguments, return the largest argument.
    """
    pass
```
第二个例子：

``` javascript
res = map(lambda x:x**2,[1,5,7,4,8])
for i in res:
    print(i)

Output:
1
25
49
16
64
```
Map 函数解析：
> Python中的map函数应用于每一个可迭代的项，返回的是一个结果list。如果有其他的可迭代参数传进来，map函数则会把每一个参数都以相应的处理函数进行迭代处理。map()函数接收两个参数，一个是函数，一个是序列，map将传入的函数依次作用到序列的每个元素，并把结果作为新的list返回。

第三个例子

``` python
res = filter(lambda x:x>10,[5,8,11,9,15])
for i in res:
    print(i)

Output:
11
15
```
Filter函数解析：
> filter()函数接收一个函数 f 和一个list，这个函数 f 的作用是对每个元素进行判断，返回 True或 False，filter()根据判断结果自动过滤掉不符合条件的元素，返回由符合条件元素组成的新list。

总结：
匿名函数一般配合map,max,min,filter,zip函数使用

##### 递归函数
递归函数的定义：在一个函数里面在调用自己本身。注意：**递归的最大深度——997**
递归函数如果不受到外力的阻止会一直执行下去。但是我们之前已经说过关于函数调用的问题，每一次函数调用都会产生一个属于它自己的名称空间，如果一直调用下去，就会造成名称空间占用太多内存的问题，于是python为了杜绝此类现象，强制的将递归层数控制在了997(只要997！你买不了吃亏，买不了上当...).拿什么来证明这个“997理论”呢？这里我们可以做一个实验：

``` python
def foo(n):
    print(n)
    n += 1
    foo(n)
foo(1)

Output:
1
.
.
.
993
994
995
996
Traceback (most recent call last):
  File "D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py", line 139, in <module>
    foo(1)
  File "D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py", line 138, in foo
    foo(n)
  File "D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py", line 138, in foo
    foo(n)
  File "D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py", line 138, in foo
    foo(n)
  [Previous line repeated 992 more times]
  File "D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py", line 136, in foo
    print(n)
RecursionError: maximum recursion depth exceeded while calling a Python object
```
由此我们可以看出，未报错之前能看到的最大数字就是997.当然了，997是python为了我们程序的内存优化所设定的一个默认值，我们当然还可以通过一些手段去修改它：

``` lisp
import sys
print(sys.setrecursionlimit(100000))
```

我们可以通过这种方式来修改递归的最大深度，刚刚我们将python允许的递归深度设置为了10w，至于实际可以达到的深度就取决于计算机的性能了。不过我们还是不推荐修改这个默认的递归深度，因为如果用997层递归都没有解决的问题要么是不适合使用递归来解决要么是你代码写的太烂了

##### 递归函数与二分查找算法
l = [2,3,5,10,15,16,18,22,26,30,32,35,41,42,43,55,56,66,67,69,72,76,82,83,88]
你观察这个列表，这是不是一个从小到大排序的有序列表呀？
如果这样，假如我要找的数比列表中间的数还大，是不是我直接在列表的后半边找就行了？
![二分查找思想](http://futuretechx.com/wp-content/uploads/2018/10/827651-20170730200049162-1549215684.png)
Code 实现：
简单版二分法
``` python
l = [2,3,5,10,15,16,18,22,26,30,32,35,41,42,43,55,56,66,67,69,72,76,82,83,88]

def func(l,aim):
    mid = (len(l)-1)//2
    if l:
        if aim > l[mid]:
            func(l[mid+1:],aim)
        elif aim < l[mid]:
            func(l[:mid],aim)
        elif aim == l[mid]:
            print("bingo",mid)
    else:
        print('找不到')
func(l,66)
func(l,6)
```
升级版二分法

``` python
def search(num,l,start=None,end=None):
    start = start if start else 0
    end = end if end is None else len(l) - 1
    mid = (end - start)//2 + start
    if start > end:
        return None
    elif l[mid] > num :
        return search(num,l,start,mid-1)
    elif l[mid] < num:
        return search(num,l,mid+1,end)
    elif l[mid] == num:
        return mid
```