# Class Basics


## Address

```python
class MyClass:
    var = 10

this_obj = MyClass()
that_obj = MyClass()

print(this_obj)
print(that_obj)

print(this_obj == that_obj)  # False

print(id(this_obj.var))
print(id(that_obj.var))


print(id(MyClass.var))


print(id(this_obj.var) == id(that_obj.var)) # True

```


this_obj 与 that_obj 是不一样的，但是 他们的var 确实在一个内存地址,其实就是 MyClass.var 的地址


## Self

```
class MyClass:

    def dothis(self):
        print('doing this')
```

`self` is the instance upon which the method is called


## Valiables

```
import random

class MyClass:

    class_val = 10  # class valiable 类变量

    def create_instance_value(self):
        self.instance_val = random.randomint(1, 10) # instance valiable 实例变量
```

特殊的__v

```python
class MyClass:

    def set_v(self, val):
        self.__v = val

    def get_v(self):
        return self.__v

a = MyClass()

a.set_v(1)
a.get_v()      # 1

a.__v = 12
a.get_v()      # 1

a.__v          # 12
a._MyClass__v  # 1

class MyClass:

    def set_v(self, val):
        self._v = val

    def get_v(self):
        return self._v

a = MyClass()

a.set_v(1)
a.get_v()      # 1

a._v = 12
a.get_v()      # 12

a._v           # 12
```


## Constructor

__init__ 作用:

1. 初始化 实例变量
2. 检查 比如服务器是否连通之类的 可靠性检查 ping


## MRO

简单的，可以使用 类.mro() 方法快速的查看会出现哪个方法

先深度优先，如果有实现 method 就返回了， 如果是两个继承自同一个父类， 那这个父类之前会遍历它所有的子类 再去查找它


## classmethod & staticmethod

1. instance method 就是 self 的，要用到 实例变量
2. classmethod 就是 cls， 不用实例变量 但是需要 用到 类变量
3. staticmethod 其实连类变量都不用，其实跟外面的函数没啥区别
(independent with class and instance value)
就是这个类单独用到的 utility 方法可以用 staticmethod 类建


## Abstract Class

常用来定义 interface 或者  methods must be implemented by subclass

```python
import abc

class GetterSetter:

    __metaclass__ = abc.ABCMeta

    @abc.abstractmethod
    def set_val(self, input):
        """ Set a value in the instance """
        return

    @abc.abstractmethod
    def get_val(self):
        """ Get and return a value from the instance """
        return
```

## Core Syntax(Magic Methods)

'abc' in var =>  var.__contains__('abc')
var == 'abc' =>  var.__eq__('abc')
var[1]       =>  var.__getitem__(1)
var[1:3]     =>  var.__getslice__(1,3)
len(var)     =>  var.__len__()
print var    =>  var.__repr__()

## __slots__

__slots__ can define allowable attributes

* saves memory by defining attributes ahead of time
* should not be used to limit attributes   not pythonic

## Variable Naming

Public:  `regular_lower_case`
Private (internal use by class or module): `_single_leading_underscore`
Private (shouldn't be subclass): `_double_leading_underscore`
Magic: `__double_underscores__`  use them don't create them

## with context

```python
class MyClass:

    def __enter__(self):
        print('we have entered "with"')
        return self

    def __exit__(self, type, value, traceback):
        print('we are leaving "with"')
        print('error type: {0}'.format(type))
        print('error value: {0}'.format(value))
        print('error traceback: {0}'.format(traceback))

    def sayhi(self):
        print('hi, instance {0}'.format(id(self)))

with MyClass() as cc:
    cc.sayhi()

# we have entered "with"
# hi, instance 4424754176
# we are leaving "with"

aa = MyClass()
aa.sayhi()

# hi, instance 4424755744
```

## pdb

一般自己用print 之类的就行了，但是遇到没有报错，但是预期结果又不对的，使用pdb

```
import pdb

values = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]

for val in values:
    mysum = 0
    mysum = mysum + val
    pdb.set_trace()        # 设置断点

print(mysum)               # 55?
```

`python3 test.py` 就会在断点前停住，然后输入你想查看的变量值，继续就按 `c` 逐行按 `n`
进入step in 看函数内部用`s`




## 写在最后

1. 类型检查 用 isinstance(val, int) 比 type(val) 好
2. getattr 可以获得 类的 attribute