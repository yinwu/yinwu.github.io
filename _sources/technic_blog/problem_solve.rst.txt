环境配置及常见问题
=========================


`长时间不操作SSH无响应问题解决`_
------------------------------------

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

.. _这里: http://www.talkwithtrend.com/Question/225451-1370171

.. _长时间不操作SSH无响应问题解决: https://blog.csdn.net/u013511989/article/details/79972435


Windows10 & ubuntu双系统搭建
--------------------------------

需要注意的问题

	#. 最新的安装不需要制作USB启动盘，把ISO文件拷贝过去，然后解压就可以了。
	#. 选择跟window10系统共存，不需要自己分割磁盘。
	#. 话说我现在不知道自己把系统装什么地方去了。在windows下面看不见linux的安装文件。
	#. 在BIOS中设置优先启动Ubuntu。这样有选项提示你启动windows。如果选择优先启动windows，则会直接进入windows系统，不会提示你选择进入unbuntu。



How to install sublime in unbuntu
---------------------------------------------

	The installed package for linux can't be opened from toplap. Please reference to
	`linux下sublime text 3安装到配置 <https://www.cnblogs.com/shenckicc/p/6032998.html>`_


How to remove software in ububtu
-----------------------------------

.. code-block:: console

	sudo apt-get remove software_name


Adding sublime到鼠标右键
------------------------

.. code-block:: console

	Windows Registry Editor Version 5.00
	[HKEY_CLASSES_ROOT\*\shell\SublimeText3]
	@="Open with SublimeText3 "
	"Icon"="C:\\Program Files\\Sublime Text 3\\sublime_text.exe,0"
	[HKEY_CLASSES_ROOT\*\shell\SublimeText3\command]
	@="C:\\Program Files\\Sublime Text 3\\sublime_text.exe %1"
	[HKEY_CLASSES_ROOT\Directory\shell\SublimeText3]
	@="Open with SublimeText3 "
	"Icon"="C:\\Program Files\\Sublime Text 3\\sublime_text.exe,0"
	[HKEY_CLASSES_ROOT\Directory\shell\SublimeText3\command]

	@="C:\\Program Files\\Sublime Text 3\\sublime_text.exe %1"












