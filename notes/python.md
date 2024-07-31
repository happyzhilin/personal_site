# Python基础相关的笔记

## python的数据类型

> **字符串型 数值型 列表 元组 字典 Bool型 集合**
>
> 数值型包括：整型int，长整型(python3版本中也是int)，浮点型float，复数型complex
>
> Bool类型只有两个值: True False
>
> 其中字符串，数值型，元组不可变类型，列表，字典和集合是可变类型
> 

> 不可变类型：python中的不可变数据类型，不允许变量的值发生变化，如果改变了变量的值，相当于是新建了一个对象，而对于相同的值的对象，在内存中则只有一个对象，内部会有一个引用计数来记录有多少个变量引用这个对象。
> 
```python
# 不可变类型，变量的值不能直接修改，要修改数据需要重新赋值，值相同的不同变量id相同
s_1 = "hello"
print(id(s_1))
s_2 = "hello"
print(id(s_2))

a = 1
print(id(a))
b = 1
print(id(b))
```
> 可变类型：python中的可变数据类型，允许变量的值发生变化，即如果对变量进行append等这种操作后，只是改变了变量的值，而不会新建一个对象，变量引用的对象的地址也不会变化，不过对于相同的值的不同对象，在内存中则会存在不同的对象，即每个对象都有自己的地址，相当于内存中对于同值的对象保存了多份，这里不存在引用计数，是实实在在的对象。
> 
```python
# 可变类型，同一个变量，值改变后变量的id不变
a_list = [1, 2]
print(id(a_list))
a_list.append(3)
print(id(a_list))
# 字典为可变类型，但是字典中的key是字符串型或是数值型，所以key是不可变类型
# 集合是不重复的元素合集，集合，列表，元组可以相互转化，集合可以快速完成列表去重
a = [1, 2, 1, 2 ,3]
list(set(a))
```

## 切片及字符串常用操作
> 支持切片的数据类型有字符串，列表，元组，这3种数据类型均是数据结构中的数组，支持下标索引。
>
> 取单个值时可直接使用下标：
 ```python
# 下标取值，0表示第一个值，-1表示最后一个值
s = "hello"
print(s[0], s[-5])
print(s[-1], s[4])
 ```
> 切片的语法为：[起始位:结束位:步长]
> 
> 范围是从起始位开始，到结束位（不包含结束位），步长为负时从后往前取值。
> 
> 要取到最后一位，结束位一般省略，步长为正时用负序号取不到最后一位。
> 
```python
# 步长为正时结束位需要序号加1，步长为负时序号减1，步长为1时可省略
# 序号可正可负，序号从0开始是正常顺序，从-1开始是倒序，是数组从后往前数
s = "abcdefg"
# 输出前3个，第一个序号为0或-7可以不写，第3个序号为2或-5，步长省略则为1是正数，"abc"
print(s[:3])
print(s[0:3])
print(s[-7:-4])
# 输出第最后3个，倒数第3个序号为4或-3，最后一个也就是第7个序号为6或-1,不写可以取到最后一个值, "efg"
print(s[4:])
print(s[4:7])
print(s[-3:])
# 输出第3，5，7个，第3个序号为2或-5，第7个也就是最后一个序号为6或-1，隔一个取值步长为2，"ceg"
print(s[2:7:2])
print(s[-5::2])
# 倒序输出倒数第1，2，3，4个,倒数第一个序号为-1可不写，倒数第4个序号为-4或3 "gfed"
print(s[:2:-1])
print(s[-1:2:-1])
print(s[-1:-5:-1])
# 倒序输出 "gfedcba"
print(s[::-1])
```
> 常用字符串操作，也就是字符串类型可调用的方法
>
> 字符串可以调用方法比如find, index, count, replace, split, capitalize, title, startswith, endswith
>
> lower, upper, lstrip, rstrip, rfind, rindex, partition, rpartition, splitilines, join等

