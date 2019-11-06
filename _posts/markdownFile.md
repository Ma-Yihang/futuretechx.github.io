---
title: python 迭代器和生成器
tags: python,迭代器，生成器
grammar_cjkRuby: true
---
### 一 迭代器
先看一段代码，如下：

``` python
print(dir([]))   #告诉我列表拥有的所有方法
ret = set(dir([]))&set(dir({}))&set(dir(''))&set(dir(range(10)))
print(ret)  #iterable
print('__iter__' in dir(int))
print('__iter__' in dir(bool))
print('__iter__' in dir(list))
print('__iter__' in dir(dict))
print('__iter__' in dir(set))
print('__iter__' in dir(tuple))
print('__iter__' in dir(enumerate([])))
print('__iter__' in dir(range(1)))
```
输出结果如下：

> ['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
{'__repr__', '__reduce_ex__', '__delattr__', '__eq__', '__setattr__', '__hash__', '__subclasshook__', '__init__', '__len__', '__sizeof__', '__lt__', '__ne__', '__getitem__', '__contains__', '__ge__', '__getattribute__', '__dir__', '__iter__', '__class__', '__doc__', '__format__', '__le__', '__gt__', '__str__', '__init_subclass__', '__new__', '__reduce__'}
False
False
True
True
True
True
True
True

这说明list，dic，str，set，tuple，句柄（f = open()），range()，enumerate都是可迭代的（interable），内部有__iter__方法，只要是能被for循环的数据类型 就一定拥有__iter__方法,例如：
`print([].__iter__())`
一个列表执行了__iter__()之后的返回值就是一个迭代器

##### 1 可迭代协议
只要含有__iter__方法的都是可迭代的
总结一下我们现在所知道的：可以被for循环的都是可迭代的，要想可迭代，内部必须有一个__iter__方法。接着分析，__iter__方法做了什么事情呢？

``` javascript
print([1,2].__iter__())

结果
<list_iterator object at 0x1024784a8>
```
执行了list([1,2])的__iter__方法，得到了一个list_iterator，现在我们又得到了一个新名词——iterator。
##### 2 迭代器的概念和迭代器协议 
内部含有__next__和__iter__方法的就是迭代器（迭代器遵循迭代器协议：必须拥有__iter__方法和__next__方法。）

``` python
'''
dir([1,2].__iter__())是列表迭代器中实现的所有方法，dir([1,2])是列表中实现的所有方法,都是以列表的形式返回给我们的，为了看的更清楚，我们分别把他们转换成集合，
然后取差集。
'''
#print(dir([1,2].__iter__()))
#print(dir([1,2]))
print(set(dir([1,2].__iter__()))-set(dir([1,2])))

结果：
{'__length_hint__', '__next__', '__setstate__'}
```
我们看到在列表迭代器中多了三个方法，那么这三个方法都分别做了什么事呢？

``` python
iter_l = [1,2,3,4,5,6].__iter__()
#获取迭代器中元素的长度
print(iter_l.__length_hint__())
#根据索引值指定从哪里开始迭代
print('*',iter_l.__setstate__(4))
#一个一个的取值
print('**',iter_l.__next__())
print('***',iter_l.__next__())
```
输入结果：
>6
\* None
** 5
*** 6

其实在for循环中，就是在内部调用了__next__方法才能取到一个一个的值。

那接下来我们就用迭代器的next方法来写一个不依赖for的遍历。

``` python
l = [1,2,3,4]
l_iter = l.__iter__()
while True:
    try:
        item = l_iter.__next__()
        print(item)
    except StopIteration:
        break
```
##### 3怎样判断可迭代？

``` python
print('__iter__' in dir( [].__iter__())) #True
print('__next__' in dir( [].__iter__())) #True
from collections import Iterable
from collections import Iterator
print(isinstance([],Iterator))
print(isinstance([],Iterable))

class A: #自定义可迭代的数据类型
    def __iter__(self):pass
    def __next__(self):pass

a = A()
print(isinstance(a,Iterator))
print(isinstance(a,Iterable))
```

> True
True
False
True
True
True

##### 4 迭代器的一些总结：
如何迭代?
    根本上说, 迭代器就是有一个 next() 方法的对象, 而不是通过索引来计数. 当你或是一个循环机制(例如 for 语句)需要下一个项时, 调用迭代器的 next() 方法就可以获得它. 条目全部取出后, 会引发一个 StopIteration 异常, 这并不表示错误发生, 只是告诉外部调用者, 迭代完成.

    不过, 迭代器也有一些限制. 例如你不能向后移动, 不能回到开始, 也不能复制一个迭代器.如果你要再次(或者是同时)迭代同个对象, 你只能去创建另一个迭代器对象. 不过, 这并不糟糕，因为还有其他的工具来帮助你使用迭代器. 

    reversed() 内建函数将返回一个反序访问的迭代器. enumerate() 内建函数同样也返回迭代器.另外两个新的内建函数, any() 和 all() , 在 Python 2.5 中新增, 如果迭代器中某个/所有条目的值都为布尔真时，则它们返回值为真. 本章先前部分我们展示了如何在 for 循环中通过索引或是可迭代对象来遍历条目. 同时 Python 还提供了一整个 itertools 模块, 它包含各种有用的迭代器.

文件对象生成的迭代器会自动调用 readline() 方法. 这样, 循环就可以访问文本文件的所有
行. 程序员可以使用 更简单的 for eachLine in myFile 替换 for eachLine in myFile.readlines() 。

可变对象和迭代器
    记住，在迭代可变对象的时候修改它们并不是个好主意. 这在迭代器出现之前就是一个问题.
一个流行的例子就是循环列表的时候删除满足(或不满足)特定条件的项:

``` javascript

for eachURL in allURLs:
    if not eachURL.startswith(‘http://’):
        allURLs.remove(eachURL) # YIKES!!
```
除列表外的其他序列都是不可变的, 所以危险就发生在这里. 一个序列的迭代器只是记录你当前到达第多少个元素, 所以如果你在迭代时改变了元素, 更新会立即反映到你所迭代的条目上.在迭代字典的 key 时, 你绝对不能改变这个字典. 使用字典的 keys() 方法是可以的, 因为keys() 返回一个独立于字典的列表. 而迭代器是与实际对象绑定在一起的, 它将不会继续执行下去:

``` python

>>> myDict = {‘a’: 1, ‘b’: 2, ‘c’: 3, ‘d’: 4}
>>> for eachKey in myDict:
… print eachKey, myDict[eachKey]
… del myDict[eachKey]
… a 1
Traceback (most recent call last):
File “<stdin>”, line 1, in <module>
RuntimeError: dictionary changed size during iteration
```
这样可以避免有缺陷的代码.
迭代器的好处：
> 从容器类型中一个一个的取值，会把所有的值都取到。
    节省内存空间
        迭代器并不会在内存中再占用一大块内存，
            而是随着循环 每次生成一个
            每次next每次给我一个