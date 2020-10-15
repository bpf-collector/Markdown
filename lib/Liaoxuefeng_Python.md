<!--
 * @Author       : bpf
 * @Date         : 2020-10-04 12:18:10
 * @Description  : 廖雪峰的python教程笔记
 * @LastEditTime : 2020-10-05 14:12:36
-->

# [廖雪峰](https://www.liaoxuefeng.com/wiki/1016959663602400)

## 1. 输出

``` python
>>> print('\\\t\\')
\    \
>>> print(r'\\\t\\')  #不进行转义
\\\t\\
```

## 2. 字符编码

### 2.1 Unicode编码

``` python
>>> ord('中') # ord()获取字符的整数表示
20013
>>> chr(25591) # chr()把编码转换为对应的字符
'文'
>>> '\u4e2d\u6587' # 还能使用十六进制写str
'中文'
```

### 2.2 字符串 -> 字节

> &emsp;&emsp;Python的字符串类型是str，在内存中以Unicode表示，一个字符对应若干个字节。如果在网络上传输，或保存到磁盘上，就需要把str变为以字节为单位的bytes。

``` python
>>> 'ABC'.encode('ascii') # 纯英文的str可以用ASCII、UTF-8编码为bytes，内容都是一样的
b'ABC'
>>> '中文'.encode('utf-8') # 包含中文的str只能用UTF-8编码为bytes
b'\xe4\xb8\xad\xe6\x96\x87'
```

> &emsp;&emsp;ASCII编码中，所有字符都只占1字节；UTF-8 编码中，英文占1字节，中文占3字节。

### 2.3 字节 -> 字符串

``` python
>>> b'ABC'.decode('ascii')
'ABC'
>>> b'\xe4\xb8\xad\xe6\x96\x87'.decode('utf-8')
'中文'
>>> b'\xe4\xb8\xad\xff'.decode('utf-8', errors='ignore') # 使用errors参数可以忽略错误的字节
'中'
```

## 3. 字符串

> ### %

``` python
>>> 'growth rate: %d%%' & 7
'growth rate: 7%'
```

> ### format()

``` python
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('Maty', 17.125)
'Hello, Maty, 成绩提升了 17.1%'
```

> ### f-string

``` python
>>> r = 2.5
>>> s = 3.14 * r ** 2
>>> print(f'The area of a circle with radius {r} is {s:.2f}')
The area of a circle with radius 2.5 is 19.62
```

## 4. 字典dict

> dict是无序的集合。
>
> dict的key必须是不可变对象。
>
> 查找和插入的速度极快，不会随着key的增加而变慢
>
> 需要占用大量的内存，内存浪费多

``` python
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```

## 4. 集合set

> set是无序和无重复元素的集合。

``` python
>>> s = set([1, 1, 2, 2, 3, 3])
>>> s
{1, 2, 3}
```

## 5. 函数

### 5.1 添加参数类型判断

``` python
def my_abs(x):
    if not isinstance(x, (int, float)): # 内置函数isinstance()
        raise TypeError('bad operand type')
    if x >= 0:
        return x
    else:
        return -x
```

### 5.2 默认参数

> + 先定义一个函数

``` python
def add_end(L=[]):
    L.append('END')
    return L
```

> + 再进行调用，发现还不错

``` python
>>> add_end([1, 2, 3])
[1, 2, 3, 'END']
>>> add_end(['x', 'y', 'z'])
['x', 'y', 'z', 'END']
>>> add_end()
['END']
```

> + 但是再次调用发现就不对了

``` python
>>> add_end()
['END', 'END']
>>> add_end()
['END', 'END', 'END']
```

> 【原因】：默认参数L也是一个变量，它指向对象[]，每次调用该函数，如果改变了L的内容
> > 【重点】：定义默认参数要牢记一点：默认参数必须指向不变对象！
>
> + 稍微修改以下就行了

``` python
def add_end(L=None):
    if L is None:
        L = []
    L.append('END')
    return L
```