```python
mystr = "hello world python2 and python3"
# find，find(str, start, end)反回查找到对应第一个字符的序号, 否则反回-1
# rfind 与find差不多，从右开始查找
mystr.find("python")
mystr.rfind("python")
mystr.find("python", 0, 10)
mystr.rfind("python", 0, 10)
# index，index(str, start, end)与find一样，无匹配字符串时会报异常
# rindex, 从右开始查找
mystr.index("python")
mystr.rindex("python")
#mystr.index("python", 0, 10)
# count，count(str, start, end)统计字符串在mystr中出现的次数
mystr.count("python")
mystr.count("python", 0, 10)
# replace, replace(str1, str2, mystr.count(str1))， 将str1替换成str2，默认全部替换
mystr.replace("python", "pycharm")
mystr.replace("python", "pycharm", 1)
# split split(str, maxsplit), 分隔maxsplit个子字符串，返回子字符串列表，比如空隔分隔
mystr.split(" ", 2)
# capitalize 字符串第一个字符大写
mystr.capitalize()
# title 字符串的每个单词大写
mystr.title()
# startswith, endswith, 检查是否是以某字符开头或结尾，返回True, False
mystr.startswith("hello")
mystr.startswith("Hello")
mystr.endswith("python3")
mystr.endswith("python2")
# lower, upper, 返回转换成小写和大写的字符串
mystr.lower()
mystr.upper()
# lstrip, rstrip 删除左边空白字符，删除右边空白字符
"   hello   ".lstrip()
"   hello   ".rstrip()
# strip 删除两边的空白字符
"   hello   ".strip()
# partition, rpartition 与split分隔一次相比多一个分隔的字符串，反回3字符串的列表
mystr.partition("python")
mystr.rpartition("python")
# splitlines 按行分隔，返回各行作为元素的列表
mystr="hello\nworld"
mystr
mystr.splitlines()
# join 拼接构造字符串
" ".join("abcdefg")
"_".join("abcdefg")
" ".join(["1", "2", "3", "4"])
"_".join(["1", "2", "3", "4"])
"HELLO".join(["a", "1", "b", "2"])
```

## 列表类型相关操作

> 列表遍历，可以使用for循环和while循环

```python
num = [10, 20, 30, 40]
for value in num:
    print(value)

i = 0
while i < len(num):
    print(num[i])
    i += 1
```

> 列表相关操作
>
> 添加元素有append, extend, insert
>

```python
a = [1, 2]
b = [3, 4]
a.append(b)
a
# extend会逐一添加
a.extend(b)
a
# insert(index, object)在指定位置添加元素
a = [0, 1, 2]
a.insert(1, 'hello')
a
```

> 修改和查询
>
> 修改通过标修改，查找元素相关的有in, not in, index, count

```python
# 使用下标修改列表数据
a = [1, 2, 3, 4]
a[1] = 20
a
# in, not in判断是否存在列表中，返回值为True, False
a = ['a', 'b', 'c']
'a' in a
'd' not in a
'b' not in a

# index, count用法与字符串中的方法相同

```

> 删除元素，del, pop,remove
>
> del 根据下票删除
>
> pop 删除最后一个元素
>
> remove 根据元素的值进行删除

```python
a = ['a', 'b', 'c', 'd', 'e', 'f', 'g']
a
del a[1]
a.remove('e')
a.pop()
a

```

> 排序 sort, reverse，Python列表自带排序方法
>
> 默认升序，由小到大， reverse=True时，倒序，由大到小， reverse方法是将列表逆置

```python
# a.sort()  a.reverse()都是直接修改列表数据
a = [5, 1, 4, 6, 2, 3, 7]
a
a.reverse()
a
a.sort()
a
a.sort(reverse=True)
a

# sorted()可以返回排序结果不改变原有数据
a = [5, 1, 4, 6, 2, 3, 7]
sorted(a)
sorted(a, reverse=True)
a

# 若不使用Python自带排序，可以使用双循环实现排序
a = [5, 1, 4, 6, 2, 3, 7]
for i in range(len(a)):
    for j in range(len(a)):
        if a[j] > a[i]:
            a[j], a[i] = a[i], a[j]

# 这样排序是升序，降序改成小于就行
a     

```

