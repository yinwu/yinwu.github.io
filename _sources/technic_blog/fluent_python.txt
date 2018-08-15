Fluent Python(流畅的python)
==============================

大概浏览了前几章，感觉这本书的还是有一些难度的。不适合python初学者，但是很适合提高。

第一部分 序幕
------------------

第一章 python 数据模型
^^^^^^^^^^^^^^^^^^^^^^^^^^^

这章主要讲Python的特殊方法，即Magic method。特殊方法的存在是为了被python解释器调用的，你自己并不需要显示的调用他们。

* __getitem__
    
    实现对象的下标操作，让对象编程可迭代的对象。

* __len__

    实现标准集合类型的len方法。

* __iter__

    实现 for i in x: 格式的语句

* __repr__

    实现对象的字符串表达形式，实现对象的repr方法

* __str__

    实现对象的str方法，没有__str__方法时，会调用__repr__作为替代。

    `str 和 repr的区别`?

* __bool__ 

    默认情况下，自定义类的实例默认情况下都是true，除非我们实现了__bool__方法。


* 其他特殊方法

    #. __format__ __abs__ __bytes__ __complex__ __float__
    #. __hash__ __index__ __setitem__ __delitem__ 
    #. __contains__ __reverser__ __next__
    #. __call__
    #. __enter__ __exit__
    #. __new__  __init__ __del__
    #. __getattr__ __getattribute__ __setattr__ __delattr__ __dir__
    #. __get__ __set__ __delete__
    #. __prepare__ __instancecheck__ __subclasscheck__

第二部分 数据结构
----------------------------

第二章 序列构成的数组
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

* 容器序列

    list, tuple, collections.deque存放不同类型的数据

* 扁平序列

    str, bytes, bytearray, memoryview, array.array只能容纳一种类型

* 可变序列

    list, bytearray, array.array, collections.deque, memoryview

* 不可变序列

    tuple, str, bytes

* 列表推导

    列表推导是创建新列表的快捷方式。

    .. code-block:: python

        codecs = [ord(symbol) for symbol in symbols]

* 笛卡尔积
    
    .. code-block:: python

        colors = ["red", "blue"]
        sizes = ["s", "m", "l"]
        t_shirt = [(color, size) for color in colors for size in sizes]

* 生成器表达式

    相比列表推导，生成器表达式是生成列表更好的选择，因为生成器表达式遵守了迭代器协议，可以逐个产出元素

    生成器表达式语法跟列表推导差不多，只不过把方括号换成圆括号


    .. code-block:: python 

        colors = ["red", "blue"]
        sizes = ["s", "m", "l"]

        for t_shirt in ("%s %s" % (c, s) for c in colors for s in sizes)

    上例中的程序，不会在内存中一次性产出有6个元素的列表，而是逐个产出元素。

* 元组的拆包

    .. code-block:: python

        x , y = (1, 2)

        passport_code = ("USA", "123456")
        print("%s %s" % passport_code)

        a, b = b, a

        # def divmod(x, y)

        # * 解引用， 把可迭代对象拆开作为函数的参数
        t = (20, 8)
        divmod(t)             # error
        divmod(*t)            # ok

        # _ 占位符
        _, filePath = os.path.split("/etc/vncserver/rsa.pub")

        # *来处理剩下的元素
        a, b，*rest = range(5) # (0, 1, [2, 3, 4])

        # 嵌套元组的拆包
        name, addr, code, (lattitude, longtitude) = ("test", "beijing", 101, (35.6124, 42.5678))

* 具名元组

    .. code-block:: python

        from collections import namedtruple
        City = nametruple('City', 'name country population coordinate')
        tokyo = City("Tokyp", "japan", 320000, (35.6124, 42.5678))

        # 具名元组具有一些特殊的方法
        >>>City._fields
        'name' 'country' 'population' 'coordinate'

        >>>Latlong = namedtuple("LatLong", 'lat long')
        >>>delphi_data = ("Delphi", "India", 21.935, LatLong(35.6124, 42.5678))
        >>>delphi = City._make(delphi_data)
        >>>delphi._asdict()
        OrderdDict([('name':'Delphi'), (...), (...), (...), ('coordinate':LatLong(35.6124, 42.5678))])

* 元组的方法和属性
    
    ...

* 切片

    切片和区间操作里面不包含区间范围的最后一个元素，是python风格。


第三章 字典和集合
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

第四章 文本和字节序列
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

第三部分 把函数视作对象
----------------------------


第四部分 面向对象惯用法
----------------------------


第十四章. 迭代器，生成器
--------------------------

序列可以迭代的原因：iter函数
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
    
    1，内置的iter函数，首先检查对象是否实现了__iter__函数，如果是就调用它，获取一个迭代器

    2，如果没有实现__iter__方法，但是实现了__getitem__方法，python会创建一个迭代器，尝试按顺序获取元素。

    3，如果尝试失败，抛出TypeError异常。

* 任何序列可迭代的原因是因为实现了__getitem__方法。

* 检查对象能否迭代的最准确的方式是调用iter(x), 如果不可迭代，再处理TypeError异常。这比isinstence(x, abc.Iterable) 更准确。iter(x)会考虑遗留的__getitem__方法。


可迭代的对象
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

使用iter内置函数可以获取迭代器的对象。如果对象实现了能返回迭代器的__iter__方法，那么对象就是可迭代的。
序列都是可迭代的原因，因为实现了__getitem__方法。

