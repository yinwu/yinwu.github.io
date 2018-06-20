教育.技术
===========


技术
------

* `Linux的任督二脉：进程调度和内存管理`_


* `长时间不操作SSH无响应问题解决`_

#. 如果您有多台服务器，不想在每台服务器上设置，只需在客户端的 ~/.ssh/ 文件夹中添加 config 文件，并添加下面的配置:

	.. code-block:: console

		ServerAliveInterval 60

#. 如果您有多台个人管理服务器，不想在每个客户端进行设置，只需在服务器的 /etc/ssh/sshd_config 中添加如下的配置:

	.. code-block:: console

		ServerAliveInterval 60

#. 如果您只想让当前的 ssh 保持连接，可以使用以下的命令：

	.. code-block:: console

		ssh -o ServerAliveInterval=60 user@sshserver

	转载自 http://www.talkwithtrend.com/Question/225451-1370171


教育
--------

.. _Linux的任督二脉：进程调度和内存管理: https://blog.csdn.net/21cnbao/article/details/77505330

.. _长时间不操作SSH无响应问题解决: https://blog.csdn.net/u013511989/article/details/79972435