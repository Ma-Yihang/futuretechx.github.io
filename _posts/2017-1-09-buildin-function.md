---
title: python 内置函数大讲堂
tags: python全栈开发，内置函数
grammar_mindmap: true
renderNumberedHeading: true
grammar_code: true
---
### 内置函数
python的内置函数截止到python版本3.6.2，现在python一共为我们提供了68个内置函数。它们就是python提供给你直接可以拿来使用的所有函数。那今天我们就一起来认识一下python的内置函数。
![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/15421040091.png)
    上面就是内置函数的表，68个函数都在这儿了。这个表的顺序是按照首字母的排列顺序来的，你会发现都混乱的堆在一起。比如，oct和bin和hex都是做进制换算的，但是却被写在了三个地方。。。这样非常不利于大家归纳和学习。那我把这些函数分成了6大类。你看下面这张图：
![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/func1.png)
上图中，标红的四大块有56个方法。今天先学习这些。
##### 作用域相关的函数
![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/locals.png)
基于字典的形式获取局部变量和全局变量

> globals()——获取全局变量的字典
>  locals()——获取执行本方法所在命名空间内的局部变量的字典

Output：

> {'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x00F6EE30>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py', '__cached__': None}

> {'__name__': '__main__', '__doc__': None, '__package__': None, '__loader__': <_frozen_importlib_external.SourceFileLoader object at 0x00F6EE30>, '__spec__': None, '__annotations__': {}, '__builtins__': <module 'builtins' (built-in)>, '__file__': 'D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py', '__cached__': None}

##### 其他
![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/other.png)
###### eval、exec、compile
==eval() 将字符串类型的代码执行并返回结果==

``` javascript
print(eval('1+2+3+4'))
Output : 
10
```
==exec()将自字符串类型的代码执行,返回位None.==

> 此函数支持Python代码的动态执行。object必须是字符串或代码对象。如果它是一个字符串，则将该字符串解析为一组Python语句，然后执行该语句（除非发生语法错误），如果是代码对象，则只执行它。在所有情况下，执行的代码应该作为文件输入有效（请参见“参考手册”中的“文件输入”部分）。请注意，
> 即使在传递给函数的代码的上下文中，也不能在函数定义之外使用return和yield语句 exec()。返回值是None。

``` python
print(exec("1+2+3+4"))
exec("print('hello,world')")
Output:
None
hello,world
```
再看一段代码

``` python
code = '''
import os 
print(os.path.abspath('.'))
'''
code = '''
print(123)
a = 20
print(a)
'''
a = 10
exec(code,{'print':print},)
print(a)

#Ouput:
123
20
10
```
**注意：如果把exec(code,{'print':print},)改成exec(code)，则输出：123 20 20**

==compile  将字符串类型的代码编译。代码对象能够通过exec语句来执行或者eval()进行求值。==
参数说明：　　　

> 1. 参数source：字符串或者AST（Abstract Syntax Trees）对象。即需要动态执行的代码段。　　
> 
> 2. 参数 filename：代码文件名称，如果不是从文件读取代码则传递一些可辨认的值。当传入了source参数时，filename参数传入空字符即可。　　
> 
> 3. 参数model：指定编译代码的种类，可以指定为 ‘exec’,’eval’,’single’。当source中包含流程语句时，model应指定为‘exec’；当source中只包含一个简单的求值表达式，model应指定为‘eval’；当source中包含了交互式命令语句，model应指定为'single'。

``` python
>>> #流程语句使用exec
>>> code1 = 'for i in range(0,10): print (i)'
>>> compile1 = compile(code1,'','exec')
>>> exec (compile1)
1
3
5
7
9

>>> #简单求值表达式用eval
>>> code2 = '1 + 2 + 3 + 4'
>>> compile2 = compile(code2,'','eval')
>>> eval(compile2)

>>> #交互语句用single
>>> code3 = 'name = input("please input your name:")'
>>> compile3 = compile(code3,'','single')
>>> name #执行前name变量不存在
Traceback (most recent call last):
  File "<pyshell#29>", line 1, in <module>
    name
NameError: name 'name' is not defined
>>> exec(compile3) #执行时显示交互命令，提示输入
please input your name:'pythoner'
>>> name #执行后name变量有值
"'pythoner'"
```
###### 输入输出相关的函数
==print() input==
``` python
s = input("请输入内容 ： ")  #输入的内容赋值给s变量
print(s)  #输入什么打印什么。数据类型是str
```
==print()输出==