> 列表嵌套，列表推倒式

```python
a = [[1,2], [3, 4], [5, 6]]
a
# 列表推倒式
[x for x in range(6)]
[x for x in range(3,10) if x%2 ==0]

# 0-99分成4组
a = [x for x in range(100) ]
[a[x:x+4] for x in range(0, len(a), 4)]

```

## 元组类型相关操作

> Python元组与列表类似，不同的点就是元组的元素不能修改。元组是圆括号，列表是方括号
>
> 访问数据使用下标
>
> 元组方法count, index与字符串用法相同

```python
a = ('a', 'b', 'c', 'b')
a[0]
a.count('b')
a.index('b', 0, 2)
```

## 字典类型相关操作

>  字典每个元素组成为key:value，键：值
>
> 列表找元素是根据下标，字典找元素是根据key进行的
>
> key可以是字符和数字，尽量用字符作为key，整数作为key时容易当成是列表下标取值

```python
# 查看元素
info = {"name": "lin", "age": 18, 1:10, 1.1:100}
info["name"]
info["age"]
info[1]
info[1.1]
# 修改元素,增加元素，有key则修改，没有则新增
info["age"] = 20
info
info["mail"] = "123@qq.com"
info
# 删除 del删除一个指定元素 clear()清空
del info[1.1]
info
info.clear()
info

```

> 字典常用方法 len(), keys(), values(), items()
>
> len()返回键值对个数
>
> keys()返回包含所有key的列表
>
> values()返回包含所有值的列表
>
> items()返回包含所有（键，值）元组的列表

```python
info = {"name": "lin", "age": 18}
len(info)
info.keys()
info.values()
info.items()

# 字典遍历
for key, value in info.items():
    print(key, value)

# 有序字典OrderDict，Python3.6及以上版本默认字典就是有序字典
```

## 函数相关内容

> Python的公共方法和内置容数 
>
> 公共方法 + * in  内置函数 max(), min(), len(), del()

```python
# + * in
"abc" + "def"
[1, 2] + [3, 4]
(1, 2) + (3, 4)

"abc"*3
[1,2] * 3
(1, 2) * 3

'a' in 'abc'
3 in [1, 2, 3]
2 in (1, 2, 3)

# max 返回最在值
# min 返回最小值
# len 返回元素个数
# del 删除变量
max("hello world")
max([1, 2, 3.14 ])
max({"a": 1, "b": 2})

min("hello world")
min([1, 2, 3.14 ])
min({"a": 1, "b": 2})

len("hello world")
len([1, 2, 3, 4])
len({"name": "lin", "age": 18})

a = ['a', 'b', 'c']
b = [1, 2, 3]
del a[0]
del(b[0])
a
b

```

> 函数的定义和调用
>
> 格式：
>
> def func_name():
>
> ​	code
>
> 调用：
>
> func_name()

```python
# 无参数函数
def test():
    print("test func_name")

test()
# 有参数有返回值的函数
def add(num1, num2):
    return num1+num2

a= 2
b = 3
add(a, b)
# 定义中的用来接收参数的为形参，比如上面的num1,num2
# 调用时传入的参数为实参，传递给函数用的，比如上面的a，b


```

> 函数参数
>
> 形参中有默认值的参数称为缺省参数，缺省参数位于参数列表的最后面
>
> 处理比函数定义里更多的参数时，多的这些参数叫做不定长参数，声明时不会命名
>
> 例如：
>
> def func_name(param1, param2, *args, **kwargs):
>
> ​	code
>
> 加了*的变量args会存放所有未命名的变量参数，args为元组，也就是调用时传入的位置参数
>
> 加了**的变量kwargs会存放命名参数，也就是调用函数时传入时是key=value的参数，kwargs为字典

