---
title: python从入门到放弃
date: 2023-06-30 11:14:42
tags: python
---

# 一. 基础

- 编译型语言
  - 定义：在程序运行之前，源代码会先经过编译器将其转换为机器语言的形式，生成可执行文件。在运行时，计算机直接执行该可执行文件，无需再进行翻译或解释。C、C++ 和 Java 等语言属于编译型语言。
  - 白话定义：只有第一次执行的时候需要编译,之后如果没修改源代码就不会再编译了
  - 示例：C++、Go、Java
- 解释型语言
  - 定义：在程序运行时，源代码逐行解释并执行。解释器将源代码转换为机器语言，并逐行执行代码。解释型语言的代码无需编译，可以直接运行，但由于需要逐行解释执行，相对于编译型语言，解释型语言的执行速度通常较慢。
  - 白话定义：每次运行都会从第一行进行编译,编译一行执行一行
  - 示例：Python、JavaScript、Ruby 

## 1. 基中基

### 1.1. 关键字

| 关键字                                       | 涉及功能                         |
| -------------------------------------------- | -------------------------------- |
| True, False, None                            | 真 假 空                         |
| if, elif, else, and, not, assert, or, is, in | 逻辑判断                         |
| try, except, finally, raise                  | 异常捕获                         |
| for, while, continue, break, return          | 循环                             |
| from, import                                 | 导包                             |
| def, class, lambda                           | 定义函数、类、匿名函数           |
| async, await, yield                          | 异步                             |
| global, nonlocal                             | 变量空间                         |
| as, del, pass, with, type                    | 重命名、删除、PASS、上下文、类型 |

### 1.2. 逻辑运算符

- 与 `and`: 一假即假
- 或 `or`: 一真即真（注意短路逻辑： `1 or 1 / 0` 不会报错，程序只会走第一个1然后就会执行下一行）
- 非 `not`: 真假取反

### 1.3. 比较运算符

- `//` 取整除 9 // 4 = 2

- `%` 取余 9%4 = 1

- `^`   取异或  把数字转化为二进制取  0 1 为 1 ，1 0 为 1， 1 1 为1， 0 0 为 0

- `**`  幂

### 1.4. 比较运算符

- `> < == != >= <=`

- 返回的结果都是bool类型, True表示条件成立, False表示不成立.

### 1.5. 输入输出

- `print()` 调用底层的`sys.stdout.write`方法，前往控制台打印输出

- `input()`  无论输入什么类型的数据，都会转化为字符串

### 1.6. 循环

- 循环语句结合`else`语句使用，当循环语句执行了`break`表示非正常结束，`else`语句不会执行，否则会执行`else`语句

- 循环语句里有`break/return`时, `break/return`执行了, `else`语句就不会执行
- `break/continue` 只影响一层循环 

### 1.7. if三目运算

- `a if a > b else b` 条件成立取a，不成立取b

- if 除了判断bool类型, 还可以判断
  - 容器类型(字符串, 列表, 元组, 字典, 集合, `range()`, `bytes()`) 判断是否有数据
  - 非零即真(只要不是0, 条件都成立)
  - None 条件不成立, not none, 表示非空, 条件成立

### 1.8 注释

- 单行 `# 这是注释`
- 多行 `""" 这是多行注释 """`

## 2. 容器

### 2.1. 字符串

> **字符串用`join`比直接`+`高效原因**：在 Python 中，字符串是不可变类型，这意味着一旦我们创建了一个字符串对象，它就不能被修改或更新。因此，每次使用 `+` 操作符拼接字符串时，都会创建一个新的字符串对象，并将之前字符串对象的内容复制到新的字符串对象中，这个复制的操作会带来额外的内存分配和内存拷贝的开销，特别是在需要拼接大量的字符串时，会消耗大量的系统资源，导致程序运行缓慢。 相对地，使用 `join()` 方法的拼接字符串操作则更加高效。`join()` 方法本质上是将多个字符串通过指定的分隔符拼接在一起，而与此相关的方法包括 `split()`，`replace()` 和 `format()` 等方法，它们均采用类似的算法。在 `join()` 方法的实现中，Python 的解释器会先在内存中分配一个足够大的单个字符串缓冲区，然后扫描要拼接的字符串，将其复制到单个缓冲区中，并在不同字符串之间插入指定的分隔符。这种方法可以有效地避免频繁创建或拷贝字符串对象，从而提高拼接字符串的效率。 此外，`join()` 方法还可以接受一个可迭代对象作为参数，如列表，元组，生成器等，它们会返回一个字符串，其中可迭代对象按照指定的分隔符进行拼接。这种方式具有更高的灵活性和实用性，因为它可以用于拼接任意数量的字符串，而且可以用于迭代较大的数据集合，而不会导致系统资源消耗过多。

- 定义：用单引号、双引号、三引号均可，仅三引号可以换行
- 切片：` [开始位置:结束位置:步长] ` 左闭右开
  - `[::-1]` 字符串快速逆置

```python
my_str = "python"
isinstance(my_str, str)  # True

my_age = 18
isinstance(my_age, int)  # True

my_age = str(my_age)  # "18"
isinstance(my_age, str)  # True
```

**常用**

- `.find(要查询的字符, 查询开始索引, 查询结束索引)` 左闭右开，查空返回 -1
- `.replace(str1, str2, 替换次数)` 字符串替换，替换次数默认-1全部替换
- `.split(str1, 切片次数)` 字符串以 str1 为分隔符进行切片，切片次数默认-1全部切，返回分隔后的列表
- `.lower()` 英文转小写 `upper()`转大写

### 2.2. 列表

**定义**：`[]` 或 `list()` 

**列表推导式**： 列表中可以包含条件语句，表示筛选符合条件的元素。在这种情况下，底层逻辑还会涉及以下步骤：