``` python
def print(self, *args, sep=' ', end='\n', file=None): # known special case of print
    """
    print(value, ..., sep=' ', end='\n', file=sys.stdout, flush=False)
    file:  默认是输出到屏幕，如果设置为文件句柄，输出到文件
		f = open('tmp_file','w')
		print(123,456,sep=',',file = f,flush=True)
    sep:   打印多个值之间的分隔符，默认为空格
    end:   每一次打印的结尾，默认为换行符
    flush: 立即把内容输出到流文件，不作缓存
    """
```
用print打印一个进度条

``` python
import time
for i in range(0,101,2):  
     time.sleep(0.1)
     char_num = i//2      #打印多少个'*'
     per_str = '\r%s%% : %s\n' % (i, '*' * char_num) if i == 100 else '\r%s%% : %s'%(i,'*'*char_num)
     print(per_str,end='', flush=True)
#小越越  ： \r 可以把光标移动到行首但不换行
#Output(动态的):
100% : **************************************************
```
###### 数据类型相关
==type(o) 返回变量o的数据类型==

###### 内存相关
==id(o) o是参数，返回一个变量的内存地址==
==hash(o) o是参数，返回一个可hash变量的哈希值，不可hash的变量被hash之后会报错。==

``` python
t = (1,2,3)
l = [1,2,3]
print(id(t))
print(hash(t))  #可hash
print(hash(l))  #会报错
```
Output:
> 59483960
Traceback (most recent call last):
-378539185
  File "D:/Study/BaiduNetdiskDownload/day15课堂笔记/Func.py", line 30, in <module>
    print(hash(l))  #会报错
TypeError: unhashable type: 'list'

**hash函数会根据一个内部的算法对当前可hash变量进行处理，返回一个int数字。每一次执行程序，内容相同的变量hash值在这一次执行过程中不会发生改变。**
###### 文件操作相关

> open()  打开一个文件，返回一个文件操作符(文件句柄),操作文件的模式有r,w,a,r+,w+,a+
> 共6种，每一种方式都可以用二进制的形式操作(rb,wb,ab,rb+,wb+,ab+),可以用encoding指定编码,不在多说。

###### 模块操作相关

> __import__导入一个模块

###### 帮助方法

> 在控制台执行help()进入帮助模式。可以随意输入变量或者变量的类型。输入q退出
> 或者直接执行help(o)，o是参数，查看和变量o有关的操作。。。

###### 和调用相关

> callable(o)，o是参数，看这个变量是不是可调用。 如果o是一个函数名，就会返回True

``` python
def func():pass
print(callable(func))  #参数是函数名，可调用，返回True
print(callable(123))   #参数是数字，不可调用，返回False
```
###### 查看参数所属类型的所有内置方法