```python
def fun(a, b, *args, **kwargs):
    print(f"a={a}")
    print(f"b={b}")
    print(f"args: {args}")
    print(f"kwargs: {kwargs}")

fun(1, 2, 3, 4, 5, 6, x=7, y=8, z=9)
# 缺省参数也就是默认值参数放在*args **kwargs之间
"""
可以发现有的函数定义中有/ *在参数之间
help(sorted) 
Help on built-in function sorted in module builtins:

sorted(iterable, /, *, key=None, reverse=False)
    Return a new list containing all items from the iterable in ascending order.

    A custom key function can be supplied to customize the sort order, and the
    reverse flag can be set to request the result in descending order.
在/之前的参数，之能用位置参数传递
在*之后的参数，只能用关键字参数传递
在/ *之间即可以传位置参数，也可以传关键字参数
a=[2, 1, 3]
sorted(a)
如果写成sorted(iterable=a)时就会报错
"""
def fun(param1, /, param2, *, param3):
    pass

fun(1, 2, param3=3)
fun(1, param2=2, param3=3)
# fun(1, 2, 3)
# fun(param1=1, param2=2, param3=3)
"""
>>> fun(1, 2, 3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: fun() takes 2 positional arguments but 3 were given
>>> fun(param1=1, param2=2, param3=3)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: fun() got some positional-only arguments passed as keyword arguments: 'param1'

"""
```

> 函数注意事项
>
> 函数参数传递是引用传递，不是值传递
>
> 对于不可变类型，变量不能修改所以运算不会影响到变量自身
>
> 对于可变类型，函数体中的运算可能会更改传入的参数变量
>
> 函数名不能重复，函数中的变量只作用在函数中（局部变量），函数外的变量可在全部函数中使用（全局变量）
>
> 函数是否有返回值看函数中有没有return关键字，执行完return意味着调用完成，不会执行return后面的代码

```python
# 作用域，函数内改全局变理需要加global关键字
def test1():
    a = 10
    print(f"a={a}, id={id(a)}")

a = 20
print(f"a={a}, id={id(a)}")
test1()
print(f"a={a}, id={id(a)}")
# 可以看出函数内与全局变量同名不加global关键字时不能改变全局变量的值，加上global关键字才能更改
def test2():
    global a
    a = 10
    print(f"a={a}, id={id(a)}")

a = 20
print(f"a={a}, id={id(a)}")
test2()
print(f"a={a}, id={id(a)}")
# 注意使用global关键字时，在加global关键子前不能使用对应变量，否则会报错
"""
>>> def test3():
...     print(f"a={a}")
...     global a
...     a = 10
...     print(f"a={a}, id={id(a)}")
...
  File "<stdin>", line 3
SyntaxError: name 'a' is used prior to global declaration
>>> a = 20
>>> print(f"a={a}, id={id(a)}")
a=20, id=9789568
>>> test3()

"""

```

> 匿名函数以及高阶函数
>
> 匿名函数就是没有名字的单行函数，格式：
>
> lambda param1, param2, ... : 表达式或函数调用
>
> 匿名函数与普通函数的区别：
>
> 匿名函数不能使用if 语句，while循环，for循环，只能编写单行表达式或函数调用
>
> 匿名函数表达式结果就是返回结果，不用写return语句
>
> 函数的参数是函数类型，那这这样的函数就是高阶函数，比如reduce，filter，返回值是函数的也算高阶函数

```python
# reduce函数使用需要导入functools模块
import functools
# help(functools.reduce)
"""Help on built-in function reduce in module _functools:

reduce(...)
    reduce(function, sequence[, initial]) -> value

    Apply a function of two arguments cumulatively to the items of a sequence,
    from left to right, so as to reduce the sequence to a single value.
    For example, reduce(lambda x, y: x+y, [1, 2, 3, 4, 5]) calculates
    ((((1+2)+3)+4)+5).  If initial is present, it is placed before the items
    of the sequence in the calculation, and serves as a default when the
    sequence is empty.
"""

# filter函数
# help(filter)
"""Help on class filter in module builtins:

class filter(object)
 |  filter(function or None, iterable) --> filter object
 |
 |  Return an iterator yielding those items of iterable for which function(item)
 |  is true. If function is None, return the items that are true.
 |
 |  Methods defined here:
 |
 |  __getattribute__(self, name, /)
 |      Return getattr(self, name).
 |
 |  __iter__(self, /)
 |      Implement iter(self).
 |
 |  __next__(self, /)
 |      Implement next(self).
 |
 |  __reduce__(...)
 |      Return state information for pickling.
 |
 |  ----------------------------------------------------------------------
 |  Static methods defined here:
 |
 |  __new__(*args, **kwargs) from builtins.type
 |      Create and return a new object.  See help(type) for accurate signature.
"""
```

