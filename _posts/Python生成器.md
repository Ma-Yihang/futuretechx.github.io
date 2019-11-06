---
title: python 生成器
tags: python,生成器
grammar_cjkRuby: true
---
##### 生成器
Python中提供的生成器：

1.生成器函数：常规函数定义，但是，使用yield语句而不是return语句返回结果。yield语句一次返回一个结果，在每个结果中间，挂起函数的状态，以便下次重它离开的地方继续执行

2.生成器表达式：类似于列表推导，但是，生成器返回按需产生结果的一个对象，而不是一次构建一个结果列表

生成器Generator：

　　本质：生成器的本质就是迭代器(所以自带了__iter__方法和__next__方法，不需要我们去实现)

　　特点：惰性运算,开发者自定义
  
##### 生成器函数：
    含有yield关键字的函数就是生成器函数
    特点：
        1 调用函数的之后函数不执行，返回一个生成器
        2 每次调用next方法的时候会取到一个值
        3 直到取完最后一个，在执行next会报错

一个简单的code 例子如下：

``` python
import time
def genrator_fun1():
    a = 1
    print('现在定义了a变量')
    yield a
    b = 2
    print('现在又定义了b变量')
    yield b

g1 = genrator_fun1()
print('g1 : ',g1)       #打印g1可以发现g1就是一个生成器
print('-'*20)   #我是华丽的分割线
print(next(g1))
time.sleep(1)   #sleep一秒看清执行过程
print(next(g1))
```
结果如下：

> g1 :  <generator object genrator_fun1 at 0x00000227FF504888>
--------------------
现在定义了a变量
1
现在又定义了b变量
2

#####  生成器的思考和好处

	一个包含yield关键字的函数就是一个生成器函数。yield可以为我们从函数中返回值，但是yield又不同于return，return的执行意味着程序的结束，调用生成器函数不会得到返回的具体的值，而是得到一个可迭代的对象。每一次获取这个可迭代对象的值，就能推动函数的执行，获取新的返回值。直到函数执行结束。
	生成器有什么好处呢？就是不会一下子在内存中生成太多数据

假如我想让工厂给学生做校服，生产2000000件衣服，我和工厂一说，工厂应该是先答应下来，然后再去生产，我可以一件一件的要，也可以根据学生一批一批的找工厂拿。
而不能是一说要生产2000000件衣服，工厂就先去做生产2000000件衣服，等回来做好了，学生都毕业了。。。

``` python
def produce():
    """生产衣服"""
    for i in range(2000000):
        yield "生产了第%s件衣服"%i

product_g = produce()
print(product_g.__next__()) #要一件衣服
print(product_g.__next__()) #再要一件衣服
print(product_g.__next__()) #再要一件衣服
num = 0
for i in product_g:         #要一批衣服，比如5件
    print(i)
    num +=1
    if num == 5:
        break
```
结果如下：

> 生产了第0件衣服
生产了第1件衣服
生产了第2件衣服
生产了第3件衣服
生产了第4件衣服
生产了第5件衣服
生产了第6件衣服
生产了第7件衣服

###### 从生成器中取值的几个方法

 1. next
 2. for
 3. 数据类型的强制转换 : 占用内存,比如list(product_g)
 
 ##### sent 函数
1. send 获取下一个值的效果和next基本一致
2. 只是在获取下一个值的时候，给上一yield的位置传递一个数据
3. 使用send的注意事项
    第一次使用生成器的时候 是用next获取下一个值
    最后一个yield不能接受外部的值
Code :

``` python
def generator():
    print(123)
    content = yield 1
    print('=======',content)
    print(456)
    yield 2

g = generator()
ret = g.__next__()
print('***',ret)
ret = g.send('hello')   #send的效果和next一样
print('***',ret)
```
> 123
*** 1
======= hello
456
*** 2