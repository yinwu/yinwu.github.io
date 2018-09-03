Linux常用工具.命令
=============================

linux 文件目录
--------------

#. /bin usr/bin /sbin/ /user/sbin 

    用户或者管理员可执行执行文件目录。

#. /etc

    系统管理配置文件。
    
#. /lib
   
    linux系统中用户的动态链接库。

#. /opt 

    主机额外安装软件的目录。

#. /proc

    虚拟目录，系统内存的影射。可以直接访问这个目录来获取系统信息。这个系统的内容不再硬盘上，而在内存里面。

#. /boot

    系统启动时需要的一些核心文件。

#. /dev
   
    系统外部设备

#. /mnt

    系统挂在目录

windows下面putty 免密登录
-------------------------

putty免密登录搞定，步骤如下

1. 生成public key及 private key。

2. 将public key拷贝到server上面。

3. 在putty中，制定private的路径，然后保存。
   
4. 搞定。

linux下ssh免密登录
------------------

1. 生成public key和private key证书

.. code-block:: console
    
    ssh-keygen -t rsa

2. 传输public key到远程机器，并且追加写入authorized_keys文件中。

.. code-block:: console

    ssh-copy-id -i ~/.ssh/id_rsa.pub tester@10.159.2xx.2xx

3. 搞定。
   

Linux下SSH登录别名配置
----------------------

修改~/.ssh/config文件，在文件中追加以下信息

.. code-block:: console

    Host    别名
        HostName        主机名
        Port            端口
        User            用户名
        IdentityFile    密钥文件的路径


linux查看硬件配置信息
----------------------------

#. CPU信息

.. code-block:: console
	:emphasize-lines: 1

	~@~:~/doc$ lscpu
	Architecture:          x86_64
	CPU op-mode(s):        32-bit, 64-bit
	Byte Order:            Little Endian
	...

#. 内存信息

.. code-block:: console
	:emphasize-lines: 1
	
	~@~:~/doc$ cat /proc/meminfo
	MemTotal:        3970012 kB
	MemFree:          140060 kB
	MemAvailable:     777144 kB
	Buffers:          692976 kB
	Cached:           293716 kB
	SwapCached:         8264 kB


#. 硬盘信息

.. code-block:: console
	:emphasize-lines: 1

	~@~:~/doc$ lsblk
	NAME   MAJ:MIN RM   SIZE RO TYPE MOUNTPOINT
	sr0     11:0    1  1024M  0 rom  
	sda      8:0    0 298.1G  0 disk 
	|--sda2   8:2    0     1K  0 part 
	|--sda5   8:5    0     4G  0 part [SWAP]
	|--sda1   8:1    0 294.2G  0 part /



linux 文本处理利器之sed
------------------------

linux 文本处理利器之cut
------------------------

cut命令是一个选取命令，其功能是将文件中的每一行“字节” “字符” “字符” 进行剪切，选取我们需要的，并将这些选取好的数据输出至标准输出


格式
^^^^^^

    `cut -[n]b file`

    `cut -c file`

    `cut -d[分隔符] -f[域] file`

参数解释
^^^^^^^^^^^^^

**-b(bytes)**

    以字节为单位进行分割。这些字节位置将忽略多字节字符边界，除非也指定了 -n 标志。

**-c(characters)**

    以字符为单位进行分割。

**-d**

    自定义分隔符，默认为制表符。

**-f(filed)**

    -d一起使用，指定显示哪个区域。

**-n**

    取消分割多字节字符。仅和 -b 标志一起使用。如果字符的最后一个字节落在由 -b 标志的 List 参数指示的范围之内，该字符将被写出；否则，该字符将被排除。

举例
^^^^^^^^

原始文本

.. code-block:: console

    yinwu@yinwu-ThinkPad-E475:~/test$ cat text1.txt 
    557adfhg
    bcd5464b
    135465453456
    233546576
    yinwu@yinwu-ThinkPad-E475:~/test$

    yinwu@yinwu-ThinkPad-E475:~/test$ cat text2.txt 
    星期一
    星期二
    星期三
    星期四
    星期五
    星期六
    星期日
    yinwu@yinwu-ThinkPad-E475:~/test$ 
   
剪切单个字节