可迭代的对象和迭代器之间的关系： python从可迭代的对象获取迭代器

.. code-block:: python

    s = "ABC"
    for char in s:
        print(char)

字符串"abc"是可迭代的对象，背后是有迭代器，只不过我们看不到

.. code-block:: python

    s = "ABC"
    it = iter(s) #使用可迭代的对象构造迭代器
    while True:
        try:
            print(next(it))     # 在迭代器上调用next函数，获取下一个元素
        except StopIteration:     # 如果没有字符了，迭代器会抛出异常
            del it
            break

迭代器
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

标准的迭代器有两个接口方法

    **__next__** 返回下一个可用的元素，如果没有元素则抛出StopIteration异常

    **__iter__** 返回self，以便在应该使用可迭代对象的地方使用迭代器

迭代器是这样的对象，实现了无参数的__next__方法，返回序列的下一个元素，没有元素则抛出StopIteration异常
python中的迭代器还实现了__iter__方法，因此迭代器也可以迭代。

`可迭代的对象一定不能是自身的迭代器，也就是说，可迭代的对象必须实现__iter__方法，但是不能实现__next__方法， 另一方面，迭代器应该一直可以迭代，迭代器的__iter__方法应该返回自身`

.. code-block:: python

    class Sentence:

        ...

        def __iter__(self):
            return SentenceIterator(self.word)

        ...

    class SentenceIterator:

        def __next__(self):
            try:
                word = self.word[self.index]
            except IndexError:
                raise StopIteration
            
            self.index += 1
            return word

        def __iter__(self):
            return self

生成器函数
^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    class Sentence:

        ...

        def __iter__(self):
            for word in self.word:
                yield word
            
            return 

用生成器函数，不在需要单独定义一个迭代器类(SentenceIterator). 迭代器就是生成器对象，每次调用__iter__
都会自动创建，因为这里的__iter__方法时生成器函数。

生成器函数工作原理
^^^^^^^^^^^^^^^^^^^^

* 只要python函数中包含关键字，这个函数就是生成器函数

* 生成器是迭代器，会生成传给yeild关键字的表达式的值

* 对迭代器调用next函数会获取yield生成的下一个元素

* 生成器函数的定义执行完毕后，生成器对象会抛出StopIteration异常。

.. code-block:: python

    def gen():
        yield 1
        yield 2
        yield 3

    g = gen()

    next(g) # 1
    next(g) # 2
    next(g) # 3
    next(g) # StopIteration.

    __iter__方法是生成器函数，调用时会构建一个一个实现了迭代器接口的生成器对象，因此不用再定义SentenceIterator类。


生成器的惰性实现
^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    class Sentence:

        def __init__(self, text):
            self.text = text

        def __iter__(self):
            for match in RE_WORD.finditer(self.text):
                yield match.group

re.finditer 是 re.find的惰性版本，返回的不是一个列表，而是一个生成器。这种实现方式让Sentence变得懒惰，
即只有在需要时才生成下一个单词。


生成器表达式
^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    def gen_ab():
        print("start")
        yield "A"
        print("continue")
        yield "B"
        print "end"

* 列表推导

.. code-block:: python

    res1 = [x*3 for x in gen_ab()]

.. code-block:: console

    >>> start
    >>> continue
    >>> end

    for i in res1:
        print i
    
    >>> AAA
    >>> BBB


* 生成器表达式

.. code-block:: python

    res2 = [x*3 for x in gen_ab()]

.. code-block:: console

    for i in res1:
        print i
    
    >>> start
    >>> AAA
    >>> continue
    >>> BBB
    >>> end

使用生成器表达式实现Sentence类
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: python

    class Sentence:

        def __iter__(self):
            return (match.group for match in RE_WORD.finditer(self.text))

如果生成器表达式要分多行写，应该使用生成器函数，提高可读性和代码重用的可能性。

标准库中生成器函数
^^^^^^^^^^^^^^^^^^^^^^^^^^^

python3.3中新语法: yield from
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

第十五章 上下文管理器和else块
--------------------------------------

for/else
^^^^^^^^^^^^^

	仅当for循环运行完毕后，才执行else语句。

while/else
^^^^^^^^^^^^^^

	仅当while语句因为条件为假值时退出时，才执行else语句。

try/except/else
^^^^^^^^^^^^^^^^^^^

    没有异常抛出时运行else语句。并且else块抛出的异常不会由except语句捕获。
    
    为了清晰和准确，try块中应该只包含抛出预期异常的语句，因此应该像下面这样

    .. code-block::python

    try:
        dangerous_call()
    except OSError:
        log("...")
    else:
        after_all()


EAFP/LBYL
^^^^^^^^^^^^^^^^

    **EAFP** (easier to ask for forgiveness than permission)

        先假定存在有效的键或者属性。如果假定不成立，那么捕获异常。这种风格简单明快，特点时代码中有大量的try/except语句。

    **LBYL** (look befor you leap)
    
        在调用函数或者查找属性或键值之前，显示测试前提条件。这种风格的特点是代码中有很多if/else语句。在多线程编程环境下有可能引入条件竞争。

with语句与上下文管理器
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

    with语句存在的目的时为了简化他依然/finally语句。用于保证一段代码执行完成后执行某个操作。即便那段代码由于异常，return语句或者sys.exit()调用而中止。

    上下文管理其存在__enter__, __exit__两个方法。with语句开始时调用__enter__，with语句结束时会调用__exit__方法。



第六部分 元编程
----------------------------
