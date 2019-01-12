python: 那些不知道的事儿
========================================


argparse - 参数解析
-------------------

参考 `官方文档 <https://docs.python.org/3/library/argparse.html>`_


str()函数和expr()函数的区别
------------------------------------


python map()方法
------------------------------------

map() 会根据提供的函数对指定序列做映射。
以参数序列中的每一个元素调用 function 函数，返回包含每次 function 函数返回值的新列表。

map函数的语法::

	map(function, iterable, ...)

返回值

	Python 2.x 返回列表。

	Python 3.x 返回迭代器。


python virtualenv环境介绍
-----------------------------------------

目的
^^^^^^^^

virtualenv为用户提供一个独立的python环境，解决多人在同一个机器上面开发不同项目，安装的包冲突的问题。
virtualenv可以为用户提供一套隔离的环境，用户在这个环境下随心所欲的安装自己的软件包，不影响其他人。

virtualenv安装步骤
^^^^^^^^^^^^^^^^^^^^^^^^

见 廖雪峰网站`virtualenv <https://www.liaoxuefeng.com/wiki/0014316089557264a6b348958f449949df42a6d3a2e542c000/001432712108300322c61f256c74803b43bfd65c6f8d0d0000>`_

pyenv和pyenv-virtualenv
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

见 简书文章`使用pyenv与pyenv-virtualenv管理python环境 <https://www.jianshu.com/p/9f6a9456ad5f>`_




