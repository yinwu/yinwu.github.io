Sphinx + Gitlub搭建自己的博客
==============================


为什么Sphinx
---------------

单位的文档一直用sphinx，这么多年用习惯了。 并且本人很喜欢Sphinx的简单，优雅的布局。


以前了解过Markdown，长时间不用就忘了。 不清楚markdown能不能支持文档的嵌套（在一个md文件中，引用同目录或者同工程下面另外的md文件），这次搭建博客时调查了一下，结论是需要其他工具的支持。markdown原生的语法中是不支持md文档之间的嵌套和引用的。我不喜欢把所有的东西都放一个page里面。Sphinx对这个支持就比较好。你可以按照自己的想法组织文档目录结构。


**注意** 这个Sphinx是用python实现的一个写文档的工具，还有一个同名的软件，是用来做中文分词的，百度搜索的时候，经常把这两个搞混。


参考的文档
------------

`文档整体解决方案(readthedocs,github,sphinx)使用`_


为什么不用ReadTheDoc
----------------------
	
我ReadTheDoc账户都已经申请了，但是最后时刻放弃了。最主要的原因就是，在单位访问ReadTheDoc没有问题，但是回家后发现ReadTheDoc断断续续的打不开，很影响用户体验。而且因为墙的存在，说不定那天ReadTheDoc就不让访问了呢。Github被封禁过一回，后来迫于压力解封了，相对来说安全一些。所以就尝试用Sphinx+github。


怎么在Github上部署Sphinx生成的网页
------------------------------------

在Github大家更习惯用markdown，观察了下用markdown写的博客，最终还是生成html页面。在工程目录下面有个index.html网页，这个网页里面内容就是打开博客后看到的内容。Sphinx也是类似，本地编译后生成一个index.html，只不过目录是在工程目录/build/html目录下面。Github展示的都是静态的网页，根本不关心你的网页是用sphinx生成的，还是Hexo生成的。所以问题就好办了，想办法用Sphinx生成的网页替换掉工程目录下面的index.html及其他文件就能解决问题。


这个过程中参考了 `Publishing sphinx-generated docs on github`_ ， 不过该作者的解决办法是，建立两个project。一个工程存放sphinx生成的静态网页文件，一个工程存放源文件(.rst)。我觉这种太麻烦，写文档时需要clone两个工程，对两个工程的目录也有要求，提交时也需要提交两次。对懒人是种折磨。

怎么能只clone一次，push一次呢？ 解决办法就是巧妙组织文档目录，然后修改工程的Makrfile。不能在Github工程根目录下直接创建Sphinx工程。而是在新建一个子目录，在子目录下面创建Sphinx工程，然后把sphinx生成的/build/html下面的所有文件拷贝到github工程的根目录下面。这样github根目录下面就有了静态网页文件。这个拷贝的过程也不需要手动去做，直接修改makefile或make.bat文件即可。

* Makefile 修改

.. code-block:: makefile
	:emphasize-lines: 17

	# Minimal makefile for Sphinx documentation
	#

	# You can set these variables from the command line.
	SPHINXOPTS    =
	SPHINXBUILD   = sphinx-build
	SPHINXPROJ    = Blog
	SOURCEDIR     = source
	BUILDDIR      = build

	# Put it first so that "make" without argument is like "make help".
	help:
		@$(SPHINXBUILD) -M help "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)

	.PHONY: help Makefile

	# Catch-all target: route all unknown targets to Sphinx using the new
	# "make mode" option.  $(O) is meant as a shortcut for $(SPHINXOPTS).
	%: Makefile
		@$(SPHINXBUILD) -M $@ "$(SOURCEDIR)" "$(BUILDDIR)" $(SPHINXOPTS) $(O)
		cp ./build/html/* ../ -rf
		echo "copy done"



* Github工程根目录(gitProject)，子目录doc是Sphinx工程所在目录。

.. code-block:: console

	～@～:~/gitProject$ ls
	algorithm  cPlusPlus  doctrees       index.html  objects.inv  search.html     _sources
	blog       doc        genindex.html  link        python       searchindex.js  _static




* 在doc子目录下面, 创建Sphinx工程，其中source目录是rst文件所在目录。build/html是生成静态网页文件所在目录。

.. code-block:: console

	~@~:~/doc$ ls doc
	build  make.bat  Makefile  source



* 把build/html下面的所有东西拷贝到gitProject下面

.. code-block:: console

	~@~:~/doc$ ls doc/build/html/
	algorithm  cPlusPlus      index.html  objects.inv  search.html     _sources
	blog       genindex.html  link        python       searchindex.js  _static



碰到的问题
------------

* 中文的支持

	我一开始是在Windows下面搭建的Sphinx环境，但是编译(make html)时，文档中的中文无法识别，编译后中文字符全变成了“？”。 在网上搜索了一个下午，也没有找到解决办法。而且相关文档特别少，怀疑不是sphinx的问题。后来放弃了，无奈在linux环境下试了一下，中文字符的处理没有任何问题。现在怀疑还是sphinx Windows版本的问题，不过不想继续调查研究了。



.. _文档整体解决方案(readthedocs,github,sphinx)使用: https://www.cnblogs.com/youxin/p/3594161.html

.. _Publishing sphinx-generated docs on github: http://daler.github.io/sphinxdoc-test/includeme.html