### 5.3 可变参数

> &emsp;&emsp;**可变参数允许传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple**

``` python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum

>>> calc(1, 2)
5
>>> calc()
0
>>> nums = [1, 2, 3]
>>> calc(*nums)
14
```

### 5.4 关键字参数

> &emsp;&emsp;**关键字参数允许传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict**

``` python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)

>>> person('Michael', 30)
name: Michael age: 30 other: {}
>>> person('Adam', 45, gender='M', job='Engineer')
name: Adam age: 45 other: {'gender': 'M', 'job': 'Engineer'}
>>> extra = {'city': 'Beijing', 'job': 'Engineer'}
>>> person('Jack', 24, **extra)
name: Jack age: 24 other: {'city': 'Beijing', 'job': 'Engineer'}
```

### 5.5 命名关键字参数

> &emsp;&emsp;**命名关键字参数必须传入参数名，这和位置参数不同。如果没有传入参数名，调用将报错**

``` python
def person(name, age, *, city, job): # 定义命名关键字参数时需要一个'*'
    print(name, age, city, job)

>>> person('Jack', 24, city='Beijing', job='Engineer')
Jack 24 Beijing Engineer

def person(name, age, *args, city, job): # 定义时有可变参数可不再加'*'
    print(name, age, args, city, job)

```

### 5.6 参数组合

``` python
def f1(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)

def f2(a, b, c=0, *, d, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'd =', d, 'kw =', kw)

>>> f1(1, 2, 3, 'a', 'b', x=99)
a = 1 b = 2 c = 3 args = ('a', 'b') kw = {'x': 99}
>>> f2(1, 2, d=99, ext=None)
a = 1 b = 2 c = 0 d = 99 kw = {'ext': None}

# 很奇怪的发现还能使用tuple和dict
>>> args = (1, 2, 3, 4)
>>> kw = {'d': 99, 'x': '#'}
>>> f1(*args, **kw)
a = 1 b = 2 c = 3 args = (4,) kw = {'d': 99, 'x': '#'}
>>> args = (1, 2, 3)
>>> kw = {'d': 88, 'x': '#'}
>>> f2(*args, **kw)
a = 1 b = 2 c = 3 d = 88 kw = {'x': '#'}
```

## 6. 迭代

``` python
>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
False

>>> for i, value in enumerate(['A', 'B', 'C']):
...     print(i, value)
...
0 A
1 B
2 C
```

## 7. 列表生成式

``` python
# 直接生成列表
>>> [x * x for x in range(1, 11)]
[1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

# 加上if判断
>>> [x * x for x in range(1, 11) if x % 2 == 0]
[4, 16, 36, 64, 100]

# if...else判断
>>> [x*x if x%2==0 else 0 for x in range(1,11)]
[0, 4, 0, 16, 0, 36, 0, 64, 0, 100]

# 两层循环
>>> [m + n for m in 'ABC' for n in 'XYZ']
['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']
```

## 8. 生成器

> &emsp;&emsp;受内存限制，列表容量肯定是有限的，而且如果创建一个包含100万个元素的列表会占用很大的存储空间。
>
> &emsp;&emsp;**在Python中，这种一边循环一边计算的机制，称为生成器：generator。**

### 8.1 创建生成器：使用()

``` python
>>> L = [x * x for x in range(10)]
>>> L
[0, 1, 4, 9, 16, 25, 36, 49, 64, 81]
>>> g = (x * x for x in range(10))
>>> g
<generator object <genexpr> at 0x1022ef630>
```

### 8.2 访问生成器

&emsp;&emsp;通过`next()`函数获得generator的下一个返回值，直到计算到最后一个元素，没有更多的元素时，抛出`StopIteration`的错误。
&emsp;&emsp;通过for循环获得下一个值

### 8.3 创建生成器：yield()

``` python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'

>>> f = fib(6)
>>> f
<generator object fib at 0x104feaaa0>

>>> for n in fib(6):
...     print(n)
...
1
1
2
3
5
8
```

