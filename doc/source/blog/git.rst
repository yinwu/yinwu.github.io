Git - Just do IT
===================

关于Git，一直记得一件事情。某年参加公司一个活动，讨论的主题好像是集中一堆编程水平高的工程师，做一个项目。会上一哥们，提起公司一直使用svn，特别不齿。
并宣称不会用GIT的人不能叫程序员。直接喷倒一大片同事。虽然我不排斥新技术，新工具，但是不认同这句话。
工具要选择适合的，公司的很多项目其实不太适合用GIT，但是真正的程序员还是要掌握GIT的，这个毋庸置疑。这些年断断续续使用github，只会一些简单的操作。
随着公司使用GIT的项目越来越多，急需掌握一些复杂的GIT操作。这个日志用来记录自己GIT学习路径。


写在学习完廖雪峰的Git教程后的知识
--------------------------------

* Git的强项不在于分布式，所谓的分布式是个伪命题。产品开发中，所有的提交最终还是要集中起来，保存到远端。 所谓分布式保存，没有意义。
* GIt的本地分支管理确实强大，这个比SVN要强非常多。一个working copy管理所有分支。

1 Git tourist
--------------

	`Git Book <https://git-scm.com/book/zh/v1/%E8%B5%B7%E6%AD%A5>`_

2 How to pull and switch remote branch?
---------------------------------------

Add remote branch
^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	git remote add origin git@server-name:path/repo-name.git

push local branch to remote
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	git push -u origin master

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


How to rename a branch
^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	$ git branch -m remotes/origin/JIRA-Support Jira-support


3 Git configuration when you first use it
------------------------------------------------

How to set git editor first time
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	$ git config --global core.editor vim

	参考 `起步 - 初次运行 Git 前的配置 <https://git-scm.com/book/zh/v1/%E8%B5%B7%E6%AD%A5-%E5%88%9D%E6%AC%A1%E8%BF%90%E8%A1%8C-Git-%E5%89%8D%E7%9A%84%E9%85%8D%E7%BD%AE>`_


4 Git diff
--------------


How to diff the commit change and working copy
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	git diff HEAD -- readme.txt
	

5 Git revert
--------------------

回撤工作区的修改 git checkout -- your_file

回撤暂存区的修改 get reset HEAD your_file/ get checkout your_file

回撤提交区的修改 get reset --hard HEAD^/HEAD^^/HEAD^^^

6 Git branch operation
-------------------------

查看分支：git branch

创建分支：git branch <name>

切换分支：git checkout <name>

创建+切换分支：git checkout -b <name>

合并某分支到当前分支：git merge <name>

删除分支：git branch -d <name>

强行删除没有合并的分支 git branch -D feature-vulcan

7 Git fix confict
---------------------------

查看分支合并图 git log --graph --pretty=oneline --abbrev-commit


8 Git work flow
--------------------

.. images:: ../_static/git_work_flow.png

9 Git 保存工作区
--------------------

git stash可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作。

git stash list 查看工作现场

git stash apply stash@{0}/git stash drop

git stash pop 恢复现场的同时删除stash

10 在本地创建远程的DEV分支
------------------------------

导出 git checkout -b dev origin/dev


提交 git push origin dev


set up-stream to a local branch
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: console

	yinwu@~ MINGW64 /d/QGP/JiraSupport/qgp (Jira-support)
	$ git branch --set-upstream-to=remotes/origin/JIRA-Support Jira-support
	Branch Jira-support set up to track remote branch JIRA-Support from origin.

多人协作模式总结
-----------------------------

    首先，可以试图用git push origin <branch-name>推送自己的修改；

    如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；

    如果合并有冲突，则解决冲突，并在本地提交；

    没有冲突或者解决掉冲突后，再用git push origin <branch-name>推送就能成功！

	如果git pull提示no tracking information，则说明本地分支和远程分支的链接关系没有创建，
	用命令git branch --set-upstream-to <branch-name> origin/<branch-name>。


Git tag
-----------------------------

    命令git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id；

    命令git tag -a <tagname> -m "blablabla..."可以指定标签信息；

    命令git tag可以查看所有标签。

    命令git push origin <tagname>可以推送一个本地标签；

    命令git push origin --tags可以推送全部未推送过的本地标签；

    命令git tag -d <tagname>可以删除一个本地标签；

    命令git push origin :refs/tags/<tagname>可以删除一个远程标签。

Git alias
-------------

$ git config --global alias.co checkout
$ git config --global alias.ci commit
$ git config --global alias.br branch

.. code-block:: console

	git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
	
Git 配置文件路径
-------------------

.git/config or .gitconfig(global configuration)