1. 创建一个空列表。
2. 对于列表推导式中的每个元素表达式，按照迭代顺序依次执行以下步骤：
   1. 在当前作用域中计算元素表达式的值。
   2. 如果条件表达式的值为真，则将计算得到的值添加到列表中。
3. 返回最终生成的列表。

**增**

- `.append` 加整个对象，加字典也是整个字典
- `.extend` 打散加进去，加字典默认加字典的`key`
- `.insert(index, obj)` 在指定位置前面加, 是整个加进去的

**删**

- `del list[::]` 可以和切片一起操作根据索引删除列表元素

- `.pop()` 只能根据单独索引删除对应元素, 默认删最后一个, 会返回删除的元素

- `.remove()` 指定元素删除

**改**

`list[index] = "new"`  可以用切片同时更改多个数据,注意下面示例

```python
>>> my_list = [1, "2", 3]
>>> my_list[0] = "1"
>>> my_list
['1', '2', 3]
>>> my_list[:0] = "456"
>>> my_list
['4', '5', '6', '1', '2', 3]
>>> my_list[:2] = [1, 2]
>>> my_list
[1, 2, '6', '1', '2', 3]
```

**查**

- `in` 判断是否存在，只可判断最外层数据，内层还有容器要索引进去查
- `.index(obj, start, end)` 左闭右开，找不到报`ValueError`
- `.count(obj)`

**排序**

- `.sort(reverse=False)` 默认是从小到大, `reverse=True` 改为从大到小

- `.reverse()` 将列表逆置, 与上面的`reverse=True`不同

### 2.3. 元组

**定义**：`tuple()` 或 `(1, 2)`  如果只有一个元素, 逗号不能省略, 有序

### 2.4. 字典

**定义**

- `dict()` 或 `{"a": 1, "b": 2}`
- `zip`组合`key`和`value` 生成字典

```python
>>> keys = ["a", "b"]
>>> values = [1, 2]

>>> my_dict = dict(zip(keys, values))
>>> my_dict
{'a': 1, 'b': 2}
```

**增:**   

- `dict[key] = value`

**删:**   

- `del dict[key]`  必须要有`key`数据

- `.pop(key, default)`  必须要有`key`数据, 会返回所删项的`value`, 如果字典里没有这个`key`就会返回`default`

- `.popitem()`  takes no arguments, return the last item as a tuple()

- `.clear()` 清空

**改:**  

-  `dict[key] = value`  和增加元素相同, 所以当原本没有此`key`就变成增加元素了

**查:**   

- `dict[key]`  如果不存在会报错

- `.get(key, default)`   如果不存在则返回`default`  不写`default`找不到会返回`None` 不会报错

**合并:**  

- `dict1.update(dict2)`  把字典2的每个键值对数据合并到字典1中, 如果有重复的则更新1的内容

**遍历:** 

- `for key in dict.keys()`
- `for values in dict.values()`
- `for item in dict.items()`           **item是个tuple**
- `for key, value in dict.items()`         遍历 + 拆包

**排序：**

- `sorted(d.items(), key=lambda x : x[0/1])`

### 2.5. 集合

- 集合是一个容器类型, 可以存储多个数据, 但是多个数据不能重复
- 集合只能存储不可变类型数据, 也就是: 数字, 字符串, 元组    同字典的key
- 空集合不能使用**{}**来表示, {}是字典, 创建时用 **set()** 来创建空集合
- 遍历集合不能用通过下标, 可以用for遍历, 可迭代对象

**特点:**

1. 无序, so集合不能通过索引获取数据和通过索引修改数据
2. 数据不能重复,数据是唯一的
3. 可变类型

**操作符：**

**^**  补  {1，2} ^ {2, 3}  =>  {1, 3}

**&** 交  {1，2} & {2, 3}  =>  {2, }

**|**   并   {1，2} | {2, 3}  =>  {1, 2, 3}

**-**   差   {1，2} - {2, 3}  =>  {1, }

**增:**

.**add()** 重复的数据只保留一个

**删:**

**.remove(value)** 指定数据删除

### 2.6. 公共方法

| 运算符 | Python 表达式      | 结果                         | 描述           | 支持的数据类型           |
| ------ | ------------------ | ---------------------------- | -------------- | ------------------------ |
| +      | [1, 2] + [3, 4]    | [1, 2, 3, 4]                 | 合并           | 字符串、列表、元组       |
| *      | ['Hi!'] * 4        | ['Hi!', 'Hi!', 'Hi!', 'Hi!'] | 复制           | 字符串、列表、元组       |
| in     | 3 in (1, 2, 3)     | True                         | 元素是否存在   | 字符串、列表、元组、字典 |
| not in | 4 not in (1, 2, 3) | True                         | 元素是否不存在 | 字符串、列表、元组、字典 |

**python内置函数**

- `len()`  获取容器的元素数量

- `max()`  返回容器中元素最大值  |  类似的 `min()`  最小

- `enumerate()` 
  - 在使用for循环的时候可以遍历数据又可以遍历索引, 列表/元组/字典都可以使用
  - 当用于字典遍历所有items时返回的是一个索引数据和一个元组

### 2.7. 可变不可变类型

不可变类型

- 定义：不允许在原本内存空间基础上修改数据, 修改数据后内存地址会发生变化
- 示例：列表, 字典, 集合

可变类型

- 定义：允许在原本内存空间修改数据，修改后一是在原有内存空间基础上修改数据内存不变，二是重新赋值内存地址可能发生变化
- 示例：数字, 字符串, 元组  

## 3. 函数

> 程序中定义的变量都是保存在内存中的, 局部变量也是, 当函数执行结束后局部变量都会销毁,内存释放

### 3.1. 文档说明