> `for循环`调用`generator`时，发现拿不到generator的`return语句的返回值`。如果想要拿到返回值，必须捕获`StopIteration`错误，返回值包含在`StopIteration`的`value`中

``` python
>>> g = fib(6)
>>> while True:
...     try:
...         x = next(g)
...         print('g:', x)
...     except StopIteration as e:
...         print('Generator return value:', e.value)
...         break
...
g: 1
g: 1
g: 2
g: 3
g: 5
g: 8
Generator return value: done
```

## 9. 迭代器

> + 凡是可作用于for循环的对象都是Iterable类型；
>
> + 凡是可作用于next()函数的对象都是Iterator类型，它们表示一个惰性计算的序列；
>
> + 集合数据类型如list、dict、str等是Iterable但不是Iterator，不过可以通过iter()函数获得一个Iterator对象。

``` python
# >>> 外部
for x in [1, 2, 3, 4, 5]:
    pass

# >>> 内部实现过程
# 首先获得Iterator对象:
it = iter([1, 2, 3, 4, 5])
# 循环:
while True:
    try:
        # 获得下一个值:
        x = next(it)
    except StopIteration:
        # 遇到StopIteration就退出循环
        break
```

## 10. 高阶函数

### 10.1 map函数

> &emsp;&emsp;**`map()`函数接收两个参数，一个是函数，一个是Iterable，map将传入的函数依次作用到序列的每个元素，并把结果作为新的Iterator返回。**

``` python
>>> def f(x):
...     return x * x
...
>>> r = map(f, [1, 2, 3, 4, 5, 6, 7, 8, 9])
>>> list(r)
[1, 4, 9, 16, 25, 36, 49, 64, 81]
```

### 10.2 reduce函数

> &emsp;&emsp;**`reduce`函数把一个函数作用在一个序列[x1, x2, x3, ...]上，这个函数必须接收两个参数，reduce把结果继续和序列的下一个元素做累积计算，其效果就是：**
>
> `reduce(f, [x1, x2, x3, x4]) = f(f(f(x1, x2), x3), x4)**`

``` python
>>> from functools import reduce
>>> def fn(x, y):
...     return x * 10 + y
...
>>> reduce(fn, [1, 3, 5, 7, 9])
13579
```

### 10.3 filter函数

> &emsp;&emsp;**`filter`函数也接收一个函数和一个序列，把传入的函数依次作用于每个元素，然后根据返回值是True还是False决定保留还是丢弃该元素**
> > `filter(function, iterable)`

``` python
>>> def not_empty(s): # 删除空字符
...    return s and s.strip()
...
>>> list(filter(not_empty, ['A', '', 'B', None, 'C', '  ']))
>>> ['A', 'B', 'C']

# 回数是指从左向右读和从右向左读都是一样的数，例如12321，909。请利用filter()筛选出回数
>>> def is_palindrome(n):
...    k = str(n)
...    return k == k[::-1]
...
>>> output = filter(is_palindrome, range(500, 610))
>>> print(list(output))
[505, 515, 525, 535, 545, 555, 565, 575, 585, 595, 606]
```

### 10.4 sorted函数

> &emsp;&emsp;**`sorted`函数接收一个序列，还能设置key来实现自定义排序**
> >`sorted(iterable, key=None, reverse=False)`

``` python
>>> L = [('Bob', 75), ('Adam', 92), ('Bart', 66), ('Lisa', 88)]
>>> def by_name(t):
...    return t[0]
...
>>> sorted(L, key=by_name)
[('Adam', 92), ('Bart', 66), ('Bob', 75), ('Lisa', 88)]
```

### 10.5 lanmda函数

> &emsp;&emsp;**`lambda`函数是匿名函数**

### 10.6 偏函数

> &emsp;&emsp;**`functools.partial`的作用就是，把一个函数的某些参数给固定住（也就是设置默认值），返回一个新的函数，调用这个新函数会更简单。**