``` python
print(dir(list))  #查看列表的内置方法
print(dir(int))  #查看整数的内置方法
#Output:
['__add__', '__class__', '__contains__', '__delattr__', '__delitem__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__getitem__', '__gt__', '__hash__', '__iadd__', '__imul__', '__init__', '__init_subclass__', '__iter__', '__le__', '__len__', '__lt__', '__mul__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__reversed__', '__rmul__', '__setattr__', '__setitem__', '__sizeof__', '__str__', '__subclasshook__', 'append', 'clear', 'copy', 'count', 'extend', 'index', 'insert', 'pop', 'remove', 'reverse', 'sort']
['__abs__', '__add__', '__and__', '__bool__', '__ceil__', '__class__', '__delattr__', '__dir__', '__divmod__', '__doc__', '__eq__', '__float__', '__floor__', '__floordiv__', '__format__', '__ge__', '__getattribute__', '__getnewargs__', '__gt__', '__hash__', '__index__', '__init__', '__init_subclass__', '__int__', '__invert__', '__le__', '__lshift__', '__lt__', '__mod__', '__mul__', '__ne__', '__neg__', '__new__', '__or__', '__pos__', '__pow__', '__radd__', '__rand__', '__rdivmod__', '__reduce__', '__reduce_ex__', '__repr__', '__rfloordiv__', '__rlshift__', '__rmod__', '__rmul__', '__ror__', '__round__', '__rpow__', '__rrshift__', '__rshift__', '__rsub__', '__rtruediv__', '__rxor__', '__setattr__', '__sizeof__', '__str__', '__sub__', '__subclasshook__', '__truediv__', '__trunc__', '__xor__', 'bit_length', 'conjugate', 'denominator', 'from_bytes', 'imag', 'numerator', 'real', 'to_bytes']
```
##### 和数字相关
![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/number.png)
==数字——数据类型相关：bool，int，float，complex
数字——进制转换相关：bin，oct，hex
数字——数学运算：abs，divmod，min，max，sum，round，pow==

``` python
print(bin(10)) #二进制 0b1010
print(oct(10)) #八进制 0o12
print(hex(10)) #十六进制 0xa

print(abs(-5))
print(abs(5))

print(divmod(7,2))   # div出发 mod取余 (3, 1)
print(divmod(9,5))   # 除余 (1, 4)

print(round(3.14159,3)) #3.142
print(pow(2,3))   #pow幂运算  == 2**3
print(pow(3,2))
print(pow(2,3,3)) #幂运算之后再取余 2
print(pow(3,2,1)) # 0

ret = sum([1,2,3,4,5,6])
print(ret)  #21

ret = sum([1,2,3,4,5,6,10],)
print(ret) #31

print(min([1,2,3,4]))
print(min(1,2,3,4))
print(min(1,2,3,-4))
print(min(1,2,3,-4,key = abs)) #按绝对值取最小值 1

print(max([1,2,3,4]))
print(max(1,2,3,4))
print(max(1,2,3,-4))
print(max(1,2,3,-4,key = abs)) #按绝对值取最大值 -4
```
##### 和数据结构相关
![enter description here](http://futuretechx.com/wp-content/uploads/2018/11/struct.png)

==序列——列表和元组相关的：list和tuple
序列——字符串相关的：str，format，bytes，bytearry，memoryview，ord，chr，ascii，repr==

``` python
# bytes 转换成bytes类型
# 我拿到的是gbk编码的，我想转成utf-8编码
print(bytes('你好',encoding='GBK'))     # unicode转换成GBK的bytes
print(bytes('你好',encoding='utf-8'))   # unicode转换成utf-8的bytes

# 网络编程 只能传二进制
# 照片和视频也是以二进制存储
# html网页爬取到的也是编码
b_array = bytearray('你好',encoding='utf-8')
print(b_array)
print(b_array[0])
'\xe4\xbd\xa0\xe5\xa5\xbd'

OutPut:
b'\xc4\xe3\xba\xc3'
b'\xe4\xbd\xa0\xe5\xa5\xbd'
bytearray(b'\xe4\xbd\xa0\xe5\xa5\xbd')
228
```
==序列：reversed，slice==

> reversed  保留原列表，返回一个反向的迭代器

``` python
l = [1,2,3,4,5]
l.reverse()
print(l)
l = [1,2,3,4,5]
l2 = reversed(l)
print(l2)

Output:
[5, 4, 3, 2, 1]
<list_reverseiterator object at 0x014DEEB0>
```

> slice 切片，和[]效果一样

``` python
l = (1,2,23,213,5612,342,43)
sli = slice(1,5,2)
print(l[sli])
print(l[1:5:2])
```
##### 数据集合
==字典和集合：dict，set，frozenset==
==数据集合：len，sorted，enumerate，all，any，zip，filter，map==
###### filter

> filter()函数接收一个函数 f 和一个list，这个函数 f 的作用是对每个元素进行判断，返回 True或
> False，filter()根据判断结果自动过滤掉不符合条件的元素，返回由符合条件元素组成的新list。

例如，要从一个list [1, 4, 6, 7, 9, 12, 17]中删除偶数，保留奇数，首先，要编写一个判断奇数的函数：

``` javascript
def is_odd(x):
    return x % 2 == 1
```
然后，利用filter()过滤掉偶数：

``` javascript

>>>list(filter(is_odd, [1, 4, 6, 7, 9, 12, 17]))
```
Output:
> [1, 7, 9, 17]

利用filter()，可以完成很多有用的功能，例如，删除 None 或者空字符串：

``` python
def is_not_empty(s):
    return s and len(s.strip()) > 0
>>>list(filter(is_not_empty, ['test', None, '', 'str', '  ', 'END']))
>>>
结果：
['test', 'str', 'END']
```
注意: s.strip(rm) 删除 s 字符串中开头、结尾处的 rm 序列的字符。当rm为空时，默认删除空白符（包括'\n', '\r', '\t', ' ')，如下：