## 文件的相关操作

> 文件的读写
>
> write()可以向文件写入数据
>
> read(num)可以从文件读取数据，num表示从文件中读取的长度（单位是字节），不传则读取文件中的所有数据

```python
f = open("test.txt", "w")
f.write("hello world")
f.close()

f = open("test.txt", "r")
content = f.read(3)
print(content)
print("-"*50)
content = f.read()
print(content)
f.close()

# with语句可以自动关闭文件，不管有没有异常都能正常关闭文件
with open("test.txt", "r") as f:
    f.read()


```

> readlines() 和不传参数的read一样一次性读取文件所有内容，readlines按行方式进行一次性读取，返回一个列表，列表中的每一个元素为文件中的一行内容
>
> readline()读取一行

```python
# readlines
"""Help on built-in function readlines:

readlines(hint=-1, /) method of _io.TextIOWrapper instance
    Return a list of lines from the stream.

    hint can be specified to control the number of lines read: no more
    lines will be read if the total size (in bytes/characters) of all
    lines so far exceeds hint.
"""
# readline
"""Help on built-in function readline:

readline(size=-1, /) method of _io.TextIOWrapper instance
    Read until newline or EOF.

    Returns an empty string if EOF is hit immediately.
"""
```

> 文件常用操作
>
> 对文件的重命名，删除等操作需要导入os模块

```python
f = open("test.txt", "w")
f.write("hello world!")
f.close()

import os
# 重命名
os.rename("test.txt", "test1.txt")
# 删除
os.remove("test1.txt")
# 创建目录（文件夹）
os.mkdir("test_dir")
# 获取当前目录
os.getcwd()
# 改变默认目录
os.chdir("test_dir")
# 获取目录列表
os.mkdir("test2_dir")
os.listdir("./")
# 删除目录
os.rmdir("test2_dir")

```

## 面向对象介绍

> 如今主流软件开发的思想有：面向过程和面向对象。面向过程典型代码是C语言，面向对象典型代码是Java和C++
>
> 面向对象的3大特征：封装，继承，多态
>
> 类和对象：对象是面向对象编程的核心，在使用对象的过程中，为了将具有共同特征和行为的一组对象抽象定义，提出的一个新的概念“类”
>
> 类的构成：
>
> 类的名称，类的属性，类的方法

```python
# 定义类
class User(object):
    def info(self):
        print(f"self={self}, type={type(self)}, id={hex(id(self))}")
        print("user info")
# object是Python里的顶级父类
# 类的命名规则按照“大驼峰命名法”
# info是一个实例方法，第一个参数一般是self，表示实例对象本身，一般不换成其它名字，其作用是指向实例对象本身的变量

# 创建对象, hex()将整数转换成16进制，id()返回的内存地址是10进制显示的
lin = User()
lin.info()
print(f"user={lin}, type={type(lin)}, id={hex(id(lin))}")

""">>> # 定义类
>>> class User(object):
...     def info(self):
...         print(f"self={self}, type={type(self)}, id={hex(id(self))}")
...         print("user info")
... # object是Python里的顶级父类
... # 类的命名规则按照“大驼峰命名法”
... # info是一个实例方法，第一个参数一般是self，表示实例对象本身，一般不换成其它名字，其作用是指向实例对象本身的变量
...
>>> # 创建对象, hex()将整数转换成16进制，id()返回的内存地址是10进制显示的
>>> lin = User()
>>> lin.info()
self=<__main__.User object at 0x7f317e00d9a0>, type=<class '__main__.User'>, id=0x7f317e00d9a0
user info
>>> print(f"user={lin}, type={type(lin)}, id={hex(id(lin))}")
user=<__main__.User object at 0x7f317e00d9a0>, type=<class '__main__.User'>, id=0x7f317e00d9a0
>>>
"""
```

