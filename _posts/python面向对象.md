---
title: python面向对象
tags: python全栈开发，初识面向对象
grammar_cjkRuby: true
---
### 面向过程 VS 面向对象 

面向过程的程序设计的核心是过程（流水线式思维），过程即解决问题的步骤，面向过程的设计就好比精心设计好一条流水线，考虑周全什么时候处理什么东西。
**优点是：极大的降低了写程序的复杂度，只需要顺着要执行的步骤，堆叠代码即可。
缺点是：一套流水线或者流程就是用来解决一个问题，代码牵一发而动全身。**
应用场景：一旦完成基本很少改变的场景，著名的例子有Linux內核，git，以及Apache HTTP Server等。
 
面向对象的程序设计的核心是对象（上帝式思维），要理解对象为何物，必须把自己当成上帝，上帝眼里世间存在的万物皆为对象，不存在的也可以创造出来。面向对象的程序设计好比如来设计西游记，如来要解决的问题是把经书传给东土大唐，如来想了想解决这个问题需要四个人：唐僧，沙和尚，猪八戒，孙悟空，每个人都有各自的特征和技能（这就是对象的概念，特征和技能分别对应对象的属性和方法），然而这并不好玩，于是如来又安排了一群妖魔鬼怪，为了防止师徒四人在取经路上被搞死，又安排了一群神仙保驾护航，这些都是对象。然后取经开始，师徒四人与妖魔鬼怪神仙互相缠斗着直到最后取得真经。如来根本不会管师徒四人按照什么流程去取。 
面向对象的程序设计的
**优点是：解决了程序的扩展性。对某一个对象单独修改，会立刻反映到整个体系中，如对游戏中一个人物参数的特征和技能修改都很容易。
缺点：可控性差，无法向面向过程的程序设计流水线式的可以很精准的预测问题的处理流程与结果，面向对象的程序一旦开始就由对象之间的交互解决问题，即便是上帝也无法预测最终结果**。于是我们经常看到一个游戏人某一参数的修改极有可能导致阴霸的技能出现，一刀砍死3个人，这个游戏就失去平衡。
应用场景：需求经常变化的软件，一般需求的变化都集中在用户层，互联网应用，企业内部软件，游戏等都是面向对象的程序设计大显身手的好地方。
在python 中面向对象的程序设计并不是全部。
面向对象编程可以使程序的维护和扩展变得更简单，并且可以大大提高程序开发效率 ，另外，基于面向对象的程序可以使它人更加容易理解你的代码逻辑，从而使团队开发变得更从容。
了解一些名词：类、对象、实例、实例化
类：具有相同特征的一类事物(人、狗、老虎)
对象／实例：具体的某一个事物（隔壁阿花、楼下旺财）
实例化：类——>对象的过程（这在生活中表现的不明显，我们在后面再慢慢解释）

### 初识类和对象
python中一切皆为对象，类型的本质就是类，用变量表示特征，用函数表示技能，因而具有相同特征和技能的一类事物就是‘类’，对象是则是这一类事物中具体的一个。
声明：

``` python
class Person:   #定义一个人类
    role = 'person'  #人的角色属性都是人
    def __init__(self,name):
        self.name = name  # 每一个角色都有自己的昵称;
        
    def walk(self):  #人都可以走路，也就是有一个走路方法
        print("person is walking...")


print(Person.role)  #查看人的role属性
print(Person.walk)  #引用人的走路方法，注意，这里不是在调用
```

> 实例化：类名加括号就是实例化，会自动触发__init__函数的运行，可以用它来为每个实例定制自己的特征

实例化的过程就是类——>对象的过程
原本我们只有一个Person类，在这个过程中，产生了一个egg对象，有自己具体的名字、攻击力和生命值。
语法：对象名 = 类名(参数)

``` python
egg = Person('egon')  #类名()就等于在执行Person.__init__()
#执行完__init__()就会返回一个对象。这个对象类似一个字典，存着属于这个人本身的一些属性和方法。
```
查看属性&调用方法