``` javascript
>>> a = ' 123'
>>> a.strip()
'123'

>>> a = '\t\t123\r\n'
>>> a.strip()
'123'
```
请利用filter()过滤出1~100中平方根是整数的数，即结果应该是：[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

方法：

``` python
import math
def is_sqr(x):
    return math.sqrt(x) % 1 == 0
print(list(filter(is_sqr, range(1, 101))))
结果：
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]
```
###### map

> Python中的map函数应用于每一个可迭代的项，返回的是一个结果list。如果有其他的可迭代参数传进来，map函数则会把每一个参数都以相应的处理函数进行迭代处理。map()函数接收两个参数，一个是函数，一个是序列，map将传入的函数依次作用到序列的每个元素，并把结果作为新的list返回。

有一个list， L = [1,2,3,4]，我们要将f(x)=x^2作用于这个list上，那么我们可以使用map函数处理。

``` python

>>> L = [1,2,3,4] 
>>> def pow2(x): 
... return x*x 
... 
>>> list(map(pow2,L))
[1, 4, 9, 16] 
```
注意：
**1 filter 执行了filter之后的结果集合 <= 执行之前的个数，filter只管筛选，不会改变原来的值
2 map 执行前后元素个数不变，值可能发生改变**
###### Sorted
> 对List、Dict进行排序，Python提供了两个方法 对给定的List L进行排序，
> 方法1.用List的成员函数sort进行排序，在本地进行排序，不返回副本
> 方法2.用built-in函数sorted进行排序（从2.4开始），返回副本，原始输入不变
> sorted(iterable, key=None, reverse=False)
Return a new list containing all items from the iterable in ascending order.
A custom key function can be supplied to customise the sort order, and the
reverse flag can be set to request the result in descending order.

参数说明：
	iterable：是可迭代类型;
	key：传入一个函数名，函数的参数是可迭代类型中的每一项，根据函数的返回值大小排序;
	reverse：排序规则. reverse = True  降序 或者 reverse = False 升序，有默认值。
	返回值：有序列表
	
列表按照其中每一个值的绝对值排序
``` python
l1 = [1,3,5,-2,-4,-6]
l2 = sorted(l1,key=abs)
print(l1)
print(l2)
```
列表按照每一个元素的len排序

``` javascript
l = [[1,2],[3,4,5,6],(7,),'123']
print(sorted(l,key=len))
```
注意：和sort的区别

``` python
l = [1,-4,6,5,-10]
l.sort(key = abs)   # 在原列表的基础上进行排序
print(l)

print(sorted(l,key=abs,reverse=True))      # 生成了一个新列表 不改变原列表 占内存
print(l)

l = ['   ',[1,2],'hello world']
new_l = sorted(l,key=len)
print(new_l)

结果：
[1, -4, 5, 6, -10]
[-10, 6, 5, -4, 1]
[1, -4, 5, 6, -10]
[[1, 2], '   ', 'hello world']
```