```python
def show():
    """ func docs """
    # ''' others '''
    print("life is short i use python")


show()
help(show)
# life is short i use python
# Help on function show in module __main__:
# 
# show()
#     func docs
```

### 3.2. 返回值

- 函数不写`return` 取函数返回值时会取到 `None`
- 在多层循环中 `return` 可把多层全部终止，`break` 只能终止一层

### 3.3. 局部变量&全局变量

- 局部变量：作用域仅在函数体内部,  随着函数执行结束会销毁
- 全局变量：在函数体内外都生效，不会随着函数执行结束会销毁

- `global` 本质是表示:  要修改全局变量的内存地址, 所以只有不可变类型需要`global`
- 在函数内部使用全局变量时, 要先声明 `global` 全局变量, 如果是可变类型就不需要了
- 对于操作全局变量的数据, 如果是通过重新赋值来完成的, 那么必须加上`global`关键字
- `nonlocal` 使用场景是函数嵌套时，内层函数要使用外层函数的变量或参数

```python
a = 1
b = [1]

def t():
    global a
    a = 2
    b.append(2)
    print(a, b)

t()
print(a, b)
# 2 [1, 2]
# 2 [1, 2]
```

### 3.4. 函数参数

- 分类

  - 位置参数：按照位置顺序依次给函数的参数传值

  - 关键字参数：按照关键字名给函数的参数传值

  注：前面按位置, 后面按关键字, 如果前面用了关键字参数, 后面不能再使用位置参数, 只能使用关键字参数传参

- 不定长参数: 函数的参数个数不确定, 可能0个, 可能多个

  - 不定长位置参数, `*args`, 调用函数时所有位置参数都封装成元组, 赋值给`args`
  - 不定长关键字参数, `**kwargs`, 调用函数时所有关键字参数都封装成字典, 赋值给`kwargs`

  注: `*args` 和 `**kwargs` 这两个参数名可以修改, 但一般不改, 大家习惯了

```python
def show(name, *args, age=18, **kwargs):
    print("name:", name, "age:", age, "args:", args, "kwargs:", kwargs)
show("李四", 1, 2, "a", a=1, b=2, age=20)

# name: 李四 age: 20 args: (1, 2, 'a') kwargs: {'a': 1, 'b': 2}
```

- **拆包**：使用不同变量保存容器类型中的每个数据，对应的变量和数据数量要保持一致致

  -  容器类型如:字符串, 列表, 元组, 字典, range, 集合(set) 都可以利用拆包, 容器类型可以使用变量保存不同的数据

  - `*my_tuple`: 对元组/列表进行拆包, 也就是把元组/列表里每个数据按位置参数进行传参
  - `**my_dict`: 对字典进行拆包, 也就是把字典里面的每一个键值对按关键字的方式进行传参

### 3.5. 匿名函数

定义：没有名字的函数, 就是匿名函数, 匿名函数返回值不需要 `return`，用` lambda` 定义

格式:  `lambda [形参1], [形参2], ... : [单行表达式] 或 [函数调用]`

```python
>>> my_func = lambda a: print(a)
>>> my_func("hello world")
hello world
```

### 3.6. 常见函数定义

- 递归函数: 在一个函数内调用的是函数本身, 这样的函数称为递归函数
- 函数嵌套：python中, 可以在函数内部再定义一个函数, 称为函数的嵌套（例：装饰器）
- 高阶函数：函数的参数或者返回值是一个函数类型, 那么这样的函数就叫高阶函数（例：装饰器）

## 4. 文件

### 4.1. 常识

- 在windows的python解释器里面, 打开文件默认的编码格式是 `gbk` 的

- 在mac和linux的解释器里面, 打开文件默认的编码格式是 `utf-8` 的

- `utf-8` 一个汉字占用三个字节, 一个字母占1个字节

- 编码:  `.encode("utf-8")`

- 解码:  `.decode("utf-8")`

## 5. 面向对象

> 面向对象就是对面向过程的封装
>
> **面向对象的三大特性**
>
> **封装:** 把属性和方法放到类里面的操作就是封装, 封装可以控制属性和方法的访问权限
>
> **继承:** 子类可以使用父类的方法或者属性, 提高了代码的复用性, 注意点: 父类的功能满足不了子类的需要, 重写父类的方法
>
> **多态:** 
>
> - 对象调用同一个方法会出现不同的表现形式(表现结果)
> - 多态的好处, 代码的可扩展性强, 代码兼容性强, 不关系类型, 只关系对象是否具有指定功能方法

### 5.0. 类的实例化过程

1. 内存分配：Python为对象分配所需的内存空间。

2. 初始化实例：调用类的__init__方法来初始化实例。__init__方法是类中一个特殊的方法，它在实例化对象时被自动调用。

3. 创建对象引用：创建一个指向该实例的引用，允许你通过变量来访问该实例。

4. 执行__new__方法（可选）：如果定义了__new__方法，它将在__init__之前被调用。__new__方法负责创建实例。

5. 返回实例：返回一个指向新实例的引用，使你可以使用该引用来操作该实例。

总结起来，实例化一个类时，Python会为对象分配内存空间，然后调用__init__方法初始化实例，最后返回新实例的引用。这样，就可以通过该引用来操作和访问该实例的属性和方法。

### 5.1. 魔法方法

**定义**：方法名前后都有两个下划线, 这样的方法称为魔法方法, 魔法方法具有一定的特殊功能

**常见魔法方法**：

- `__new__` 分配内存的方法, 在`__init__`之前调用

- `__init__`, 在创建一个对象时默认被调用,不需要手动调用, 可以在此方法内添加对象属性

- `__del__`, 创建对象后, python解释器默认调用`__init__`方法, 当删除对象时, python解释器也会默认调用`__del__`方法