> `__init_(self)`方法，在创建一个对象时默认被调用，不需要手动调用，self参数不需要开发者传递，python会自动把当明的对象引用传递过去
>
> `__str__()`方法返回一个字符串，作为这个对象的描述信息，如果没有定义改函数，则打打印对象的内存地址
>
> 在类的内部获取属性和方法通过self获取，在类的外部获取属性和实例方法通过对象名获取
>
> 一个类可以创建多个对象，如果一个类有多个对象，每个对象的属性是各自保存的，都有各自独立的内存地址
>
> 实例方法是所有对象共享的，只占用人分空间，类会通过self判断是哪个对象调用了实例方法

```python
# __init__(self)方法
"""Help on wrapper_descriptor:

__init__(self, /, *args, **kwargs)
    Initialize self.  See help(type(self)) for accurate signature.
"""
# __str__()方法
"""Help on wrapper_descriptor:

__str__(self, /)
    Return str(self).
"""

```

> 继承相关笔记
>
> 继承描述的是多个类之间的所属关系，如果类A里面的属性和方法可以复用，则可以通过继承的方式，传递到类B里，A则叫基类，也叫父类，B叫派生类，也叫子类。
>
> `super()`可以逐一调用所有的父类方法，并且只执行一次

```python
class A(object):
    def __init__(self):
        self.num = 20
    
    def print_num(self):
        print(self.num + 2)

class B(A):
    pass

b = B()
print(b.num)
b.print_num()

""">>> class A(object):
...     def __init__(self):
...         self.num = 20
...
...     def print_num(self):
...         print(self.num + 2)
...
>>> class B(A):
...     pass
...
>>> b = B()
>>> print(b.num)
20
>>> b.print_num()
22
>>>
"""
# 虽然⼦类没有定义 __init__ ⽅法初始化属性，也没有定义实例⽅法，但是⽗类有。所以只要创建⼦类的对象，就默认执⾏了那个继承过来的 __init__ ⽅法
# ⼦类在继承的时候，在定义类时，⼩括号()中为⽗类的名字
# 父类的属性、⽅法，会被继承给⼦类
```

> 三大特性：封装，继承，多态
>
> 封装的意义：
>
> 将属性和⽅法放到⼀起做为⼀个整体，然后通过实例化对象来处理
>
> 隐藏内部实现细节，只需要和对象及其属性和⽅法交互就可以了
>
> 对类的属性和⽅法增加 访问权限控制
>
> 私有权限：在属性名和⽅法名 前⾯ 加上两个下划线 __
>
> 类的私有属性 和 私有⽅法，都不能通过对象直接访问，但是可以在本类内部访问
>
> 类的私有属性 和 私有⽅法，都不会被⼦类继承，⼦类也⽆法访问
>
> 私有属性 和 私有⽅法 往往⽤来处理类的内部事情，不通过对象处理，起到安全作⽤
>
> 多态：
>
> 在需要使⽤⽗类对象的地⽅,也可以使⽤⼦类对象, 这种情况就叫多态
> ⽐如, 在函数中,我需要调⽤ 某⼀个⽗类对象的⽅法, 那么我们也可以在这个地⽅调⽤⼦类对象的⽅法
>
> 程序中实现多态
>
> 子类继承父类，重写父类中的方法，通过对象调用这个方法

```python
class A(object):
    def print_name(self):
        print("A print name")

class B(A):
    def print_name(self):
        print("B print name")

def who_print(user):
    user.print_name()

a = A()
who_print(a)
b = B()
who_print(b)
""">>> class A(object):
...     def print_name(self):
...         print("A print name")
...
>>> class B(A):
...     def print_name(self):
...         print("B print name")
...
>>> def who_print(user):
...     user.print_name()
...
>>> a = A()
>>> who_print(a)
A print name
>>> b = B()
>>> who_print(b)
B print name
>>>
"""
```

