Git - Just do IT
===================

关于Git，一直记得一件事情。某年参加公司一个活动，讨论的主题好像是集中一堆编程水平高的工程师，做一个项目。会上一哥们，提起公司一直使用svn，特别不齿。并宣称不会用GIT的人不能叫程序员。直接喷倒一大片同事。虽然我不排斥新技术，新工具，但是不认同这句话。工具要选择适合的，公司的很多项目其实不太适合用GIT，但是真正的程序员还是要掌握GIT的，这个毋庸置疑。这些年断断续续使用github，只会一些简单的操作。随着公司使用GIT的项目越来越多，急需掌握一些复杂的GIT操作。这个日志用来记录自己GIT学习路径。


How to pull and switch remote branch?
---------------------------------------

show all remote branch
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	[yinwu@~]$ git branch -a
	  JIRA-Support
	* master
	  remotes/origin/20180227html
	  remotes/origin/BUG-01
	  remotes/origin/BUG-01-a
	  remotes/origin/BUG-01-m
	  remotes/origin/DOD-01
	  remotes/origin/DOD02
	  remotes/origin/Fix-Auth

How to switch branch
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	[yinwu@qgp_dev qgp]$ git checkout -b remotes/origin/JIRA-Support
	Switched to a new branch 'remotes/origin/JIRA-Support'