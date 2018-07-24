REDIS KEY-VALUE数据库
========================

Redis五种数据类型
--------------------------

#. string
^^^^^^^^^^^

    string是redis最基本的类型，你可以理解成与Memcached一模一样的类型，一个key对应一个value。

    string类型是**二进制安全**的。意思是redis的string可以包含任何数据。比如jpg图片或者序列化的对象 。

    string类型是Redis最基本的数据类型，一个键最大能存储512MB。 

    .. code-block:: console

	    redis 127.0.0.1:6379> SET name "runoob"
	    OK
	    redis 127.0.0.1:6379> GET name
	    "runoob"

#. hash
^^^^^^^^^^^

    Redis hash 是一个**键值对集合**。

    Redis hash 是一个string类型的field 和value的映射表，hash特别适合用于存储对象。

    .. code-block:: console

        redis> HMSET myhash field1 "Hello" field2 "World"
        "OK"
        redis> HGET myhash field1
        "Hello"
        redis> HGET myhash field2
        "World"

#. list
^^^^^^^^^^^

    Redis列表是简单的字符串列表，按照插入顺序排序。
    你可以添加一个元素到列表的头部（左边）或者尾部（右边)。类似**双向链表**。

    .. code-block::console

        redis 127.0.0.1:6379> lpush runoob redis
        (integer) 1
        redis 127.0.0.1:6379> lpush runoob mongodb
        (integer) 2
        redis 127.0.0.1:6379> lpush runoob rabitmq
        (integer) 3
        redis 127.0.0.1:6379> lrange runoob 0 10
        1) "rabitmq"
        2) "mongodb"
        3) "redis"
        redis 127.0.0.1:6379>

#. set
^^^^^^^^^^^
    
    Redis的set是string类型的无序集合。集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。

    .. code-block::console
    
        redis 127.0.0.1:6379> sadd runoob redis
        (integer) 1
        redis 127.0.0.1:6379> sadd runoob mongodb
        (integer) 1
        redis 127.0.0.1:6379> sadd runoob rabitmq
        (integer) 1
        redis 127.0.0.1:6379> sadd runoob rabitmq
        (integer) 0
        redis 127.0.0.1:6379> smembers runoob

        1) "redis"
        2) "rabitmq"
        3) "mongodb"


#. zset
^^^^^^^^^^^^
    
    Redis zset和set一样也是string类型元素的集合,且不允许重复的成员。

    不同的是每个元素都会关联一个double类型的分数。
    redis正是通过分数来为集合中的成员进行从小到大的排序。

    zset的成员是唯一的,但分数(score)却可以重复

    .. code-block:: console

        redis 127.0.0.1:6379> zadd runoob 0 redis
        (integer) 1
        redis 127.0.0.1:6379> zadd runoob 0 mongodb
        (integer) 1
        redis 127.0.0.1:6379> zadd runoob 0 rabitmq
        (integer) 1
        redis 127.0.0.1:6379> zadd runoob 0 rabitmq
        (integer) 0
        redis 127.0.0.1:6379> > ZRANGEBYSCORE runoob 0 1000
        1) "mongodb"
        2) "rabitmq"
        3) "redis"

Redis发布订阅
-------------------

Redis 发布订阅(pub/sub)是一种消息通信模式：发送者(pub)发送消息，订阅者(sub)接收消息。

订阅
^^^^^^^

.. code-block:: console

    redis 127.0.0.1:6379> SUBSCRIBE redisChat

    Reading messages... (press Ctrl-C to quit)
    1) "subscribe"
    2) "redisChat"
    3) (integer) 1

发布
^^^^^^^

.. code-block:: console

    redis 127.0.0.1:6379> PUBLISH redisChat "Redis is a great caching technique"

    (integer) 1

    redis 127.0.0.1:6379> PUBLISH redisChat "Learn redis by runoob.com"

    (integer) 1


Redis事务
------------------------

Redis 事务可以一次执行多个命令， 并且带有以下三个重要的保证：

    * 批量操作在发送 EXEC 命令前被放入队列缓存。
    * 收到 EXEC 命令后进入事务执行，事务中任意命令执行失败，其余的命令依然被执行。
    * 在事务执行过程，其他客户端提交的命令请求不会插入到事务执行命令序列中。

一个事务从开始到执行会经历以下三个阶段：

    * 开始事务
    * 命令入队
    * 执行事务

单个 Redis 命令的执行是原子性的，但 Redis 没有在事务上增加任何维持原子性的机制，所以 Redis 事务的执行并不是原子性的。

事务可以理解为一个打包的批量执行脚本，但批量指令并非原子化的操作，中间某条指令的失败不会导致前面已做指令的回滚，也不会造成后续的指令不做。

.. code-block:: console

    redis 127.0.0.1:6379> MULTI
    OK

    redis 127.0.0.1:6379> SET book-name "Mastering C++ in 21 days"
    QUEUED

    redis 127.0.0.1:6379> GET book-name
    QUEUED

    redis 127.0.0.1:6379> SADD tag "C++" "Programming" "Mastering Series"
    QUEUED

    redis 127.0.0.1:6379> SMEMBERS tag
    QUEUED

    redis 127.0.0.1:6379> EXEC
    1) OK
    2) "Mastering C++ in 21 days"
    3) (integer) 3
    4) 1) "Mastering Series"
       2) "C++"
       3) "Programming"

Redis 连接
-------------------------


redis数据备份
-------------------------


redis安全
-------------------------


redis客户端
-------------------------


redis管道技术
-------------------------

redis分区
-------------------------


python中使用redis
-------------------------