&emsp;&emsp;假设要转换大量的二进制字符串，每次都传入`int(x, base=2)`非常麻烦，于是想到可以定义一个`int2()`的函数，默认把base=2传进去：

``` pytohn
def int2(n):
    return int(n, base=2)

# 这样就可以很方便使用转二进制了
>>> int2('1000000')
64
>>> int2('1010101')
85
```

&emsp;&emsp;而偏函数的好处就在这，可以直接返回函数而无需进行复杂的定义。

``` python
>>> import functools
>>> int2 = functools.partial(int, base=2)
>>> int2('1000000')
64
>>> int2('1010101')
85
```

### 10.7 装饰器

> &emsp;&emsp;**在代码运行期间动态增加功能的方式，称之为“装饰器”（Decorator）**

【待续】....

## 11. 对象

### 11.1 获取对象类型

> `type()`

### 11.2 获取对象的所有属性和方法

> `dir()`

### 11.3 操作对象状态

| 方法名 | 说明 |
| -- | -- |
| hassttr(obj, str) | 是否含有属性str |
| getsttr(obj, str, default) | 获取obj的str属性值，不存在时返回默认值default |
| setsttr(obj, str, default) | 设置obj的str属性值为default |

## 12. 类

### 12.1 给实例绑定属性

``` python
class Student(object):
    pass

>>> s = Student()
>>> s.name = 'Mike'
>>> print(s.name)
Mike
```

### 12.2 给实例绑定方法

> &emsp;&emsp;绑定一个实例的方法不能用在其他实例，除非【绑定到class】

``` python
def set_age(self, age):
    self.age = age

>>> from types import MethodType
>>> s.set_age = MethodType(set_age, s) # 给实例绑定方法
>>> s.set_age(17) # 调用实例方法
>>> print(s.set_age)
17
```

### 12.3 给类绑定方法

``` python
def set_score(self, score):
    self.score = score

>>> Student.set_age = set_age # 给类绑定方法
>>> s.set_score(100)
>>> s.score
100
```

### 12.4 限制类的属性

> &emsp;&emsp;**使用`__slots__`属性来限制类的实例能绑定的属性**

``` python
class Student(object):
    __slots__ = ('name', 'age') # 使用tuple定义允许绑定的属性名称
```

### 12.5 类似属性调用方法

``` python
class Student(object):

    def get_score(self):
         return self._score

    def set_score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0 ~ 100!')
        self._score = value

>>> s = Student()
>>> s.set_score(60) # ok!
>>> s.get_score()
60
>>> s.set_score(9999)
Traceback (most recent call last):
  ...
ValueError: score must between 0 ~ 100!
```

> &emsp;&emsp;Python内置的@property装饰器就是负责把一个方法变成属性调用

``` python
class Student(object):

    @property
    def score(self):
        return self._score

    @score.setter
    def score(self, value):
        if not isinstance(value, int):
            raise ValueError('score must be an integer!')
        if value < 0 or value > 100:
            raise ValueError('score must between 0 ~ 100!')
        self._score = value

>>> s = Student()
>>> s.score = 60 # OK，实际转化为s.set_score(60)
>>> s.score # OK，实际转化为s.get_score()
60
>>> s.score = 9999
Traceback (most recent call last):
  ...
ValueError: score must between 0 ~ 100!
```

## 13. 异常

### 13.1 捕获异常

> 语法格式：`try...except...else...finally...`

### 13.2 记录异常

&emsp;&emsp;Python内置的logging模块可以非常容易地记录错误信息，同时能让程序继续执行下去。

> 实例

``` python
import logging
def foo():
    return 10 / int(s)
def bar():
    return foo(s) * 2
def main():
    try:
        bar('0')
    except Exception as e:
        logging.exception(e)
if __name__ == '__main()__':
    main()
    print('END')
```

> 返回结果