> 类属性和实例属性
>
> 如果需要在类外修改 类属性 ，必须通过 类对象 去引⽤然后进⾏修改。如果通过实例对象去引
> ⽤，会产⽣⼀个同名的 实例属性 ，这种⽅式修改的是 实例属性 ，不会影响到 类属性 ，并且之后
> 如果通过实例对象去引⽤该名称的属性，实例属性会强制屏蔽掉类属性，即引⽤的是 实例属性 ，
> 除⾮删除了该 实例属性 。

```python
# 类属性
class People(object):
	name = 'lin' # 公有的类属性
	__age = 18 # 私有的类属性

p = People()
print(p.name) # 正确
print(People.name) # 正确
print(p.__age) # 错误，不能在类外通过实例对象访问私有的类属性
print(People.__age) # 错误，不能在类外通过类对象访问私有的类属性

# 实例属性（对象属性）
class People(object):
	address = 'jiangxi' # 类属性
	def __init__(self):
		self.name = 'lin' # 实例属性
		self.age = 18 # 实例属性

p = People()
p.age = 12 # 实例属性
print(p.address) # 正确
print(p.name) # 正确
print(p.age) # 正确
print(People.address) # 正确
print(People.name) # 错误
print(People.age) # 错误

```

## 静态方法和类方法

> 类方法
>
> 是类对象所拥有的⽅法，需要⽤修饰器 @classmethod 来标识其为类⽅法，对于类⽅法，第⼀个参数必
> 须是类对象，⼀般以 cls 作为第⼀个参数（可以用别的参数名，最好就用cls），能够通过实例对象和类对象去访问
>
> 类方法还可以用来修改类属性

```python
class User(object):
    name = "lin"
    @classmethod
    def get_name(cls):
        return cls.name

u = User()
print(u.get_name())
print(User.get_name())

# 修改类属性
class User(object):
    name = "lin"
    @classmethod
    def get_name(cls):
        return cls.name
    
    @classmethod
    def set_name(cls, name):
        cls.name = name

u = User()
print(u.get_name())
print(User.get_name())
u.set_name("zhilin")
print(u.get_name())
print(User.get_name())

```

> 静态方法
>
> 需要通过修饰器` @staticmethod `来进⾏修饰，静态⽅法不需要多定义参数，可以通过对象和类来访问

## 包和模块

> `import module_name `导入模块，模块名.函数进行调用
>
> `from module_name import function_name` 可直接调用函数
>
> `as`给导入的模块起别名
>
> 模块定位
>
> 可以从sys.path中查看查找模块顺序

```python
import sys
sys.path
"""
>>> import sys
>>> sys.path
['', '/usr/lib/python38.zip', '/usr/lib/python3.8', '/usr/lib/python3.8/lib-dynload', '/home/zhilin/.local/lib/python3.8/site-packages', '/usr/local/lib/python3.8/dist-packages', '/usr/local/lib/python3.8/dist-packages/cloud_init-20.1-py3.8.egg', '/usr/lib/python3/dist-packages']
>>>
"""
```

> python每个文件都是一个模块，模块名就是文件的名字
>
> 一个目录下有`__init__.py`文件，则这个目录就是包，在里面可以放该文件里面写`__all__ = [模块名1， 模块名2]`可以在`from package_name import *`时导入`__all__`里的模块
>
> `__init__.py`控制包的导入行为，为空时不会导入包中模块，可以在该文件中编写语句，当导入时这些语句会被执行

Python有很多常用的第三方包，比如发请求用的requests，Web类框架有django, flask这些包，还有爬虫scrapy等等，import这些包时需要先安装这些包，可以下载对应文件放到site-packages目录下或者直接使用python的pip包管理工具，比如`pip install requests`会自动安装对应的包，下载较慢可以更换镜像源（比如阿里开源镜像站里搜索pip然后更换）下载。

