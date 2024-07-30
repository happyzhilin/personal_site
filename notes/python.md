# Python相关的笔记

## python的数据类型

> **字符串型 数值型 列表 元组 字典 Bool型**
>
> 数值型包括：整型int，长整型(python3版本中也是int)，浮点型float，复数型complex
>
> Bool类型只有两个值: True False
>
> 其中字符串，数值型，元组不可变类型，列表可元组是可变类型
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

> 列表嵌套

```python
a = [[1,2], [3, 4], [5, 6]]
a

```