- `__str__`, 当使用`print`输出对象的时候, 默认打印对象的内存地址, 如果类定义了此方法,那么就会打印从在这个方法中`return`的数据, 此方法返回必须是字符串类型, 作为这个对象的描述信息. 

- `__slots__`方法, 限定自定义类型的的对象只能绑定某些属性, 只对当前类对象生效, 对子类并不起任何作用

- `__enter__`表示上文方法，需要返回一个操作文件对象

- `__exit__`表示下文方法，with语句执行完成会自动执行，即使出现异常也会执行该方法

**对象销毁的方式**:

- 程序运行结束, 程序中所使用对象都要在内存中销毁

- 当对象没有变量使用的时候, 该对象就会被销毁, 引用计数为0时会销毁

### 5.2. 继承

**语法**：`class 子类名(父类名):`  / `class 子类名(父类1, 父类2):`

**说明**：子类复用父类里面的属性或方法,  提高代码的复用性,  能够使用父类里面的方法或者属性, 包括`__init__`方法

**常识：**

- 父类也称为基类,  子类也称为派生类

- 单继承：子类只继承一个父类
- 多继承：子类继承多个父类, 可以使用多个父类里的方法
  - `.mro()`  方法可查看类的继承顺序
- 多层继承：只要有类继承关系, 子类对父类及所有上层父类的方法都可以使用

- 继承后方法的调用：先从本类查找, 依次往后查找, 找到就停, 如果没找到对应方法, 程序崩溃
- 重写：子类继承父类, 对父类的功能方法进行重新改造（子类方法名要和父类方法名相同）

**子类调用父类方法：**

- `self.方法()` : 当子类没有这个方法时候才可以用, 子类有相同方法时用`父类的类名.方法(self)`

- `父类的类名.方法(self)` :  类名调用对象方法, 需要自己手动传入self参数, 对象调用对象方法, 不需要传self参数

- `super().方法()` :  `super`是一个类, `super()`表示创建了一个父类对象, 通过`__init__`方法给对象添加属性 

  - 完整写法 `super(子类名称, self).父类方法()`  : 指定类名, 根据子类获取对应父类

  -  super本质: 根据指定类 在类的继承顺序**类名.mro()**中获取下一个类, 然后调用下一个类的方法, 如果是单继承, super的调用可以认为是调用的是父类的方法

### 5.3. 私有权限

1. 在属性名和方法名前加两个下划线
2. 私有属性和私有方法只能在本类中使用, 不能在类外部使用
3. 其实私有属性及方法只是对属性名和方法名进行了包装, 把名字进行了修改
4. 总结: 私有属性和方法 的包装格式: 在属性名和方法名前面加 `_本类类名__`
5. 子类无法使用父类的私有属性和私有方法, 也是把名字做了包装, 同上
6. 给对象添加私有属性只能在`__init__`方法里面完成

### 5.4. 类属性和实例属性

- **类属性**: 在类的内部init方法外部定义的属性, 类属性属于类

- - **私有类属性**: 类名前加两个下划线, 也是把名字做了包装, 实际同对象的私有

- **实例属性**: 在init方法内部定义的属性称为实例属性, 实例属性属于实例  (实例 == 对象)

- **类不能访问对象属性, 但是对象可以访问类属性(对象不能修改类属性, 只能类去修改)**
- **总结**: 对象属性的操作是由对象完成, 类属性操作由类来完成, 只不过对象可以访问类属性(也可以用 **self.__class__.类属性** 修改类属性, 用class找到类然后是类去修改类属性), 类不能访问对象属性

### 5.5. 类中方法的种类

- **实例方法**: 方法的第一个参数是self, 那么这样的方法就是对象方法, self表示当前对象, 实例方法, 类不能调用
- **类方法**(修改和获取类的私有属性时使用): 方法第一参数cls并且还需要使用`@classmethod`的关键字进行修饰, cls表示当前类, 类方法可以获取和修改类的私有属性, 类方法类和对象都可以调用

- **静态方法**: 方法里没有self和cls参数并且还需要使用`@staticmethod`的关键字进行修饰

## 6. 异常&模块

### 6.1. 异常

**异常捕获` try...except...`**

- `try` 表示尝试执行可能出问题的代码, `except` 表示如果代码出现异常, 进行捕获 `as e:`
- 捕获异常类型的通用写法就是用`Exception`,  因为大多数异常类型都是最终继承`Exception`的
- `BaseException` 可以捕获任何异常

**`try...except...else...finally`**

- `except` 与 `else` 互斥,  `finally`不管有没有异常都执行

**异常的传递**

- 当执行代码的时候遇到错误, 首先判断当前代码块对异常进行捕获, 如果没有, 那么再把异常一层一层往外传递, 如果外界的都没对异常的捕获, 程序就会崩溃, 如果有异常捕获, 就不会崩溃了

**自定义异常**

- class定义自定义异常类, 必须继承`Exception`或者`BaseException`才可以
- 抛出自定义异常使用关键字`raise`
- 注意:raise只能抛出异常类的对象

### 6.2. 模块

 **通俗理解模块就是一个 .py 文件, 模块里面可以定义具体的功能代码(类, 函数, 全局变量, 匿名函数等等)**

```python
# 查看导入模块的搜索路径 
import sys 

print(sys.path)       
```

- 模块好比一个工具箱, 模块里的每一个具体代码好比一个工具
- 模块的命名规则和变量名的命名规则一样 使用下划线命名
- 模块名的组成和变量名组成一样, 字母, 数字, 下划线开头, 如果以数字开头, 这个模块就不能使用了

**导入模块的两种方式**

- import 模块名  as 别名
- from 模块名 import 功能代码(函数, 类, 全局变量)   as 别名
- from 模块名 import *  导入模块里所有功能代码 一般不这样使用

