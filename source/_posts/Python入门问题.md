title: Python入门问题
author: Lightfish
toc: true
comment: true
tags:
  - Python
  - Python基础
categories:
  - Python
date: 2018-12-04 22:35:40
---
# Python基础要点一

### 1.一行代码实现1--100之和
```
sum(range(101))
```

![img](https://lightfisher.github.io/img/Python_question/1.jpg)

<!-- more -->
### 2.如何在一个函数内部修改全局变量
利用`global`修改全局变量<br>

![global](https://lightfisher.github.io/img/Python_question/2.jpg)


### 3.列出5个Python的标准库
* `os`: 提供了不少于操作系统相关联的函数
* `sys`: 通常用于命令行参数
* `re`: 正则匹配
* `math`: 数学运算
* `datetime`: 处理日期时间

### 4.字典如何删除键和合并两个字典
    删除用 del,合并用 update
```
dic = {'name':'qg','age':18}
del dic['name']
dic2 = {'name':'fh'}
dic.update(dic2)
```
<br>
![del update](https://lightfisher.github.io/img/Python_question/3.jpg)
<br>

### 5.谈下python的GIL
* GIL是Python的全局解释器锁，同一个进程加入由多个线程运行，一个线程在运行python程序的时候会霸占python解释器(加了一个锁即GIL)
，使进程内的其他线程无法运行，等该线程运行完后其他线程才能运行。如果线程运行过程中遇到耗时操作，则解释器锁解开，使其他线程
运行。所以在多线程中，线程的运行仍是有先后顺序，并不是同时运行。
* 多进程中因为每个进程都能被喜用分批资源，相当于每个进程有了个python解释器，多以多进程可以实现多个进程的同时运行，缺点是金城系统资源开销大

### 6.python实现列表去重的方法
>熟悉使用`set`

```
list=[np.random.randint(10,15) for _ in range(10)]
print(list)
a = set(list)
print(a)
[i for i in a]
```
<br>
![set](https://lightfisher.github.io/img/Python_question/6.jpg)
<br>
### 7.fun(*args,**kwargs)中*args，**kwargs是什么意思？
* *args和*kwargs主要用于函数的定义。你可以将不定数量的参数传递给一个函数。这里的不定的意思是：预先并不知道，函数使用者会传递多少个参数给你，所以在这个场景下使用这两个关键字。*args是用来发送一个非键值对的可变数量的参数列表给一个函数。这里有一个例子

```
def demo(args_f,*args_v):
    print(args_f)
    for x in args_v:
        print(x)
demo('a','b','c','d',e')
```
<br>
![*args](https://lightfisher.github.io/img/Python_question/7.jpg)
<br>
* **kwargs 允许你将不定长度的键值对传递给一个函数。如果你想要一个函数里处理带名字的参数，你因该使用**kwargs，这里有一个例子

```
def demo(**args_v):
    for k,v in args_v.items():
        print(k,v)
demo(name='light',name='fish)
```
<br>
![*kwargs](https://lightfisher.github.io/img/Python_question/7-2.jpg)
<br>

### 8.python2和python3的range的区别

>python2返回一个列表，python3返回一个迭代器，节约内存


### 9.一句话解释什么样的语言能过用装饰器

>函数可以作为参数传递的语言，可以使用装饰器


### 10.python内建函数类型有哪些
* 整型 -- `int`
* 布尔型 -- `bool`
* 字符串 -- `str`
* 列表 -- `list`
* 元组 -- `tuple`
* 字典 -- `dict`
* 集合 -- `set`

### 11.简述面向对象中__new__和__init__的区别
* __init__是初始化方法，创建对象后，就立刻被默认调用，相当于C语言的构造函数，可接受参数，如下图：
<br>
![__init__](https://lightfisher.github.io/img/Python_question/11-1.jpg)
<br>

* __new__至少要有一个参数cls，代表是当前类，此参数在实例化的时候由Python解释器自动识别
* __new__必须要有返回值，返回实例化出来的实例，这点在自己实现__new__时要特别注意，可以return父类(通过super(当前类，cls)) __new__出来的实例，或者直接是object的__new__出来的实例
* __init__有一个参数self,就是这个__new__返回的实例，__init__在__new__的基础上可以完成一些其他初始化的动作，__init__不需要返回值
* 如果__new__创建的是当前类的实例，会自动调用__init__函数，通过return语句里面调用__new__函数的第一个参数cls来保证是当前类实例，如果是其他类的类名；那么实际创建返回的就是其他类的实例，其实就不会调用当前类的__init__函数，也不会调用其他类的__init__函数
<br>
```
class Test(object):
    def __init__(self):
        print('这是 init 方法',self)
    def __new__(cls):
        print('这是cls的ID',id(cls))
        print('这是 new 方法',object.__new__(cls))
        return object.__new__(cls)
Test()
print('这是A的ID',id(Test))
```

![__new__](https://lightfisher.github.io/img/Python_question/11.jpg)

### 12.列表[1,2,3,4,5],请使用map函数输出[1,4,9,16,25],并使用列表推导式提取出大于10的数
* `map()`函数的第一个参数是fun
* `map()`生成的生成器，只能使用一次
```
list1 = list(range(1,6))
res = map(lambda x: x**2,list1)
res_list = [i for i in res if i > 10]
```
![map](https://lightfisher.github.io/img/Python_question/12.jpg)

### 13.python中生成随机数的若干方法
* random.uniform(a,b) 闭区间取浮点数,a,b可换序
* random.randint(q,b) 闭区间取整型数，a,b不可换序
* random.randrange(a,b,c) b开,取a向上递增2数的随机数
* random.choice('12345asd?"') 随机取数
* random.sample('abcdefg',3) 随机取三个数

### 14.避免转义给字符串加什么字符表示原是字符串？
* `r`,表示需要原始字符串

### 15.python中断言的方法
* assert()方法，断言成功程序继续运行，断言失败，则程序报错
![assert](https://lightfisher.github.io/img/Python_question/15.jpg)

### 16.数据库中student有重复的name，消除重复，请写sql语句
    select distinct name from studnet
    
### 17.10个Linux常用命令
    ls pwd cd touch rm mkdir tree cp mv cat vi more echo grep

### 18.python2和python3的区别?
* Python3使用print必须要用小括号包裹打印内容，Python2可以使用小括号也可以空格
* Python2 range(10) 返回的实列表，Python3返回的是迭代器，节约内存
* Python2中使用ascii编码，Python3中使用utf-8编码
* Python3中str表示字符串序列，byte表示字节序列
* Python2中unicode表示字符串序列，str表示字节序列
* Python2为了正常显示中文，要coding申明，Python3不需要
* Python2是raw_input(),Python 是input()

### 19.列出Python中可变数据和不可变数据类型，并简述原理
* 不可变数据类型：数值型、字符串型string和元组tuple
不允许变量的值发生变化，如果改变了变量的值，相当于创建了一个对象，而对于相同的值的对象，在内存中则只有一个对象(一个地址)<br>
![assert](https://lightfisher.github.io/img/Python_question/19.jpg)
* 可变数据类型：列表list和字典dict；
允许变量的值发生变化，而不会新建一个对象，变量引用的对象的地址也不会发生变化，不过对于相同的值的不同对象，在内存中则会存在不同的对象，即每个对象都有自己的地址，相当于内存中对于同值的对象保存了多份，这里不存在引用计数，是实实在在的对象<br>
![assert](https://lightfisher.github.io/img/Python_question/20.jpg)

### 20.去重并从小到大排序输出
* 相信你肯定学过`set`集合，`set`是可以实现去重的，不失为一种好的方法，然后利用sort方法进行排序，默认参数reverse = False就是从小到大排序，为True，是从大到小
* list是可变数据类型，所以list.sort()没有返回值，所以注释掉的代码写法不正确
```
s = 'amnshgisabcd'
s = set(s)
s = list(s)
s.sort()
# s = s.sort()
res = ''.join(s)
```
* 利用集合或者生成器解决问题，去重并保持顺序
```
def dupe(items):
	seen = set() #创建一个空的集合
      for item in items:
         if item not in seen:
     	   yield item
            seen.add(item)
a = [1,3,6,1,8,1,5]
list(dupe(a))
```

![yield](https://lightfisher.github.io/img/Python_question/21.jpg)

* 消除元素不可哈希：如字典类型

```
def rem(items, key=None):
    seen = set()  # 创建一个空的集合
    for item in items:
        va = item if key is None else key(item)
        if va not in seen:
            yield item
            seen.add(va)
a = [{'x':1, 'y':2}, {'x':1,'y': 3}, {'x':1, 'y':2}, {'x':2, 'y':4}]
list(rem(a, key=lambda d: (d['x'],d['y'])))
```
![set](https://lightfisher.github.io/img/Python_question/22.jpg)

### 21.lambda的基本使用，字典根据键值从小到大排序，用sorted函数
```
dict1 = {'name': 'zs', 'age': 18, 'city': '杭州', 'tel': '1234'}
list1 = sorted(
    dict1.keys(),
    key=lambda d: d[0],
    reverse=False)  # reverse 为True是降序
print(list1)
print(dict1.items())
print(dict1.keys())
print(dict1.values())
```
![img](https://lightfisher.github.io/img/Python_question/23.jpg)

### 22.利用collections库的Counter方法统计字符串每个单词的出现次数
```
from collections import Counter
a = 'amsjdasduqwenasdlaqiasmd'
res = Counter(a)
print(res)
```
![collection](https://lightfisher.github.io/img/Python_question/24.jpg)

### 23.filter函数的简单用法
* a = list(range(1,10)) 求出所有奇数，并构造新列表
```
a = list(range(1,10))
newlist = [i for i in filter(lambda x: x % 2, a)]
print(newlist)
```

![filter](https://lightfisher.github.io/img/Python_question/25.jpg)

### 24.列表推导式求上述问题
```
a = list(range(1, 10))
newlist = [i for i in a if i % 2 == 1]
print(newlist)
```

### 25. (1,)、(1)、("1")分别是什么类型

* (1) 是int类型
* ("1") 是str类型
* (1,) 是元组类型