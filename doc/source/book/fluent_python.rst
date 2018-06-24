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
		divmod(t) 			# error
		divmod(*t)			# ok

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

第五部分 控制流程
----------------------------

第六部分 元编程
----------------------------