``` python
print(egg.name)     #查看属性直接 对象名.属性名
print(egg.walk())   #调用方法，对象名.方法名()
```
关于self:self：在实例化时自动将对象/实例本身传给__init__的第一个参数，你也可以给他起个别的名字，但是不建议。

``` python
class Preson:
    def __init__( self, name, age, role, job ) :
        self.__name = name
        self.age = age
        self.role = role
        self.job = job
    def getname(self):
        return self.__name

    def setjob(self,newjob):
        self.job = newjob

cosmo=Preson('Cosmo_Ma',18,'student','Learn Python')
print(cosmo.getname(),cosmo.age,cosmo.job)

print(dir(Preson))
print(Preson.__dict__)
print(Preson.__name__)
print(Preson.__doc__)
print(Preson.__base__)
print(Preson.__bases__)
print(Preson.__module__)
print(Preson.__class__)
Output:
Cosmo_Ma 18 Learn Python
['__class__', '__delattr__', '__dict__', '__dir__', '__doc__', '__eq__', '__format__', '__ge__', '__getattribute__', '__gt__', '__hash__', '__init__', '__init_subclass__', '__le__', '__lt__', '__module__', '__ne__', '__new__', '__reduce__', '__reduce_ex__', '__repr__', '__setattr__', '__sizeof__', '__str__', '__subclasshook__', '__weakref__', 'getname', 'setjob']
{'__module__': '__main__', '__init__': <function Preson.__init__ at 0x000001A4F091DA60>, 'getname': <function Preson.getname at 0x000001A4F091D950>, 'setjob': <function Preson.setjob at 0x000001A4F091D9D8>, '__dict__': <attribute '__dict__' of 'Preson' objects>, '__weakref__': <attribute '__weakref__' of 'Preson' objects>, '__doc__': None}
Preson
None
<class 'object'>
(<class 'object'>,)
__main__
<class 'type'>
```
方法详见，非常实用
``` javascript
一：我们定义的类的属性到底存到哪里了？有两种方式查看
dir(类名)：查出的是一个名字列表
类名.__dict__:查出的是一个字典，key为属性名，value为属性值

二：特殊的类属性
类名.__name__# 类的名字(字符串)
类名.__doc__# 类的文档字符串
类名.__base__# 类的第一个父类(在讲继承时会讲)
类名.__bases__# 类所有父类构成的元组(在讲继承时会讲)
类名.__dict__# 类的字典属性
类名.__module__# 类定义所在的模块
类名.__class__# 实例对应的类(仅新式类中)
```
### 类命名空间与对象、实例的命名空间
**创建一个类就会创建一个类的名称空间，用来存储类中定义的所有名字，这些名字称为类的属性**
而类有两种属性：静态属性和动态属性

 - 静态属性就是直接在类中定义的变量 
 - 动态属性就是定义在类中的方法

==其中类的数据属性是共享给所有对象的==
在上面的code中加入静态属性：place='China'

``` lisp
print(id(cosmo.place))
print(id(Preson.place))
1579379311592
1579379311592
```
==而类的动态属性是绑定到所有对象的==

``` javascript
print(cosmo.setjob)
print(Preson.setjob)
<bound method Preson.setjob of <__main__.Preson object at 0x0000010A178707F0>>
<function Preson.setjob at 0x0000010A1786D9D8>
```
**创建一个对象/实例就会创建一个对象/实例的名称空间，存放对象/实例的名字，称为对象/实例的属性**
在obj.name会先从obj自己的名称空间里找name，找不到则去类中找，类也找不到就找父类...最后都找不到就抛出异常
类中的静态变量 可以被对象和类调用

 - 对于不可变数据类型来说，类变量最好用类名操作 
 - 对于可变数据类型来说，对象名的修改是共享的，重新赋值是独立的

### 面向对象的组合用法
==软件重用的重要方式除了继承之外还有另外一种方式，即：组合
组合指的是，在一个类中以另外一个类的对象作为数据属性，称为类的组合==