**导入模块注意点**

- 自制的模块名不要和系统的模块重名
- 使用from 模块名 import 功能, 在当前模块不要再定义导入功能的代码, 否则会覆盖之前导入功能代码

**自制模块**

- __all__ 指定导入对应的功能代码  __all__ = [类名, 类名.....]  all定义针对外界使用from 模块名 import * 导入,  只能导入all里面指定的功能代码

**主模块名字**: __main__  

**导入的模块名字**:  就是模块原本的名字

**包:** **通俗理解只要文件夹里包含一个__init__.py文件, 那么这个文件夹就是包**

- 包的作用: 包是用来管理不同模块的 
- 模块的作用: 模块是用来管理不同功能代码的
- 包名的命名规则和变量名一样, 使用下划线命名法
- 包名的组成和变量名的组成一样, 数字, 字母, 下划线 不能数字开头
- **包的特点**:

- - 包里面有一个__init__.py文件,这是包的初始化文件, 当且仅当第一次导入包的时候会执行这个文件
  - __init__.py 其实就是包的象征文件
  - __init__.py 可以控制模块的导入行为
  - __init__.py 可以定义类, 函数, 全局变量等代码

**包的导入目的使用包里面的模块**

**格式**: 

- import 包名  指定导入包, 用包调用模块, 使用模块中的功能代码 第一次导入包的时候会默认调用__init__.py  
- import 包名.模块名
- from 包名 import 模块名
- from 包名 import 模块名 as 模块别名
- from 包名 import *      默认不是导入包里所有模块, 需要在__init__.py中使用__all__去指定

# 二. 高级

## 1. 多任务

### 1.1. 常识

- 多任务的目的：充分利用CPU资源，提高执行效率

- 时间片：内核分配给程序执行的一小段时间，这个时间内进程拥有cpu资源

- 同步：协同步调，按预定的先后次序进行运行。如：你说完，我再说

- 进程、线程同步：可理解为进程或线程A和B一块配合，A执行到一定程度时要依靠B的某个结果，于是停下来，示意B运行; B执行，再将结果给A; A再继续操作

- 进程状态: 等待状态不占用时间片, 即使时间片有剩余也会退出不占用CPU资源, 只有运行状态才占用CPU资源

  ![image-20230704132442670](..\images\image-20230704132442670.png)

### 1.2. 执行形式

- 并发：在一个时间段内，交替的执行多个任务，任务数 > CPU核心数，时间片轮转
- 并行：在一个时间点，多核CPU同时执行多个任务，任务数 < CPU核心数
- 一般情况下，并发和并行同时存在

### 1.3. 实现方式：进程

- **进程是操作系统进行资源(CPU、内存)分配的基本单位**
- 程序中至少有一个进程，这个进程称为主进程
- 主进程会等待所有子进程执行结束再结束
  - 如果子进程没执行完，主进程会一直等待，此时如果子进程进入死循环会导致主进程无法退出解决办法：
    - 设置子进程为守护主进程，主进程退出时子进程直接销毁: `sub_process.daemon = True`
    - 主进程退出前先销毁子进程: `sub_process.terminate()`
- 每个进程中至少有一个线程，这个线程称为主线程
- 进程间不共享全局变量
- 进程之间执行也是无序的，由操作系统调度决定

```python
# 进程创建子进程时程序会复制一份代码去跑(也就是说操作系统会再次进行资源分配，所以创建出来的子进程所拥有的内存是和创建它的进程的内存是不同的，所以不可能共享全局变量)
# 打印全局变量id可发现变量的内存地址是不同的
import time
import multiprocessing


my_list = []  # 列表可变类型，为全局变量


def read_val():
    print(f"reading list: {my_list}, id: {id(my_list)}")


def write_val():
    for i in range(3):
        my_list.append(i)
        print(f"writed.....{my_list}, id: {id(my_list)}")
        time.sleep(0.5)


# 创建子进程时：linux和mac不会拷贝主进程执行的代码，但windows会拷贝主进程代码并执行，所以对windows来说创建子进程的代码会发生递归执行而报错，需要把此部分代码放在__name__ == "__main__"判断下（判断主模块的代码只会执行一次），linux和mac就不需要
if __name__ == "__main__":
    read_task = multiprocessing.Process(target=read_val)
    write_task = multiprocessing.Process(target=write_val)

    write_task.start()
    read_task.start()
```

### 1.4. 实现方式：线程

- 线程是进程中执行代码的一个分支，每个线程想到执行代码需要CPU进行调度
- **线程是CPU调度的基本单位**，每个进程至少有一个线程，称为主线程
- 主线程会等待所有子线程结束再结束
  - `sub_thread.setDaemon(True)`
  - `threading.Thread(target=task, daemon=True)`
- 线程执行时无序的, 谁抢到CPU, 谁就执行
- 线程之间共享全局变量，因为在同一进程里面，所以使用的内存资源是相同的，这会导致数据错乱问题，解决方案
  - 线程等待 `sub_thread.join()`
  - 互斥锁：对共享数据进行锁定，保证同一时刻只有一个线程操作共享数据
  - 以上两种方法都是把多任务改成单任务去执行，保证了数据的准确性，但执行效率会下降