``` bash
$ python3 err_logging.py
ERROR:root:division by zero
Traceback (most recent call last):
  File "err_logging.py", line 13, in main
    bar('0')
  File "err_logging.py", line 9, in bar
    return foo(s) * 2
  File "err_logging.py", line 6, in foo
    return 10 / int(s)
ZeroDivisionError: division by zero
END
```

### 13.3 抛出错误

> 语法格式：`raise ...`

``` python
def foo(s):
    n = int(s)
    if n==0:
        raise ValueError('invalid value: %s' % s)
    return 10 / n
def bar():
    try:
        foo('0')
    except ValueError as e:
        print('ValueError!')
        raise
if __name__ == '__main()__':
    bar()
```

## 14. 调试

### 14.1 断言

> 语法格式：`assert`
>
> 取消assert：`python -O xx.py`

### 14.2 logging

> [日志HowTo](https://docs.python.org/zh-cn/3.7/howto/logging.html)
>
> [模块logging](https://docs.python.org/zh-cn/3.7/library/logging.html)

### 14.3 调试器pdb

> 启动：`python -m pdb xx.py`
> 说明文档：[PDB](https://docs.python.org/zh-cn/3/library/pdb.html)

### 14.4 单元测试

库：`unittest`  

> 测试方法
>
> > + 输入正数，比如1、1.2、0.99，期待返回值与输入相同；
> > + 输入负数，比如-1、-1.2、-0.99，期待返回值与输入相反；
> > + 输入0，期待返回0；
> > + 输入非数值类型，比如None、[]、{}，期待抛出TypeError。

``` python
import unittest

from mydict import Dict

class TestDict(unittest.TestCase):
    def setUp(self): # 测试前运行
        print('setUp...')
    def tearDown(self): # 测试后运行
        print('tearDown...')

    def test_key(self):
        d = Dict()
        d['key'] = 'value'
        self.assertEqual(d.key, 'value')
    def test_keyerror(self):
        d = Dict()
        with self.assertRaises(KeyError):
            value = d['empty']
```

运行：

``` python
if __name__ == '__main__':
    unittest.main()

>>> python mydict_test.py
>>> python -m unittest mydict_test.py
```

## 15. IO编程

### 15.1 文件IO

### 15.2 内存IO

``` python
>>> from io import StringIO
>>> f = StringIO()
>>> f.write('hello')
5
>>> print(f.getvalue())
hello

>>> from io import BytesIO
>>> f = BytesIO(b'\xe4\xb8\xad\xe6\x96\x87')
>>> f.read()
b'\xe4\xb8\xad\xe6\x96\x87'
>>> f.getvalue().decode('utf-8')
'中文'
```

### 15.3 文件与目录

``` python
>>> import os
>>> os.name # 操作系统类型
'posix' # 'nt'是windows
>>> os.environ # 获取环境变量
>>> os.path.abspath('.') # 当前路径的绝对路径
>>> new_dir = os.path.join('E:', 'testdir') # 获取新目录的完整路径
>>> os.mkdir(new_dir) # 创建目录
>>> os.rmdir(new_dir) # 删除目录
>>> os.path.split('/Users/michael/testdir/file.txt') # 分割出目录和文件
('/Users/michael/testdir', 'file.txt')
>>> os.path.splitext('/path/to/file.txt') # 获取文件扩展名
('/path/to/file', '.txt')
>>> os.rename('test.txt', 'test.py') # 重命名文件
>>> os.remove('test.py') # 删掉文件
>>> [x for x in os.listdir('.') if os.path.isdir(x)] # 列出所有目录
>>> [x for x in os.listdir('.') if os.path.isfile(x) and os.path.splitext(x)[1]=='.py'] # 列出所有的.py文件
```


## 【其他】
>
> > + 装饰器
> > + [多继承](https://www.liaoxuefeng.com/wiki/1016959663602400/1017502939956896)
> > + [枚举类](https://www.liaoxuefeng.com/wiki/1016959663602400/1017595944503424)
> > + [元类](https://www.liaoxuefeng.com/wiki/1016959663602400/1017592449371072)
