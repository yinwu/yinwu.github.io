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


Link

`分享1 <http://www.itwechat.space/thread-9859155-1-2.html>`_
`分享2 <http://www.itwechat.space/thread-9858953-1-2.html>`_
`分享3 <http://www.itwechat.space/thread-9858392-1-3.html>`_
`分享4 <http://www.itwechat.space/thread-9843499-1-5.html>`_
`分享5 <http://www.itwechat.space/thread-9843404-1-5.html>`_
`分享6 <http://www.itwechat.space/thread-9843404-1-5.html>`_
`分享7 <http://www.itwechat.space/thread-9843246-1-6.html>`_
`分享8 <http://www.itwechat.space/thread-9843191-1-6.html>`_
`分享9 <http://www.itwechat.space/thread-9836468-1-9.html>`_
`分享10 <http://www.itwechat.space/thread-9797564-1-12.html>`_
`分享11 <http://www.itwechat.space/thread-9785452-1-13.html>`_
`分享12 <http://www.itwechat.space/thread-9784101-1-15.html>`_
`分享13 <http://www.itwechat.space/thread-9769075-1-16.html>`_
`分享13 <http://www.itwechat.space/thread-9749873-1-19.html>`_
`分享13 <http://www.itwechat.space/thread-9746982-1-21.html>`_
`分享13 <http://www.itwechat.space/thread-9746955-1-21.html>`_
`分享13 <http://www.itwechat.space/thread-9723552-1-23.html>`_
`分享13 <http://www.itwechat.space/thread-9723425-1-24.html>`_
`分享13 <http://www.itwechat.space/thread-9723354-1-24.html>`_