``` javascript
class Weapon:
    def prick(self, obj):  # 这是该装备的主动技能,扎死对方
        obj.life_value -= 500  # 假设攻击力是500

class Person:  # 定义一个人类
    role = 'person'  # 人的角色属性都是人

    def __init__(self, name):
        self.name = name  # 每一个角色都有自己的昵称;
        self.weapon = Weapon()  # 给角色绑定一个武器;
        
egg = Person('egon')
egg.weapon.prick() 
#egg组合了一个武器的对象，可以直接egg.weapon来使用组合类中的所有方法
```
圆环是由两个圆组成的，圆环的面积是外面圆的面积减去内部圆的面积。圆环的周长是内部圆的周长加上外部圆的周长。
这个时候，我们就首先实现一个圆形类，计算一个圆的周长和面积。然后在"环形类"中组合圆形的实例作为自己的属性来用

``` javascript
from math import pi

class Circle:
    '''
    定义了一个圆形类；
    提供计算面积(area)和周长(perimeter)的方法
    '''
    def __init__(self,radius):
        self.radius = radius

    def area(self):
         return pi * self.radius * self.radius

    def perimeter(self):
        return 2 * pi *self.radius


circle =  Circle(10) #实例化一个圆
area1 = circle.area() #计算圆面积
per1 = circle.perimeter() #计算圆周长
print(area1,per1) #打印圆面积和周长

class Ring:
    '''
    定义了一个圆环类
    提供圆环的面积和周长的方法
    '''
    def __init__(self,radius_outside,radius_inside):
        self.outsid_circle = Circle(radius_outside)
        self.inside_circle = Circle(radius_inside)

    def area(self):
        return self.outsid_circle.area() - self.inside_circle.area()

    def perimeter(self):
        return  self.outsid_circle.perimeter() + self.inside_circle.perimeter()


ring = Ring(10,5) #实例化一个环形
print(ring.perimeter()) #计算环形的周长
print(ring.area()) #计算环形的面积
```

> 用组合的方式建立了类与组合的类之间的关系，它是一种‘有’的关系,比如教授有生日，教授教python课程,当类之间有显著不同，并且较小的类是较大的类所需要的组件时，用组合比较好

### 面向对象的三大特性
#### 1 继承
继承是一种创建新类的方式，在python中，新建的类可以继承一个或多个父类，父类又可称为基类或超类，新建的类称为派生类或子类,python中类的继承分为：单继承和多继承

``` javascript
class ParentClass1: #定义父类
    pass

class ParentClass2: #定义父类
    pass

class SubClass1(ParentClass1): #单继承，基类是ParentClass1，派生类是SubClass
    pass

class SubClass2(ParentClass1,ParentClass2): #python支持多继承，用逗号分隔开多个继承的类
    pass
```
查看继承

``` javascript
>>> SubClass1.__bases__ #__base__只查看从左到右继承的第一个子类，__bases__则是查看所有继承的父类
(<class '__main__.ParentClass1'>,)
>>> SubClass2.__bases__
(<class '__main__.ParentClass1'>, <class '__main__.ParentClass2'>)
```
提示：如果没有指定基类，python的类会默认继承object类，object是所有python类的基类，它提供了一些常见方法（如__str__）的实现。

