交叉编译
===================

背景
------

１０年一个轮回，最近换工作，加入了新单位，又做起嵌入式项目来了。
现在手头的活是给一个嵌入式项目写单元测试用例，目标板的是32位ARM结构的板子。
如果你接触过嵌入式项目，你就知道嵌入式代码跟目标板紧密耦合，代码中大量奇奇怪怪的写法，在目标板上跑起来没有任何问题。
但是换个平台，分分钟钟崩溃的节奏。
虽然我们做项目一直在强调要考虑可移植性，但是实际状态就是，板子能跑起来，功能正常已经万事大吉了。再提别的要求不现实，重构什么的更谈不上。
ｃ语言本身就不是灵活有余，抽象不足，给ｃ代码写单元测试用例，更是比较别扭。 
Java、python都有比较成熟的测试框架，c++也有gtest,但是我本人没听过ｃ有比较流行的单元测试框架，也可能是我比较孤陋寡闻。有一些商业的框架，都是收费贼贵，不差钱的大公司可以考虑。

问题
-------

跑单元测试用例，代码崩了。访问了非法指针，用printf打印，指针没有问题，申请时和使用时，指针的值都是一样。

原因
-------

被printf("%x")给欺骗了。跑case的机器是64位，指针的值是48位的，代码中用int型变量保存这个指针，这种写法值得商榷，但是３２位系统中运行没有问题，导致指针值的高16位被截掉了。但是printf打印时，只打印低３２
位，所以出现指针的值没有问题的假象。实际上低３２位确实一样，但是高位已经不一样了。

解决办法
--------

虽然这种情况应该修改产品代码，但是...你懂的，我选择修改程序运行环境，把测试用例也编译成３２位可执行程序，在６４位机器上运行。

关键步骤
---------

修改编译选项
^^^^^^^^^^^^^^^^

在编译时，加上-m32的宏，告诉我们要编译３２位的可执行程序。

.. code-block: console

    add_definitions("-m32")


链接时，也需要加上链接的flag

.. code-block: console

    set(TEST_LINK_FLAGS "-Wl,-melf_i386")


修改库文件
^^^^^^^^^^^^^^^^^^^

测试框架是ｃｍｏｃｋａ，下载源码后自己编译的，当然是６４位可执行程序。无法跟３２位的测试用例链接到一起。在链接的时候报错。
需要重新编译ｃｍｏｃｋａ，想按照编译测试用例的方法一样修改ｃｍｏｃｋａ的ｃｍａｋｅ文件，但是失败了，原因不清楚。
后来发现ｃｍｏｋａ根目录下面有个文件叫*Toolchain-cross-m32.cmake*。原来ｃｍｏｃｋａ的早就考虑到各种平台的编译问题了，提供了一个
交叉编译文件，这样问题就变的非常简单了，在编译时指定交叉编译文件就搞定了ｃｍｏｋａ－３２程序。

.. code-block: console

    cmake -DCMAKE_TOOLCHAIN_FILE="../cmake/Toolchain-cross-m32.cmake" ..


Toolchain-cross-m32.cmake这个文件有参考意义，赋值到这里供以后参考

.. code-block: console

    set(CMAKE_C_FLAGS "-m32" CACHE STRING "C compiler flags"   FORCE)
    set(CMAKE_CXX_FLAGS "-m32" CACHE STRING "C++ compiler flags" FORCE)

    set(LIB32 /usr/lib) # Fedora

    if(EXISTS /usr/lib32)
        set(LIB32 /usr/lib32) # Arch, Solus
    endif()

    set(CMAKE_SYSTEM_LIBRARY_PATH ${LIB32} CACHE STRING "system library search path" FORCE)
    set(CMAKE_LIBRARY_PATH        ${LIB32} CACHE STRING "library search path"        FORCE)

    # this is probably unlikely to be needed, but just in case
    set(CMAKE_EXE_LINKER_FLAGS    "-m32 -L${LIB32}" CACHE STRING "executable linker flags"     FORCE)
    set(CMAKE_SHARED_LINKER_FLAGS "-m32 -L${LIB32}" CACHE STRING "shared library linker flags" FORCE)
    set(CMAKE_MODULE_LINKER_FLAGS "-m32 -L${LIB32}" CACHE STRING "module linker flags"         FORCE)

    # on Fedora and Arch and similar, point pkgconfig at 32 bit .pc files. We have
    # to include the regular system .pc files as well (at the end), because some
    # are not always present in the 32 bit directory
    if(EXISTS ${LIB32}/pkgconfig)
        set(ENV{PKG_CONFIG_LIBDIR} ${LIB32}/pkgconfig:/usr/share/pkgconfig:/usr/lib/pkgconfig:/usr/lib64/pkgconfig)
    endiF()

安装一些编译32位程序需要的库文件
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

这里主要是问度娘，参考文章还是很多的。这里吐槽一下，中文博客重复的太多了。有些人写博客就是把其他人的复制一份，连错误都不修改就放上去。

需要安装的库大概有下面几个：

.. code-block: console

    sudo apt-get install build-essential module-assistant
    sudo apt-get install gcc-multilib g++-multilib
    sudo apt-get install lib32ncurses5 lib32z1

网上很多人说要安装ia32-libs,实际上这个早已不用了，被lib32ncurses5 lib32z1替换掉了。

你以为结束了吗？
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

本以为到这里就结束了，结果还是没有编译成功，报的错误是

.. code-block: console

    /usr/bin/ld: i386:x86-64 architecture of input file /usr/lib/gcc/x86_64-linux-gnu/5/../../../x86_64-linux-gnu/crt1.o is incompatible with i386 output


在网上搜啊搜，没找到解决办法，我知道是库搜索路径不正确导致的，但是正确路径在哪里，怎么搜索一直都没有搞明白。实在没办法，想想还是
参考ｃｍｏｋａ的写法，在ｃｍａｋｅ中增加了下面的两段，成功解决问题。

.. code-block: console

    set(LIB32 /usr/lib32)

    set(CMAKE_EXE_LINKER_FLAGS    "-m32 -L${LIB32}" CACHE STRING "executable linker flags"     FORCE)
    set(CMAKE_SHARED_LINKER_FLAGS "-m32 -L${LIB32}" CACHE STRING "shared library linker flags" FORCE)
    set(CMAKE_MODULE_LINKER_FLAGS "-m32 -L${LIB32}" CACHE STRING "module linker flags"         FORCE)


至此成功解决６４位机器下面编译运行３２位程序的问题。
