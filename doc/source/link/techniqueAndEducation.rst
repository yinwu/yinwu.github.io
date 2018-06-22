教育.技术
===========


技术
------

`Linux的任督二脉：进程调度和内存管理`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

`长时间不操作SSH无响应问题解决`_
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

#. 如果您有多台服务器，不想在每台服务器上设置，只需在客户端的 ~/.ssh/ 文件夹中添加 config 文件，并添加下面的配置:

	.. code-block:: console

		ServerAliveInterval 60

#. 如果您有多台个人管理服务器，不想在每个客户端进行设置，只需在服务器的 /etc/ssh/sshd_config 中添加如下的配置:

	.. code-block:: console

		ServerAliveInterval 60

#. 如果您只想让当前的 ssh 保持连接，可以使用以下的命令：

	.. code-block:: console

		ssh -o ServerAliveInterval=60 user@sshserver

	转载自`这里`_


linux查看硬件配置信息
^^^^^^^^^^^^^^^^^^^^^^^

* CPU信息

.. code-block:: console
	:emphasize-lines: 1

	~@~:~/doc$ lscpu
	Architecture:          x86_64
	CPU op-mode(s):        32-bit, 64-bit
	Byte Order:            Little Endian
	...

* 内存信息

.. code-block:: console
	:emphasize-lines: 1
	
	~@~:~/doc$ cat /proc/meminfo
	MemTotal:        3970012 kB
	MemFree:          140060 kB
	MemAvailable:     777144 kB
	Buffers:          692976 kB
	Cached:           293716 kB
	SwapCached:         8264 kB


* 硬盘信息

.. code-block:: console
	:emphasize-lines: 1

	~@~:~/doc$ lsblk
	NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
	sr0     11:0    1  1024M  0 rom  
	sda      8:0    0 298.1G  0 disk 
	|--sda2   8:2    0     1K  0 part 
	|--sda5   8:5    0     4G  0 part [SWAP]
	|--sda1   8:1    0 294.2G  0 part /


教育
--------




.. _Linux的任督二脉：进程调度和内存管理: https://blog.csdn.net/21cnbao/article/details/77505330

.. _长时间不操作SSH无响应问题解决: https://blog.csdn.net/u013511989/article/details/79972435

.. _这里： http://www.talkwithtrend.com/Question/225451-1370171