``` ruby

>>> ParentClass1.__bases__
(<class 'object'>,)
>>> ParentClass2.__bases__
(<class 'object'>,)
```
**继承与抽象（先抽象再继承）**
抽象即抽取类似或者说比较像的部分。
抽象分成两个层次： 
1.将奥巴马和梅西这俩对象比较像的部分抽取成类； 
2.将人，猪，狗这三个类比较像的部分抽取成父类。
抽象最主要的作用是划分类别（可以隔离关注点，降低复杂度）
![抽象](http://futuretechx.com/wp-content/uploads/2018/12/827651-20170809205054370-2144865424.png)
继承：是基于抽象的结果，通过编程语言去实现它，肯定是先经历抽象这个过程，才能通过继承的方式去表达出抽象的结构。
抽象只是分析和设计的过程中，一个动作或者说一种技巧，通过抽象可以得到类
![继承](http://futuretechx.com/wp-content/uploads/2018/12/827651-20170809205126886-720065307.png)
 
在开发程序的过程中，如果我们定义了一个类A，然后又想新建立另外一个类B，但是类B的大部分内容与类A的相同时我们不可能从头开始写一个类B，这就用到了类的继承的概念。通过继承的方式新建类B，让B继承A，B会‘遗传’A的所有属性(数据属性和函数属性)，实现代码重用。
> 提示：用已经有的类建立一个新的类，这样就重用了已经有的软件中的一部分设置大部分，大大生了编程工作量，这就是常说的软件重用，不仅可以重用自己的类，也可以继承别人的，比如标准库，来定制新的数据类型，这样就是大大缩短了软件开发周期，对大型软件开发来说，意义重大.

**派生**
当然子类也可以添加自己新的属性或者在自己这里重新定义这些属性（不会影响到父类），需要注意的是，一旦重新定义了自己的属性且与父类重名，那么调用新增的属性时，就以自己为准了。
在子类中，新建的重名的函数属性，在编辑函数内功能的时候，有可能需要重用父类中重名的那个函数功能，应该是用调用普通函数的方式，即：类名.func()，此时就与调用普通函数无异了，因此即便是self参数也要为其传值.
在python3中，子类执行父类的方法也可以直接用super方法.supper().函数名()

**抽象类与接口类**
**1 接口类**
继承有两种用途：
一：继承基类的方法，并且做出自己的改变或者扩展（代码重用）  
二：声明某个子类兼容于某基类，定义一个接口类Interface，接口类中定义了一些接口名（就是函数名）且并未实现接口的功能，子类继承接口类，并且实现接口中的功能

``` javascript
class Alipay:
    '''
    支付宝支付
    '''
    def pay(self,money):
        print('支付宝支付了%s元'%money)

class Applepay:
    '''
    apple pay支付
    '''
    def pay(self,money):
        print('apple pay支付了%s元'%money)

class Wechatpay:
    def fuqian(self,money): #函数名不是pay
        '''
        实现了pay的功能，但是名字不一样
        '''
        print('微信支付了%s元'%money)

def pay(payment,money):
    '''
    支付函数，总体负责支付
    对应支付的对象和要支付的金额
    '''
    payment.pay(money)


p = Wechatpay()
pay(p,200)   #执行会报错
```
接口初成：手动报异常：NotImplementedError来解决开发中遇到的问题
使用abc模块来实现接口

``` python
from abc import ABCMeta,abstractmethod

class Payment(metaclass=ABCMeta):
    @abstractmethod
    def pay(self,money):
        pass


class Wechatpay(Payment):
    def fuqian(self,money):
        print('微信支付了%s元'%money)

p = Wechatpay() #不调就报错了
```
实践中，继承的第一种含义意义并不很大，甚至常常是有害的。因为它使得子类与基类出现强耦合。
继承的第二种含义非常重要。它又叫“接口继承”。
接口继承实质上是要求“做出一个良好的抽象，这个抽象规定了一个兼容接口，使得外部调用者无需关心具体细节，可一视同仁的处理实现了特定接口的所有对象”——这在程序设计上，叫做归一化。
归一化使得高层的外部使用者可以不加区分的处理所有接口兼容的对象集合——就好象linux的泛文件概念一样，所有东西都可以当文件处理，不必关心它是内存、磁盘、网络还是屏幕（当然，对底层设计者，当然也可以区分出“字符设备”和“块设备”，然后做出针对性的设计：细致到什么程度，视需求而定）。

> 依赖倒置原则：
高层模块不应该依赖低层模块，二者都应该依赖其抽象；抽象不应该应该依赖细节；细节应该依赖抽象。换言之，要针对接口编程，而不是针对实现编程

在python中根本就没有一个叫做interface的关键字，上面的代码只是看起来像接口，其实并没有起到接口的作用，子类完全可以不用去实现接口 ，如果非要去模仿接口的概念，可以借助第三方模块：
http://pypi.python.org/pypi/zope.interface
twisted的twisted\internet\interface.py里使用zope.interface
文档https://zopeinterface.readthedocs.io/en/latest/
设计模式：https://github.com/faif/python-patterns

> 接口提取了一群类共同的函数，可以把接口当做一个函数的集合。
然后让子类去实现接口中的函数。
这么做的意义在于归一化，什么叫归一化，就是只要是基于同一个接口实现的类，那么所有的这些类产生的对象在使用时，从用法上来说都一样。
归一化，让使用者无需关心对象的类是什么，只需要的知道这些对象都具备某些功能就可以了，这极大地降低了使用者的使用难度。
比如：我们定义一个动物接口，接口里定义了有跑、吃、呼吸等接口函数，这样老鼠的类去实现了该接口，松鼠的类也去实现了该接口，由二者分别产生一只老鼠和一只松鼠送到你面前，即便是你分别不到底哪只是什么鼠你肯定知道他俩都会跑，都会吃，都能呼吸。
再比如：我们有一个汽车接口，里面定义了汽车所有的功能，然后由本田汽车的类，奥迪汽车的类，大众汽车的类，他们都实现了汽车接口，这样就好办了，大家只需要学会了怎么开汽车，那么无论是本田，还是奥迪，还是大众我们都会开了，开的时候根本无需关心我开的是哪一类车，操作手法（函数调用）都一样\

#### 2 抽象类
什么是抽象类
    与java一样，python也有抽象类的概念但是同样需要借助模块实现，抽象类是一个特殊的类，它的特殊之处在于只能被继承，不能被实例化
为什么要有抽象类
    如果说类是从一堆对象中抽取相同的内容而来的，那么抽象类就是从一堆类中抽取相同的内容而来的，内容包括数据属性和函数属性。
　 比如我们有香蕉的类，有苹果的类，有桃子的类，从这些类抽取相同的内容就是水果这个抽象的类，你吃水果时，要么是吃一个具体的香蕉，要么是吃一个具体的桃子。。。。。。你永远无法吃到一个叫做水果的东西。
    从设计角度去看，如果类是从现实对象抽象而来的，那么抽象类就是基于类抽象而来的。
　 从实现角度来看，抽象类与普通类的不同之处在于：**抽象类中有抽象方法，该类不能被实例化，只能被继承，且子类必须实现抽象方法。这一点与接口有点类似，但其实是不同的**，即将揭晓答案
在python中实现抽象类

``` python
#一切皆文件
import abc #利用abc模块实现抽象类

class All_file(metaclass=abc.ABCMeta):
    all_type='file'
    @abc.abstractmethod #定义抽象方法，无需实现功能
    def read(self):
        '子类必须定义读功能'
        pass

    @abc.abstractmethod #定义抽象方法，无需实现功能
    def write(self):
        '子类必须定义写功能'
        pass

# class Txt(All_file):
#     pass
#
# t1=Txt() #报错,子类没有定义抽象方法

class Txt(All_file): #子类继承抽象类，但是必须定义read和write方法
    def read(self):
        print('文本数据的读取方法')

    def write(self):
        print('文本数据的读取方法')

class Sata(All_file): #子类继承抽象类，但是必须定义read和write方法
    def read(self):
        print('硬盘数据的读取方法')

    def write(self):
        print('硬盘数据的读取方法')

class Process(All_file): #子类继承抽象类，但是必须定义read和write方法
    def read(self):
        print('进程数据的读取方法')

    def write(self):
        print('进程数据的读取方法')

wenbenwenjian=Txt()

yingpanwenjian=Sata()

jinchengwenjian=Process()

#这样大家都是被归一化了,也就是一切皆文件的思想
wenbenwenjian.read()
yingpanwenjian.write()
jinchengwenjian.read()

print(wenbenwenjian.all_type)
print(yingpanwenjian.all_type)
print(jinchengwenjian.all_type)

Output:
文本数据的读取方法
硬盘数据的读取方法
进程数据的读取方法
file
file
file
```
##### 抽象类与接口类
抽象类的本质还是类，指的是一组类的相似性，包括数据属性（如all_type）和函数属性（如read、write），而接口只强调函数属性的相似性。
抽象类是一个介于类和接口直接的一个概念，同时具备类和接口的部分特性，可以用来实现归一化设计 
