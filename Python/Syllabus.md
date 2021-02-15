# 类

## Magic Methods 魔法函数

pre-defined functional methods

### `__getitem__(self, item)`

- 使得类称为可迭代的对象
- 可以做切片操作 `self.var[item] 意为 self.var[::2]`，实现的时候注意，返回值应该是相同的class类型
- 获取第item个的数据。`self.var[item] 意为 self.var[0]`

```python
import numbers
def __getitem__(self, item):
    cls = type(self)
    if isinstance(item, slice):
        return cls(__initfunc__(var = var[item]))
    elif isinstance(item, number):
        return cls(__initfunc__(var = [var[item]]))
```



###  `__subclasshook__`

支持isinstance函数

### `__str__`

能够print

### `__enter__`和`__exit__`

支持with上下文，进入with时执行enter，退出时执行exit

### `__contains__` 

- 可使用`a in b`语句判断是否存在
- 如果定义`__getitem__`也支持in
- 两者都定义时，先用contains

### `__iadd__`

支持extend

## Abstract Base Classes

抽象基类

只定义函数名，不定义实现。blueprint for other classes。

接口的强制规定，不常用。可作为文档来阅读

### raise实现

``` python
class Base:
	def get(self, key):
		raise NotImplementedError
```

缺点：调用方法时才会出异常

### abc模块实现

```python
import abc
class Base(metaclass=abc.ABCMeta):
    @abc.abstractmethod
	def get(self, key):
		pass
```

如果没有实现方法，初始化就报异常。

### 通用抽象基类

collection.abc

## 类变量和实例变量

- 类变量：不带self。一个类一个值，所有实例公用
  - 读（先查实例，没有再查类）
    - 类名.变量名
    - 实例.变量名
  - 赋值
    - 类名.变量名 = x
    - 如果是实例.变量名，会为实例创建变量。
- 实例变量：带self。
  - 实例.变量名
- `__dict__`
  - 打印实例变量（不包含类变量）

### MRO

Method Resolution Order

通过`__mro__`打印查找顺序

- DFS：python <2
  - 菱形结构：某个子类无法覆盖父类变量
- BFS：python <2.3
  - V型结构，右边子类覆盖左边父类
- C3：python >2.3

### MIXIN模式

- 某一种类只定义单一功能实现多态，类名习惯以MIXIN结尾命名
- MINXIN类中不使用super等设计MRO的方法
- 和其他基类混合使用

## 类方法

- 静态方法
  - `@staticmethod`修饰
  - 不带self参数
  - 只能`类名.静态函数`来调用
- 类方法
  - `@classsmethod`修饰
  - 把self替换成cls，表示类本身. `cls = type(self)`
  - 需要用到类当作参数的，可以选择使用类方法，保持一致性。其他用静态方法
- 实例方法
  - 正常的self函数

### super函数

好处

- 重用父类的初始化函数

执行顺序

- MRO顺序
- super意味着调用MRO下一个类的函数

### 自省

自省：查询对象内部结构

- `object_name.__dict__`打印
  - 类的dict打印类+实例的属性
  - 实例的dict只打印实例的属性（不包含父类）
  - 通过`__dict__[a] = b`的方式，为实例添加实例属性a
- `dir(object_name)`函数
  - 列出对象所有属性

## 数据封装

### 私有属性

变量用双下划线开头。只是增加了访问难度，python是没有绝对安全的。

- 子类、实例无法直接访问
- 子类可以使用`实例变量._类名__私有属性`来访问
- 类公共方法可以访问

# 序列类型 Iterable 

都可以用for进行遍历

常用的抽象基类`from collection import abc`

## 概念

### 类型

- 容器序列：可放置任意类型
  - list、tuple、dequue
- 扁平序列：只能放置同一种类型
  - str, bytes, bytearray, array.array
- 可变序列：创建后可修改 
  - list, deque, bytearray, array
- 不可变序列
  - str, tuple, bytes

### 协议要求

抽象基类abc定义

- Serial类
  - 迭代器
- MutableSerial
  - 增删改

### 切片[start : end : step]

Slice

切片将返回一个新的序列

- 参数值（超过长度会取最大长度）
  - start 默认为0
  - end 默认为len
  - step 默认为1
    - 负数表示反向遍历
- 修改
  - a[:3] = [1, 2]
    - 将后续序列插入
  - a[::2] = [0] * (len(a)/2) 间隔插入，要求个数正好能插完，否则报错
- 删除
  - a[:3] = []
  - del a[::2] 删除偶数位数

##  协议

### +=和+

- +两边要同类型
- +=只要可迭代的类型，调用extend连接
- append是添加元素，不是连接序列

## 已排序序列bisect

### 正序插入item

`bisect.insort(var_list, item)`

### 获取数值插入的位置

- `bisect.bisect(var_list, item)`
  - 相同数值插在原数组右面
  - 等同于bisect_right
- `bisect.bisect_left(var_list, item)`
  - 相同数值插在原数组左面

## Array

array只能存放指定的数据类型，而list可以存放任意.

array使用c++实现，效率很高

```python
import array
my_array = array.array('i')
# refer to official guideline for valid 'i'
```

## List

### 列表推导式

用一行代码生成列表，性能高于列表操作

`a = [func(i) for i in A logic_block]`

### 生成器generator表达式

中括号内的是generator，可迭代

`Alist = list(Agen)`

### 字典推导式

一行代码生成字典

`mydict = {key: value for value, key in olddict.items()}`

### 集合推导式

`my_set = {key for key,value in my_dict.items()}`

# Dict

- 和list一样，都是继承collection
- 属于MutableMapping类型，实现了MutableMapping的函数
- 额外有contain，get
- 不建议继承dict和list
  - C语言实现，某些时候不会调用super方法。以至于重载函数不是一直生效
  - 如果要继承，继承这个`from collection import UserDict`

# 概念及语法使用

## Duke Type

extend，需要iterate即可

## 上下文

- 使用类的魔法函数`__enter__`和`__exit__`
- 使用类contextlib修饰函数

```python
import contextlib

@contextlib.contextmanager
def func(argv):
    # do something as __enter__
    yield {}
    # do something as __exit__
    
# usage
with func(argv) as f:
    pass
```



## isinstance优于type

- isinstance可用于继承关系的类型判断。isinstance（父类）输出True. 

## is和==的差别

- is判断两者的对象id是否相同
- == 判断的是值是否相同

## return在try模块中的执行顺序

- 先 final > try > except