.. code-block:: console

    yinwu@yinwu-ThinkPad-E475:~/test$ cut -b 1 text1.txt 
    5
    b
    1
    2
    yinwu@yinwu-ThinkPad-E475:~/test$ 

剪切多个字节

.. code-block:: console

    yinwu@yinwu-ThinkPad-E475:~/test$ cut -b 1,3,5 text1.txt 
    57d
    bd4
    156
    234
    yinwu@yinwu-ThinkPad-E475:~/test$


    yinwu@yinwu-ThinkPad-E475:~/test$ cut -b 1-5 text1.txt 
    557ad
    bcd54
    13546
    23354
    yinwu@yinwu-ThinkPad-E475:~/test$


    yinwu@yinwu-ThinkPad-E475:~/test$ cut -b -5 text1.txt 
    557ad
    bcd54
    13546
    23354
    yinwu@yinwu-ThinkPad-E475:~/test$ 

    yinwu@yinwu-ThinkPad-E475:~/test$ cut -b 3- text1.txt 
    7adfhg
    d5464b
    5465453456
    3546576


剪切字符

首先按照上面的例子对test2.txt进行操作，看有什么现象

.. code-block:: console

    yinwu@yinwu-ThinkPad-E475:~/test$ cut -b 2 text2.txt 
    �
    �
    �
    �
    �
    �
    �

出现了乱码的现象，因为-b 只是针对字节进行裁剪，对一个汉字进行字节裁剪，得到的结果必然是乱码，若想使用 -b 命令对字节进行裁剪，那么则需要使用 -n 选项，此选项的作用是取消分割多字节字符

.. code-block:: console

    [root@localhost shell]# cut -nb 3 test2.txt 

    星
    星
    星
    星
    星
    星
    [root@localhost shell]# cut -nb 3,6  test2.txt 
    星
    星期
    星期
    星期
    星期
    星期
    星期
    [root@localhost shell]# cut -nb 3,6,9  test2.txt 
    星期
    星期二
    星期三
    星期四
    星期五
    星期六
    星期日
    [root@localhost shell]# cut -nb 3,6,9,12  test2.txt 
    星期一
    星期二
    星期三
    星期四
    星期五
    星期六
    星期日
    [root@localhost shell]# 

使用-c的来剪切字符，和上面的 -nb 有些类似

.. code-block:: console
    
    [root@localhost shell]# cut -c 1 test2.txt 

    星
    星
    星
    星
    星
    星
    [root@localhost shell]# cut -c 2 test2.txt 
    星
    期
    期
    期
    期
    期
    期
    [root@localhost shell]# cut -c 1-3 test2.txt 
    星期
    星期二
    星期三
    星期四
    星期五
    星期六
    星期日
    [root@localhost shell]# 
    
上面的-b -c 只是针对于格式固定的数据中剪切，但是对于一些格式不固定的，就没有办法获取到我们想要的数据，因此便有了 -f 域的概念

.. code-block::console

    yinwu@yinwu-ThinkPad-E475:~/test$ cat /etc/passwd | head -n 3
    root:x:0:0:root:/root:/bin/bash
    daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
    bin:x:2:2:bin:/bin:/usr/sbin/nologin
    yinwu@yinwu-ThinkPad-E475:~/test$ 

例如将上面的第一个 ： 前面的字符给剪切出来，那么我们就可以使用 -d 命令，指定其分割符为 ： 然后再选取第一个域内的内容即可，如下

.. code-block::console

    yinwu@yinwu-ThinkPad-E475:~/test$ cat /etc/passwd | head -n 3 | cut -d : -f 1
    root
    daemon
    bin
    yinwu@yinwu-ThinkPad-E475:~/test$ 

剪切ip地址，如下

.. code-block::console

    yinwu@yinwu-ThinkPad-E475:~/test$ ifconfig wlp4s0 | grep "inet "
    inet 192.168.1.103  netmask 255.255.255.0  broadcast 192.168.1.255
    
    yinwu@yinwu-ThinkPad-E475:~/test$ ifconfig wlp4s0 | grep "inet " | cut -d " " -f 10
    192.168.1.103
    yinwu@yinwu-ThinkPad-E475:~/test$ 


linux文本处理终极大招之awk
-----------------------------
