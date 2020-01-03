shell基本知识
=============

变量
----

定义时不加$符号，等号左右不能有空格。 使用时需要加$。unset 可以清空变量。

.. code-block:: shell

	name=test
	echo ${name}
	unset name

字符串
------

**单引号**

* 单引号的所有字符会原样输出，字符串中的变量是无效的。
* 单引号中不能再出现单引号，也不能出现转义符。


.. code-block:: console
	:linenos:                                                   
    :emphasize-lines: 7

	yinwu@yinwu-ThinkPad-E475:~/learning/shell$ cat variable.sh 
	#/usr/bin/sh
	name="yinwu"
	world='hello ${name}'
	echo ${world}
	yinwu@yinwu-ThinkPad-E475:~/learning/shell$ ./variable.sh 
	hello ${name}
	yinwu@yinwu-ThinkPad-E475:~/learning/shell$


**双引号**a

* 双引号中可以出现变量
* 双引号中可以出现转义符

.. code-block:: console
	:linenos:                                                   
    :emphasize-lines: 7

	yinwu@yinwu-ThinkPad-E475:~/learning/shell$ cat variable.sh 
	#/usr/bin/sh
	name="yinwu"
	world="hello ${name}"
	echo ${world}
	yinwu@yinwu-ThinkPad-E475:~/learning/shell$ ./variable.sh 
	hello yinwu
	yinwu@yinwu-ThinkPad-E475:~/learning/shell$ 

**拼接字符串**

.. code-block:: shell

	your_name="runoob"

	greeting="hello, "$your_name" !"
	greeting_1="hello, ${your_name} !"
	echo $greeting  $greeting_1

	greeting_2='hello, '$your_name' !'
	greeting_3='hello, ${your_name} !'
	echo $greeting_2  $greeting_3

**获取字符串长度**

.. code-block:: shell

	string="abcd"
	echo ${#string}

**提取字符串**

.. code-block:: shell

	string="this is a test"
	echo ${string:1:4}

**查找字符串**

.. code-block:: shell

	string="this is find test"
	echo `expr index "${string} io"`

shell 数组
----------

**定义数组**::

	array_name=(value0 value1 value2 value3)

**访问数组**::

	${array_name[n]} # 获取单个元素
	${array_name[@]} # 获取数组所有元素

**获取数据的长度**::

	length=${#array_name[@]}
	length=${#array_name[*]}

注释
----

**单行注释**::
	
	# 这是一个注释

**多上注释**::
	
	:<<EOF
	注释内容...
	注释内容...
	注释内容...
	EOF

shell 传递的参数
----------------

* $n : 表示第n个参数，n=0表示文件文字。
* $* : 表示所有参数，以一个整体来现实。
* $@ : 表示所有参数，但是每个参数都是用引号括起来的。 
* $# : 获取参数的个数
* $! : 最后运行的进程的ID号
* $$ : 脚本运行的当前进程ID号
* $? : 最后命令的退出状态，0 表示没有错误。
  
.. code-block:: shell

	echo "-- \$* 演示 ---"
	for i in "$*"; do
	    echo $i
	done

	echo "-- \$@ 演示 ---"
	for i in "$@"; do
	    echo $i
	done

输出结果为

.. code-block:: console

	$ chmod +x test.sh 
	$ ./test.sh 1 2 3
	-- $* 演示 ---
	1 2 3
	-- $@ 演示 ---
	1
	2
	3

shell运算符
-----------

**算数云算法** 

	+ - * / % = == !=

	bash不支持原生的数学运算，需要其他命令来实现::

		var=`expr 2 + 2`
		echo ${var}

**关系云算符**

a=10, b=20

* -eq equal 			[ $a -eq $b ] is false
* -ne not equal 		[ $a -ne $b ] is true
* -gt great than 		[ $a -gt $b ] is false
* -lt less than 		[ $a -lt $b ] is true
* -ge great or equal 	[ $a -ge $b ] is false
* -le less or equal     [ $a -le $b ] is true
  
**布尔运算符**

#. ! 非运算
#. -o 或运算
#. -a 与运算

**逻辑运算符**

#. $$ 逻辑AND
#. || 逻辑OR

**字符串运算符**

#. = 检测字符串是否相等
#. ！= 检测字符串是否不等
#. -z 检测字符串长度是否为0，为0返回true
#. -n 检测字符串长度是否为0，为0返回false。 在表达式中，表达式必须加引号。
#. [$str] 如果str不为空，则返回true

**文件测试运算符**

#. -d 检测文件是否是目录
#. -f 检测文件是否为普通文件(非目录和设备文件)
#. -r 检测文件是否可读
#. -w 检测文件是否可写
#. -x 检测文件是否可执行
#. -s 检测文件是否为空
#. -e 检测文件是否存在
   
shell流程控制
-------------

**if-else**::

	if condition
	then
	    command1 
	    command2
	    ...
	    commandN
	else
	    command
	fi

**if-elseif**::

	if condition1
	then
	    command1
	elif condition2 
	then 
	    command2
	else
	    commandN
	fi

**for**::

	for var in item1 item2 ... itemN
	do
	    command1
	    command2
	    ...
	    commandN
	done

或者::

	#!/bin/bash
	for((i=1;i<=5;i++));do
	    echo "这是第 $i 次调用";
	done;

**while**::

	while condition
	do
	    command
	done

**until**::

	until condition
	do
	    command
	done

**case**::

	case 值 in
	模式1)
	    command1
	    command2
	    ...
	    commandN
	    ;;
	模式2）
	    command1
	    command2
	    ...
	    commandN
	    ;;
	esac

**break**

**continue**

shell函数
---------

**函数定义**::

	[ function ] funname [()]
	{
	    action;
	    [return int;]
	}

如果省略掉return语句，将返回最后一条命令的执行结果。

**函数返回值**

函数返回值通过$?来获取

**函数参数**

函数参数在函数内部通过$n的方式来获取。当n>=10时，需要使用${n}来获取参数

shell重定向
-----------

#. command > file 命令重定向输出到file
#. command < file 命令输入重定向到file
#. command >> file 命令输出以追加的方式重定向到file
#. n > file, 描述符为n的文件重定向到file
#. n >> fle   描述符为n的文件以追加的方式重定向到file
#. n&>m 输出文件n和m合并
#. n<&m 输入文件n和m合并

**标准输出和标准错误合并**::

	command > file 2>&1

**屏蔽标准输出和标准错误**::

	command > /dev/null 2>&1

shell文件包含
-------------

引入其他文件的方式::

	. filename   # 注意点号(.)和文件名中间有一空格

或者::

	source filename
