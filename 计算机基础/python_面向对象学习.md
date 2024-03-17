# 函数和模块使用

* 函数可以声明默认参数，未提供则使用默认值
* _下划线被用作一个临时变量名，表示在循环中不需要使用该变量的值

```python
def roll_dice(n=2):
    """摇色子"""
    total = 0
    for _ in range(n):
        total += randint(1, 6)
    return total
```

* *args：函数可以接受N个参数

```python
def add(*args):
    total = 0
    for val in args:
        total += val
    return total
```

* module，在python中*.py视为一个module，通过引用使用。

# 字符串与常用数据结构

* 字符串有多个字符组成，单引号或者双引号包围起来就是一个字符串。
  * 成员函数，字符串用[]制作切片；或者用in 和 not in 来判断字符是否存在字符串中。
  * 查找某个字符所在位置，用find、rfind函数十分方便，字符串本质是N个字符的组成。

* 反斜杠"\"用来转义，\+字母来转义：如\n是换行，\t也就是制表符。
  * 相表示引号，得用转义字符\'；同理表示反斜杠，得\\\.

# 面向对象

* init是class的构造函数，self表示该class的实例对象。

* 写好class源代码，实现的时候由另外一个def函数来完成。

* class(parent_relationship)表示继承关系

* 形参由self的是实例方法，static method得有@staticmethod修饰器表达。

  * | 语言   | 关键字/参数 |                             作用                             |
    | :----- | :---------- | :----------------------------------------------------------: |
    | Java   | this        | 代表当前对象的引用，用于访问当前对象的属性和方法。可以解决实例变量和局部变量之间的命名冲突，也可以在一个对象的方法中调用其他方法。 |
    | Python | self        | 约定俗成的参数名，代表当前实例对象本身。通过在类的方法中将`self`作为第一个参数传递，可以访问实例的属性和方法。用于在类的方法中访问和操作当前实例的属性和方法。 |
    | C++    | this        | 指向当前对象的指针。通过`this`指针可以访问当前对象的成员变量和成员函数。在解决成员变量和局部变 |

```python

class Student(object):
    def __int__(self,name,age):
        self.name=name
        self.age=age
    def study(self,course_name):
        print("%s正在学习%s"%(self.name,course_name))
```

* 如果你想在类的外部调用这个方法，你可以将它定义为公有方法（不使用双下划线作为前缀），或者定义一个公有的包装方法，通过这个包装方法间接地调用私有方法
* python中没有`private`、`protected` 等关键词，于是python默认在变量、方法前面加上__（双下划线)前缀表示私有变量，不希望class外访问。
* 修饰器，@property，@setter都行

```python
class Test:
    def __init__(self,foo,name):
        self.__foo=foo
        self.__name=name
    def __bar(self):
        print(self.__foo)
        print("__bar")
        return  self.__name
    def call_bar(self):
        print(self.__foo,self.__bar())

if __name__ == '__main__':
    test=Test("hello","DZG")
    test.call_bar()
```

## 类方法！=对象方法

```python
from math import sqrt
class Triangle(object):
def __init__(self, a, b, c):
    self._a = a
    self._b = b
    self._c = c

@staticmethod
def is_valid(a, b, c):
    return a + b > c and b + c > a and a + c > b

def perimeter(self):
    return self._a + self._b + self._c

def area(self):
    half = self.perimeter() / 2
    return sqrt(half * (half - self._a) *
                (half - self._b) * (half - self._c))
```

`super()`是一个内置函数，用于调用父类的方法。它可以在子类中调用父类的构造函数、普通方法或静态方法

```python
class Student(Person):
    """学生"""
    def __init__(self,name,age,grade):
        super.__init__(name,age)
        self.grade=grade
```

`__str__`是一个特殊方法（也称为魔术方法或魔法方法），用于定义对象的字符串表示形式。它被称为对象的"to-string"方法,通过定义`__str__`方法，你可以控制对象的字符串表示形式，以便更好地展示对象的信息。这在调试、日志记录和可读性方面非常有用。

```python
def __str__(self):
    return '~~~%s奥特曼~~~\n' % self._name + \
           '生命值: %d\n' % self._hp + \
           '魔法值: %d\n' % self._mp
 class MyClass:
    def __init__(self, name):
        self.name = name

    def __str__(self):
        return f"MyClass object with name: {self.name}"
obj = MyClass("example")
print(obj)  # 输出：MyClass object with name: example
```

`__slots__`是用于定义类的实例可以拥有的属性的列表使用`__slots__`时，你需要将一个属性名称的字符串列表赋值给`__slots__`类变量。这样，类的实例将只能拥有`__slots__`中指定的属性，并且无法动态地添加其他属性。

# 参考

[python_100天速成](https://github.com/jackfrued/Python-100-Days/blob/master/Day01-15/09.%E9%9D%A2%E5%90%91%E5%AF%B9%E8%B1%A1%E8%BF%9B%E9%98%B6.md)