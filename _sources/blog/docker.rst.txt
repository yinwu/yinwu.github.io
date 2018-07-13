Docker技术
==============

docker常用命令
------------------------------

* -t:在新容器内指定一个伪终端或终端。

* -i:允许你对容器内的标准输入 (STDIN) 进行交互

* 在容器内使用docker logs命令，查看容器内的标准输出

* 我们使用 docker stop 命令来停止容器

* -d:让容器在后台运行。

* -P:将容器内部使用的网络端口映射到我们使用的主机上

* 我们也可以指定 -p 标识来绑定指定端口

* docker port 可以查看指定 （ID或者名字）容器的某个确定端口映射到宿主机的端口号

* docker top 来查看容器内部运行的进程

* docker inspect 来查看Docker的底层信息。它会返回一个 JSON 文件记录着 Docker 容器的配置和状态信息

* docker rm 命令来删除不需要的容器

* docker images 来列出本地主机上的镜像

* docker pull 命令来下载repository上面的镜像

* docker search 命令来搜索镜像

* 当我们从docker镜像仓库中下载的镜像不能满足我们的需求时，我们可以通过以下两种方式对镜像进行更改。

	1.从已经创建的容器中更新镜像，并且提交这个镜像

	2.使用 Dockerfile 指令来创建一个新的镜像

* docker commit来提交容器副本

* 我们可以使用 docker tag 命令，为镜像添加一个新的标签

* 我们也可以使用 -p 标识来指定容器端口绑定到主机端口

	-P :是容器内部端口随机映射到主机的高端口。

	-p : 是容器内部端口绑定到指定的主机端口。

* docker有一个连接系统允许将多个容器连接在一起，共享连接信息。docker连接会创建一个父子关系，其中父容器可以看到子容器的信息

* 我们也可以使用–name标识来命名容器


Docker install
--------------------

#. 安装命令

.. code-block:: console

    yinwu@yinwu-ThinkPad-E475:~$ sudo snap install docker
    docker 17.06.2-ce from 'docker-inc' installed


#. 查看版本

.. code-block:: console

    yinwu@yinwu-ThinkPad-E475:~$ docker -v
    Docker version 17.06.2-ce, build a04f55b


#. Hello world

.. code-block:: console

    yinwu@yinwu-ThinkPad-E475:~$ sudo docker run ubuntu:15.10 /bin/echo "Hello world"
    Unable to find image 'ubuntu:15.10' locally
    15.10: Pulling from library/ubuntu
    7dcf5a444392: Pull complete 
    759aa75f3cee: Pull complete 
    3fa871dc8a2b: Pull complete 
    224c42ae46e7: Pull complete 
    Digest: sha256:02521a2d079595241c6793b2044f02eecf294034f31d6e235ac4b2b54ffc41f3
    Status: Downloaded newer image for ubuntu:15.10
    Hello world

#. reference document

安装命令的提示来自shell中输入docker.

.. code-block:: console
    :emphasize-lines: 5,6

    yinwu@yinwu-ThinkPad-E475:~$ docker

    Command 'docker' not found, but can be installed with:

    sudo snap install docker     # version 17.06.2-ce, or
    sudo apt  install docker.io

    See 'snap info docker' for additional versions.

    yinwu@yinwu-ThinkPad-E475:~$ 


Docker compose
----------------------

#. `Overview`_

#. `Docker-compose file`_

#. `command line reference`_

.. _Overview: https://docs.docker.com/compose/overview/#release-notes

.. _Docker-compose file: https://docs.docker.com/compose/compose-file/

.. _command line reference: https://docs.docker.com/compose/reference/


