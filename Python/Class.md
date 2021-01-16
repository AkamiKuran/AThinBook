# 类

## Magic Methods 魔法函数

pre-defined functional methods

#### `__getitem__`

使得类称为可迭代的对象

####  `__subclasshook__`

支持isinstance函数

#### `__str__`

能够print

## Abstract Base Classes抽象基类

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

### MRO（Method Resolution Order）

通过`__mro__`打印查找顺序

- DFS：python <2
  - 菱形结构：某个子类无法覆盖父类变量
- BFS：python <2.3
  - V型结构，右边子类覆盖左边父类
- C3：python >2.3

## 类方法

- 静态方法
  - `@staticmethod`修饰
  - 不带self参数
  - 只能`类名.静态函数`来调用
- 类方法
  - `@classsmethod`修饰
  - 把self替换成cls，表示类本身
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

# Duck Type的自带函数

- extend，需要iterate即可

# 其他常用技巧

- isinstance优于type
  - isinstance使用与继承关系。isinstance（父类）输出True
- is和==的差别
  - is判断两者的对象id是否相同
  - == 判断的是值是否相同