```python
import time
import threading


def sing(name):
    cur_thread = threading.current_thread()
    print(f"sing: {cur_thread}\n")
    for _ in range(3):
        print(f"singing {name}... \n")
        time.sleep(0.2)

def dance():
    cur_thread = threading.current_thread()
    print(f"dance: {cur_thread}\n")
    for _ in range(3):
        print("dancing... \n")
        time.sleep(0.2)

def tutorial0():
    """线程无序"""
    main_thread = threading.current_thread()
    print(f"main thread: {main_thread}")

    sing_thread = threading.Thread(target=sing, args=("正月十八", ))
    dance_thread = threading.Thread(target=dance)

    sing_thread.start()
    dance_thread.start()


# 线程之间共享全局变量
g_list = []


def add_data():
    for i in range(3):
        g_list.append(i)
        print(f"added, {g_list}\n")


def read_data():
    print(f"read data {g_list}\n")


def tutorial1():
    """线程共享全局变量"""
    add_thread = threading.Thread(target=add_data)
    read_thread = threading.Thread(target=read_data)

    add_thread.start()
    read_thread.start()


g_num = 0
lock = threading.Lock()


def add_num0():
    lock.acquire()
    for _ in range(100_0000):
        global g_num  # int不可变要用全局需要声名
        g_num += 1
    print(f"add0: {g_num}")
    lock.release()


def add_num1():
    lock.acquire()
    for _ in range(100_0000):
        global g_num  # int不可变要用全局需要声名
        g_num += 1
    print(f"add1: {g_num}")
    lock.release()


def tutorial2():
    """数据保护"""
    thread0 = threading.Thread(target=add_num0)
    thread1 = threading.Thread(target=add_num1)

    thread0.start()
    # thread0.join()  # 线程等待 在0执行完再向下执行
    thread1.start()

if __name__ == "__main__":
    tutorial2()

```

### 1.5. 实现方式：协程

**迭代器 Iterator**

- 可迭代对象(Iterable)定义：包含 `__iter__` 方法
  - 可迭代对象不一定是迭代器，但迭代器一定是可迭代对象

```python
# 判断一个对象是否可迭代
from collections import Iterable

isinstance(A, Iterable)
```

- 迭代器定义：包含 `__iter__` 和 `__next__` 方法
  - 迭代是访问集合元素的一种方式
  - 迭代器是一个可以记住遍历位置的对象
  - 迭代器对象从集合第一个元素开始访问，直到所有元素被访问结束
  - 迭代器只能往前不能后退
  - 迭代器可以节省内存空间，实现循环
- 迭代器优点：存放生成数据的实现方式而不是具体数据，占用很少的内存空间

```python
from collections.abc import Iterable, Iterator


class ClassIterator:

    def __init__(self, obj) -> None:
        self.obj = obj
        self.cur_num = 0

    def __iter__(self):
        pass

    def __next__(self):
        if self.cur_num >= len(self.obj.names):
            raise StopIteration

        res = self.obj.names[self.cur_num]
        self.cur_num += 1
        return res


class Classmate:

    def __init__(self) -> None:
        self.names = list()

    def add(self, name):
        self.names.append(name)

    def __iter__(self):
        """想要一个对象称为一个 可迭代对象, 即可以用for遍历
        必须要有此方法
        """
        return ClassIterator(self)


# iter返回self
class Fibonacci:

    def __init__(self, nums) -> None:
        self.nums = nums
        self.cur_num = 0
        self.a = 0
        self.b = 1

    def __iter__(self):
        return self

    def __next__(self):
        if self.cur_num >= len(self.nums):
            raise StopIteration
        
        res = self.a
        self.a, self.b = self.b, self.a + self.b
        self.cur_num += 1

        return res


if __name__ == "__main__":
    classmate = Classmate()

    classmate.add("foo")
    classmate.add("zoo")
    classmate.add("yoo")

    # iter方法会自动调用__iter__方法接收返回值, 其返回值就是迭代器也就是ClassIterator类创建的对象就是迭代器
    classmate_iterator = iter(classmate)
    print(isinstance(classmate_iterator, Iterator))  # 判断是否是迭代器 True

    for i in classmate:
        print(i)  # foo zoo yoo

    print(isinstance(classmate, Iterable))

```

**生成器 Generator**

- 生成器是一种特殊的迭代器
- 如果一个函数中有`yield`语句，那么这个函数就不再是函数，而是一个生成器模板
- 定义：生成器推导式
  - 列表推导式：`[i for i in range(3)]`
    - 把列表推导式的`[]` 改为 `()` 返回的就是一个生成器
- 生成器的启动：让生成器从断点处继续执行，即唤醒生成器
  - `next()`第几次启动都可以，但不能传参
  - `obj.send(param)` 需要传参时使用，不能第一次启动时使用
- 获取生成器数据用 `next(generator)`方法
- 生成器数据全部取出后再次使用`next()`方法会报`StopIteration`错误
- `yield`关键字有两个作用
  - 保存当前运行状态，暂停执行，将生成器挂起
  - 将`yield`关键字后面表达式的值作为返回值返回，此时类似`return`

```python
def create_num(cnt):
    a, b = 0, 1
    cur_num = 0
    while cur_num < cnt:
        yield a
        a, b = b, a + b
        cur_num += 1

gen_obj = create_num(10)  # 此时创建了一个生成器对象
print(gen_obj)  # <generator object create_num at 0x0000022C5899D510>
print([i for i in gen_obj])  # [0, 1, 1, 2, 3, 5, 8, 13, 21, 34]

```

**协程 Coroutine**

```python
# 使用greenlet

import time
from greenlet import greenlet

def t1():
    while True:
        print("----------A----------")
        gr2.switch()
        time.sleep(1)


def t2():
    while True:
        print("----------B----------")
        gr1.switch()
        time.sleep(1)

gr1 = greenlet(t1)
gr2 = greenlet(t2)

print(gr1, gr2)
gr2.switch()

"""
<greenlet.greenlet object at 0x00000276263C30F0 (otid=0x00000276263A9EE0) pending> <greenlet.greenlet object at 0x00000276263C31A0 (otid=0x00000276263C7040) pending>
----------B----------
----------A----------
----------B----------
----------A----------
...
"""

# 使用gevent碰到延时就切换到其他的greenlet去运行
from gevent import monkey
monkey.patch_all()
```

