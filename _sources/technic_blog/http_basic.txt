HTTP 基础知识
=============

URL（资源标识符）
---------------

`schema://host[:port#]/path/.../[?query-string][#anchor]`

#. scheme        指定低层使用的协议(例如：http, https, ftp)

#. host          HTTP服务器的IP地址或者域名

#. port         HTTP服务器的默认端口是80，这种情况下端口号可以省略。如果使用了别的端口，必须指明，例如 http://www.cnblogs.com:8080/

#. path          访问资源的路径

#. query-string  发送给http服务器的数据

#. anchor-       锚


http消息结构
------------

#. **method**

#. **header**

#. **body**

response 状态码
---------------

#. 1XX  提示信息 - 表示请求已被成功接收，继续处理
#. 2XX  成功 - 表示请求已被成功接收，理解，接受
#. 3XX  重定向 - 要完成请求必须进行更进一步的处理
#. 4XX  客户端错误 -  请求有语法错误或请求无法实现
#. 5XX  服务器端错误 -   服务器未能实现合法的