### 1.6. 不同实现方式对比

- 进程是资源分配的基本单位，切换需要资源最大，效率很低
- 线程是操作系统调度的基本单位，切换需要的资源一般，效率一般(不考虑GIL的情况下)
- 协程切换任务需要的资源很小，效率高
- 多进程、多线程根据CPU核数不同可能是并行的，协程在一个线程中所以一定是并发的

### 1.7. GIL锁

> GIL（全局解释器锁）是一个在CPython解释器中的锁，用于确保同一时刻只有一个线程执行Python字节码。这是由于CPython的内存管理机制并不是线程安全的，因此GIL可以防止多个线程同时访问、修改同一块内存，从而避免了可能出现的数据竞争和内存错误。但同时，GIL也限制了Python多线程并行性能，在一些密集计算和多线程CPU密集型任务场景中表现不及其他语言和并发框架。

> CPython解释器的内存管理机制是基于引用计数的垃圾回收，即对象被引用一次计数器加一，对象引用被释放计数器减一，当计数器变为0时，对象被回收。这种内存管理机制并不是线程安全的，因为多个线程可能同时访问和修改同一块内存，从而导致计数器不一致，或者对象被销毁多次，或者内存泄漏等问题。因此，为了避免这些问题，CPython引入了GIL锁来确保同一时刻只有一个线程执行Python字节码，从而保证内存管理的线程安全性。

>  CPython（即C实现的Python解释器）的内存管理机制在默认情况下并不是线程安全的，这是由于全局解释器锁（Global Interpreter Lock，GIL）所导致的。 GIL是一种机制，确保每个时刻只有一个线程执行Python字节码。这个锁的存在是为了简化CPython的设计实现，因为锁的存在可以防止多个线程同时访问和修改Python对象的内部数据结构，从而提供了一种简单而有效的线程安全保证机制。 由于GIL的存在，当多个线程同时运行Python代码时，它们必须相互竞争获取全局解释器锁。这意味着在进行CPU密集型任务时，多线程并不能充分利用多核心处理器的优势。 而在内存管理方面，CPython使用引用计数机制进行内存的自动分配和释放。每个Python对象都有一个引用计数器，用于跟踪对象的引用数量。但是，由于GIL的存在，多个线程同时修改对象的引用计数可能会导致竞争条件和不一致性，从而破坏了线程安全性。 虽然CPython提供了一些线程安全的数据结构和锁机制（如`threading`模块的`Lock`类），但因为GIL的存在，多线程Python代码的执行效率并不能获得明显提升。 值得注意的是，其他实现的Python解释器，如Jython和IronPython，并不使用全局解释器锁，因此在多线程环境中可能具有更好的性能和线程安全性。

-   全局解释器锁
-   保证同一时间, 只有一个线程使用CPU, 不管主子线程
-   GIL的存在导致, python中只有进程是可以并行的, 多线程实际也是并发的
-   一个进程有一个GIL锁
-   GIL不是python的特性, 只是CPython解释器的概念, 历史遗留问题

现不及其他语言和并发框架。

  **GIL锁什么时候释放**

-   当前线程执行超时后会释放
-   当前线程阻塞操作时会自动释放(input, io/输入输出)
-   当前执行完成时

  **GIL的弊端**

-   GIL对计算密集型的程序会产生影响。因为计算密集型的程序，需要占用系统资源。
-   GIL的存在，相当于始终在进行单线程运算，这样自然就慢了。
-   IO密集型影响不大的原因在于，IO，input/output，这两个词就表明程序的瓶颈在于输入所耗费的时间，线程大部分时间在等待，所以它们是多个一起等（多线程）还是单个等（单线程）无所谓的。

  **解决方案：**

  要提升多线程执行效率，解决方案：

-   更换解释器
-   改为进程替换多线程
-   子线程使用C语言实现（绕过GIL锁）

  **必须要知道的是：**

-   CPU 密集(计算密集)型不太适合多线程
-   I/O 密集型适合多线程/协程（Gil锁会释放）

  

## 2. 高级语法

### 2.1. 闭包&装饰器

```python


"""闭包
定义：函数嵌套的前提下，内部函数使用了外部函数的变量或参数，外部函数返回内部函数
作用：保存外部函数内的变量, 不会随着外部函数调用结束而销毁，但消耗内存!

"""
def outter0(a):
    local_a = "world"
    def inner(b):
        print(f"inner: {a}, {b} {local_a}")
    return inner

def t0():
    foo = outter0("foo")
    foo("hello")

    goo = outter0("goo")
    goo("hello")

    # inner: foo, hello world
    # inner: goo, hello world


def outter1(a=10):
    print(f"outter: {a}")

    def inner(b=10):
        nonlocal a
        a = a + b  # 此时默认是是取local vars不声名nonlocal会报UnboundLocalError
        print(f"inner a: {a}, b: {b}")
    return inner


def t1():
    f = outter1()
    f()
    # outter: 10
    # inner a: 20, b: 10


"""
装饰器：本质就是一个闭包函数（但要求闭包函数有且只有一个参数, 参数必须是函数类型）
装饰器的执行事件是加载模块事立即执行 (在函数定义时候执行了), 所以一般外部函数内不写其他东西, 只有内部函数
特点：
    - 不修改已有函数的源代码
    - 不修改已有函数的调用方式
    - 给已有函数增加额外的功能
"""

# 通用装饰器(inner的参数为 *args, **kwargs也就是接收任意参数)
def outter2(f):
    def inner(*args, **kwargs):
        print(f"inner: {args, kwargs}")
        res = f(*args, **kwargs)
        print(f"inner: {res}")
        return res
    return inner


@outter2  # 相当于执行了这句代码：func = outter2(func)
def func2(a, b, c=3, d=None):
    print(f"func: {a, b, c, d}")
    return "hello world"


def t2():
    func2(1, 2, d=5)
    # inner: ((1, 2), {'d': 5})
    # func: (1, 2, 3, 5)
    # inner: hello world


# 带有参数的装饰器：装饰器外再加一层闭包
def outter3(flag=False):
    def outter2(f):
        def inner(*args, **kwargs):
            # 此时只是打印flag, 没修改不可变类型，不需要声名nonlocal
            print(f"inner: {args, kwargs}, {flag=}")
            res = f(*args, **kwargs)
            print(f"inner: {res}, {flag=}")
            return res
        return inner
    return outter2


@outter3(True)
def func3(a, b, c=3, d=None):
    print(f"func: {a, b, c, d}")
    return "hello world"

def t3():
    func3(1, 2, d=4)
    # inner: ((1, 2), {'d': 4}), flag=True
    # func: (1, 2, 3, 4)
    # inner: hello world, flag=True


# 类装饰器
class Outter4:
    
    def __init__(self, f):
        self.f = f
    
    def __call__(self, *args, **kwargs):
        print(f"inner: {args=}, {kwargs=}")
        res = self.f(*args, **kwargs)
        return res

@Outter4
def func4(a, b, c=3, d=None):
    print(f"func: {a, b, c, d}")
    return "hello world"


def t4():
    func4(1, 2, d=4)
    # inner: args=(1, 2), kwargs={'d': 4}
    # func: (1, 2, 3, 4)


if __name__ == "__main__":
    t4()

```

### 2.2. property

**3. property属性**

- property属性就是负责把一个方法当做属性进行使用，这样做可以简化代码使用
- 定义方式
  - 装饰器方式
  - 类属性方式

```python
# 类属性方式 
class Student(object):   

    def __init__(self):     
        self.__age = 0   

    def get_age(self):     
        return self.__age   

    def set_age(self, value):    
        self.__age = value

    # 第一个参数是获取值的方法， 第二个是设置值的方法   
    age = property(get_age, set_age)      


# 装饰器方式
class Student(object):   

    def __init__(self):
        self.__age = 0

    # 获取年龄
    @property
    def age(self):
        return self.__age   

    # 设置年龄
    @age.setter
    def age(self, value):     
        self.__age = value  

```

### 2.3. with语句&上下文管理器

- with 语句执行完成以后自动调用关闭文件操作, 即使出现异常
- 一个类只要实现了``__enter__()``和``__exit__()``这个两个方法，通过该类创建的对象我们就称之为上下文管理器

```python
# 要实现上下文管理器， 要实现__enter__ 和 __exit__  
class File(object):   

    def __init__(self, file_name, file_mode):
        self.file_name = file_name
        self.file_mode = file_mode

        # 实现上文的方法，主要用来提供资源，需要返回一个对象
        def __enter__(self):
            print('entered up')
            self.fp = open(self.file_name, self.file_mode)
            return self.fp

        
        # 实现下文的方法，主要用来释放资源
        def __exit__(self, exc_type, exc_val, exc_tb):
            print('exited down')
            self.fp.close()

            
with File("a.txt", "w") as f:
    print('-' * 28)

# entered up
# ----------------------------
# exited down
```

- 上下文管理器可以使用 with 语句，with语句之所以这么强大，背后是由上下文管理器做支撑的，也就是说刚才使用 open 函数创建的文件对象就是就是一个上下文管理器对象
- ``__enter__``表示上文方法，需要返回一个操作文件对象

- `__exit__`表示下文方法，with语句执行完成会自动执行，即使出现异常也会执行该方法

### 2.4. 深拷贝和浅拷贝

- `import copy`拷贝的目的: 保证原数据和拷贝的数据之间不影响
- **`copy.copy()` 浅拷贝**，只对可变类型的第一层对象进行拷贝，对拷贝的对象开辟新的内存空间进行存储，不会拷贝对象内部的子对象
  - 不可变类型进行浅拷贝不会给拷贝的对象开辟新的内存空间，而只是拷贝了这个对象的引用
  - 可变类型进行浅拷贝只对可变类型的第一层对象进行拷贝，对拷贝的对象会开辟新的内存空间进行存储，子对象不进行拷贝
- **`copy.deepcopy()` 深拷贝**, 只要发现对象有可变类型就会对该对象到最后一个可变类型的每一层对象就行拷贝, 对每一层拷贝的对象都会开辟新的内存空间进行存储
  - 不可变类型进行深拷贝如果子对象没有可变类型则不会进行拷贝，而只是拷贝了这个对象的引用，否则会对该对象到最后一个可变类型的每一层对象就行拷贝, 对每一层拷贝的对象都会开辟新的内存空间进行存储
  - 可变类型进行深拷贝会对该对象到最后一个可变类型的每一层对象就行拷贝, 对每一层拷贝的对象都会开辟新的内存空间进行存储
- **浅拷贝最多拷贝对象的一层 (即使可变类型, 也只拷贝第一层) 其它情况都是拷贝引用**
- **深拷贝可能拷贝对象的多层 (只要是有可变类型, 就全部拷贝) 其它情况都是拷贝引用**

### 2.5. 单例

```python
# 只有一份内存空间
# __new__ 开辟内存空间, 会在__init__之前执行 

class Singleton(object):   
    is_instance = None   
    def __new__(cls, *args, **kwargs):
        if cls.is_instance is None:
            # 保证下边代码执行一次
            cls.is_instance = object.__new__(cls)
            return cls.is_instance
        else:
            return cls.is_instance


a = Singleton()
b = Singleton()
c = Singleton()

>>> id(a) == id(b) == id(c)
>>> True

```





























