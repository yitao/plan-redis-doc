# 概述

Redis(Remote Dictionary Server)



## 相关资源

Redis 官网：https://redis.io/

Redis 在线测试：http://try.redis.io/

Redis 命令参考：http://doc.redisfans.com/



# 基本操作

## Redis keys 命令

下表给出了与 Redis 键相关的基本命令：（表格来源：[菜鸟教程](https://www.runoob.com/redis/redis-keys.html)）

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | DEL key<br>该命令用于在 key 存在时删除  key。                |
| 2    | DUMP key<br>序列化给定 key ，并返回被序列化的值。            |
| 3    | EXISTS key<br>检查给定 key 是否存在。                        |
| 4    | EXPIRE key seconds<br>为给定 key 设置过期时间，以秒计。      |
| 5    | EXPIREAT key timestamp<br/>EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)。 |
| 6    | PEXPIRE key milliseconds<br/>设置 key 的过期时间以毫秒计。   |
| 7    | PEXPIREAT key milliseconds-timestamp<br/>设置 key 过期时间的时间戳(unix timestamp) 以毫秒计 |
| 8    | KEYS pattern<br/>查找所有符合给定模式( pattern)的 key 。     |
| 9    | MOVE key db<br/>将当前数据库的 key 移动到给定的数据库 db 当中。 |
| 10   | PERSIST key<br/>移除 key 的过期时间，key 将持久保持。        |
| 11   | PTTL key<br/>以毫秒为单位返回 key 的剩余的过期时间。         |
| 12   | TTL key<br/>以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)。 |
| 13   | RANDOMKEY<br/>从当前数据库中随机返回一个 key 。              |
| 14   | RENAME key newkey<br/>修改 key 的名称                        |
| 15   | RENAMENX key newkey<br/>仅当 newkey 不存在时，将 key 改名为 newkey 。 |
| 16   | SCAN cursor [MATCH pattern] [COUNT count]<br/>迭代数据库中的数据库键。 |
| 17   | TYPE key<br/>返回 key 所储存的值的类型。                     |

更多命令请参考：https://redis.io/commands



# 数据类型



## 基础数据类型

### String

下表列出了常用的 redis 字符串命令：（表格来源：[菜鸟教程](https://www.runoob.com/redis/redis-strings.html)）

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | SET key value <br>设置指定 key 的值                          |
| 2    | GET key<br>获取指定 key 的值。                               |
| 3    | GETRANGE key start end<br/>返回 key 中字符串值的子字符       |
| 4    | GETSET key value<br/>将给定 key 的值设为 value ，并返回 key 的旧值(old value)。 |
| 5    | MGET key1 key2...<br/>获取所有(一个或多个)给定 key 的值。    |
| 6    | SETEX key seconds value<br/>将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)。 |
| 7    | SETNX key value<br/>只有在 key 不存在时设置 key 的值。       |
| 8    | SETRANGE key offset value<br/>用 value 参数覆写给定 key 所储存的字符串值，从偏移量 offset 开始。 |
| 9    | STRLEN key<br/>返回 key 所储存的字符串值的长度。             |
| 10   | MSET key value key value...<br/>同时设置一个或多个 key-value 对。 |
| 11   | MSETNX key value key value...<br/>同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。 |
| 12   | PSETEX key milliseconds value<br/>这个命令和 SETEX 命令相似，但它以毫秒为单位设置 key 的生存时间，而不是像 SETEX 命令那样，以秒为单位。 |
| 13   | INCR key<br/>将 key 中储存的数字值增一。                     |
| 14   | INCRBY key increment<br/>将 key 所储存的值加上给定的增量值（increment） 。 |
| 15   | INCRBYFLOAT key increment<br/>将 key 所储存的值加上给定的浮点增量值（increment） 。 |
| 16   | DECR key<br/>将 key 中储存的数字值减一。                     |
| 17   | DECRBY key decrement<br/>key 所储存的值减去给定的减量值（decrement） 。 |
| 18   | APPEND key value<br/>如果 key 已经存在并且是一个字符串， APPEND 命令将指定的 value 追加到该 key 原来值（value）的末尾。 |

> 思考:INCRBY的增量值是否可以为负数，浮点数？

###  List

一个列表最多可以包含 2^32^ - 1 个元素 (4294967295, 即42亿多)。

下表列出了列表相关的基本命令：

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | BLPOP key1 [key2...] timeout<br/>移出并获取列表的第一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |
| 2    | BRPOP key1 [key2...] timeout<br/>移出并获取列表的最后一个元素， 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |
| 3    | BRPOPBLPUSH source destination timeout<br/>从列表中弹出一个值，将弹出的元素插入到另外一个列表中并返回它； 如果列表没有元素会阻塞列表直到等待超时或发现可弹出元素为止。 |
| 4    | LINDEX key index<br/>通过索引获取列表中的元素                |
| 5    | LINSERT key BEFORE\|AFTER pivot value<br/>在列表的元素前或者后插入元素 |
| 6    | LLEN key<br/>获取列表长度                                    |
| 7    | LPOP key<br/>移出并获取列表的第一个元素                      |
| 8    | LPUSH key value1 value2...<br/>将一个或多个值插入到列表头部  |
| 9    | LPUSHX key value<br/>将一个值插入到已存在的列表头部          |
| 10   | LRANGE key start stop<br/>获取列表指定范围内的元素           |
| 11   | LREM key count value<br/>移除列表元素<br/>count > 0 : 从表头开始向表尾搜索，移除与 VALUE 相等的元素，数量为 COUNT 。<br/>count < 0 : 从表尾开始向表头搜索，移除与 VALUE 相等的元素，数量为 COUNT 的绝对值。<br/>count = 0 : 移除表中所有与 VALUE 相等的值。 |
| 12   | LSET key index value<br/>通过索引设置列表元素的值            |
| 13   | LTRIM key start stop<br/>对一个列表进行修剪(trim)，就是说，让列表只保留指定区间内的元素，不在指定区间之内的元素都将被删除。 |
| 14   | RPOP key<br/>移除列表的最后一个元素，返回值为移除的元素。    |
| 15   | RPOPLPUSH source destination<br/>移除列表的最后一个元素，并将该元素添加到另一个列表并返回 |
| 16   | RPUSH key value1 value2...<br/>在列表中添加一个或多个值      |
| 17   | RPUSHX key value<br/>为已存在的列表添加值                    |

###  Set

Redis 的 Set 是 String 类型的无序集合。集合成员是唯一的，这就意味着集合中不能出现重复的数据。

Redis 中集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是 O(1)。

无序集合中最大的元素个数为2^32^ - 1 个元素 (4294967295, 即42亿多)。

下表列出了 Redis 集合基本命令：

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | [SADD key member1 [member2\]](https://www.runoob.com/redis/sets-sadd.html)  向集合添加一个或多个成员 |
| 2    | [SCARD key](https://www.runoob.com/redis/sets-scard.html)  获取集合的成员数 |
| 3    | [SDIFF key1 [key2\]](https://www.runoob.com/redis/sets-sdiff.html)  返回第一个集合与其他集合之间的差异。 |
| 4    | [SDIFFSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sdiffstore.html)  返回给定所有集合的差集并存储在 destination 中 |
| 5    | [SINTER key1 [key2\]](https://www.runoob.com/redis/sets-sinter.html)  返回给定所有集合的交集 |
| 6    | [SINTERSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sinterstore.html)  返回给定所有集合的交集并存储在 destination 中 |
| 7    | [SISMEMBER key member](https://www.runoob.com/redis/sets-sismember.html)  判断 member 元素是否是集合 key 的成员 |
| 8    | [SMEMBERS key](https://www.runoob.com/redis/sets-smembers.html)  返回集合中的所有成员 |
| 9    | [SMOVE source destination member](https://www.runoob.com/redis/sets-smove.html)  将 member 元素从 source 集合移动到 destination 集合 |
| 10   | [SPOP key](https://www.runoob.com/redis/sets-spop.html)  移除并返回集合中的一个随机元素 |
| 11   | [SRANDMEMBER key [count\]](https://www.runoob.com/redis/sets-srandmember.html)  返回集合中一个或多个随机数 |
| 12   | [SREM key member1 [member2\]](https://www.runoob.com/redis/sets-srem.html)  移除集合中一个或多个成员 |
| 13   | [SUNION key1 [key2\]](https://www.runoob.com/redis/sets-sunion.html)  返回所有给定集合的并集 |
| 14   | [SUNIONSTORE destination key1 [key2\]](https://www.runoob.com/redis/sets-sunionstore.html)  所有给定集合的并集存储在 destination 集合中 |
| 15   | [SSCAN key cursor [MATCH pattern\] [COUNT count]](https://www.runoob.com/redis/sets-sscan.html)  迭代集合中的元素 |

### Sorted Set

Redis 有序集合和集合一样也是string类型元素的集合,且不允许重复的成员。

不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。

有序集合的成员是唯一的,但分数(score)却可以重复。

集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。 集合中最大的成员数为 232 - 1 (4294967295, 每个集合可存储40多亿个成员)。 



下表列出了 redis 有序集合的基本命令:

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | [ZADD key score1 member1 [score2 member2\]](https://www.runoob.com/redis/sorted-sets-zadd.html)  向有序集合添加一个或多个成员，或者更新已存在成员的分数 |
| 2    | [ZCARD key](https://www.runoob.com/redis/sorted-sets-zcard.html)  获取有序集合的成员数 |
| 3    | [ZCOUNT key min max](https://www.runoob.com/redis/sorted-sets-zcount.html)  计算在有序集合中指定区间分数的成员数 |
| 4    | [ZINCRBY key increment member](https://www.runoob.com/redis/sorted-sets-zincrby.html)  有序集合中对指定成员的分数加上增量 increment |
| 5    | [ZINTERSTORE destination numkeys key [key ...\]](https://www.runoob.com/redis/sorted-sets-zinterstore.html)  计算给定的一个或多个有序集的交集并将结果集存储在新的有序集合 destination 中 |
| 6    | [ZLEXCOUNT key min max](https://www.runoob.com/redis/sorted-sets-zlexcount.html)  在有序集合中计算指定字典区间内成员数量 |
| 7    | [ZRANGE key start stop [WITHSCORES\]](https://www.runoob.com/redis/sorted-sets-zrange.html)  通过索引区间返回有序集合指定区间内的成员 |
| 8    | [ZRANGEBYLEX key min max [LIMIT offset count\]](https://www.runoob.com/redis/sorted-sets-zrangebylex.html)  通过字典区间返回有序集合的成员 |
| 9    | [ZRANGEBYSCORE key min max [WITHSCORES\] [LIMIT]](https://www.runoob.com/redis/sorted-sets-zrangebyscore.html)  通过分数返回有序集合指定区间内的成员 |
| 10   | [ZRANK key member](https://www.runoob.com/redis/sorted-sets-zrank.html)  返回有序集合中指定成员的索引 |
| 11   | [ZREM key member [member ...\]](https://www.runoob.com/redis/sorted-sets-zrem.html)  移除有序集合中的一个或多个成员 |
| 12   | [ZREMRANGEBYLEX key min max](https://www.runoob.com/redis/sorted-sets-zremrangebylex.html)  移除有序集合中给定的字典区间的所有成员 |
| 13   | [ZREMRANGEBYRANK key start stop](https://www.runoob.com/redis/sorted-sets-zremrangebyrank.html)  移除有序集合中给定的排名区间的所有成员 |
| 14   | [ZREMRANGEBYSCORE key min max](https://www.runoob.com/redis/sorted-sets-zremrangebyscore.html)  移除有序集合中给定的分数区间的所有成员 |
| 15   | [ZREVRANGE key start stop [WITHSCORES\]](https://www.runoob.com/redis/sorted-sets-zrevrange.html)  返回有序集中指定区间内的成员，通过索引，分数从高到低 |
| 16   | [ZREVRANGEBYSCORE key max min [WITHSCORES\]](https://www.runoob.com/redis/sorted-sets-zrevrangebyscore.html)  返回有序集中指定分数区间内的成员，分数从高到低排序 |
| 17   | [ZREVRANK key member](https://www.runoob.com/redis/sorted-sets-zrevrank.html)  返回有序集合中指定成员的排名，有序集成员按分数值递减(从大到小)排序 |
| 18   | [ZSCORE key member](https://www.runoob.com/redis/sorted-sets-zscore.html)  返回有序集中，成员的分数值 |
| 19   | [ZUNIONSTORE destination numkeys key [key ...\]](https://www.runoob.com/redis/sorted-sets-zunionstore.html)  计算给定的一个或多个有序集的并集，并存储在新的 key 中 |
| 20   | [ZSCAN key cursor [MATCH pattern\] [COUNT count]](https://www.runoob.com/redis/sorted-sets-zscan.html)  迭代有序集合中的元素（包括元素成员和元素分值） |

### Hash

Redis hash 是一个 string 类型的 field（字段） 和 value（值） 的映射表，hash 特别适合用于存储对象。

Redis 中每个 hash 可以存储 232 - 1 键值对（40多亿）。



下表列出了 redis hash 基本的相关命令：

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | [HDEL key field1 [field2\]](https://www.runoob.com/redis/hashes-hdel.html)  删除一个或多个哈希表字段 |
| 2    | [HEXISTS key field](https://www.runoob.com/redis/hashes-hexists.html)  查看哈希表 key 中，指定的字段是否存在。 |
| 3    | [HGET key field](https://www.runoob.com/redis/hashes-hget.html)  获取存储在哈希表中指定字段的值。 |
| 4    | [HGETALL key](https://www.runoob.com/redis/hashes-hgetall.html)  获取在哈希表中指定 key 的所有字段和值 |
| 5    | [HINCRBY key field increment](https://www.runoob.com/redis/hashes-hincrby.html)  为哈希表 key 中的指定字段的整数值加上增量 increment 。 |
| 6    | [HINCRBYFLOAT key field increment](https://www.runoob.com/redis/hashes-hincrbyfloat.html)  为哈希表 key 中的指定字段的浮点数值加上增量 increment 。 |
| 7    | [HKEYS key](https://www.runoob.com/redis/hashes-hkeys.html)  获取所有哈希表中的字段 |
| 8    | [HLEN key](https://www.runoob.com/redis/hashes-hlen.html)  获取哈希表中字段的数量 |
| 9    | [HMGET key field1 [field2\]](https://www.runoob.com/redis/hashes-hmget.html)  获取所有给定字段的值 |
| 10   | [HMSET key field1 value1 [field2 value2 \]](https://www.runoob.com/redis/hashes-hmset.html)  同时将多个 field-value (域-值)对设置到哈希表 key 中。 |
| 11   | [HSET key field value](https://www.runoob.com/redis/hashes-hset.html)  将哈希表 key 中的字段 field 的值设为 value 。 |
| 12   | [HSETNX key field value](https://www.runoob.com/redis/hashes-hsetnx.html)  只有在字段 field 不存在时，设置哈希表字段的值。 |
| 13   | [HVALS key](https://www.runoob.com/redis/hashes-hvals.html)  获取哈希表中所有值。 |
| 14   | [HSCAN key cursor [MATCH pattern\] [COUNT count]](https://www.runoob.com/redis/hashes-hscan.html)  迭代哈希表中的键值对。 |



## 高级数据类型

### GEO[v3.2+]



Redis GEO 主要用于存储地理位置信息，并对存储的信息进行操作，该功能在 Redis 3.2 版本新增。

Redis GEO 操作方法有：

- geoadd：添加地理位置的坐标。
- geopos：获取地理位置的坐标。
- geodist：计算两个位置之间的距离。
- georadius：根据用户给定的经纬度坐标来获取指定范围内的地理位置集合。
- georadiusbymember：根据储存在位置集合里面的某个地点获取指定范围内的地理位置集合。
- geohash：返回一个或多个位置对象的 geohash 值。
- 

### HyperLogLog[v2.8.9+]

Redis 在 2.8.9 版本添加了 HyperLogLog 结构。

Redis HyperLogLog 是用来做基数统计的算法，HyperLogLog 的优点是，在输入元素的数量或者体积非常非常大时，计算基数所需的空间总是固定 的、并且是很小的。

在 Redis 里面，每个 HyperLogLog 键只需要花费 12 KB 内存，就可以计算接近 2^64 个不同元素的基 数。这和计算基数时，元素越多耗费内存就越多的集合形成鲜明对比。

但是，因为 HyperLogLog 只会根据输入元素来计算基数，而不会储存输入元素本身，所以 HyperLogLog 不能像集合那样，返回输入的各个元素。



下表列出了 redis HyperLogLog 的基本命令：

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | [PFADD key element [element ...\]](https://www.runoob.com/redis/hyperloglog-pfadd.html)  添加指定元素到 HyperLogLog 中。 |
| 2    | [PFCOUNT key [key ...\]](https://www.runoob.com/redis/hyperloglog-pfcount.html)  返回给定 HyperLogLog 的基数估算值。 |
| 3    | [PFMERGE destkey sourcekey [sourcekey ...\]](https://www.runoob.com/redis/hyperloglog-pfmerge.html)  将多个 HyperLogLog 合并为一个 HyperLogLog |



### Stream[v5.0+]

Redis Stream 是 Redis 5.0 版本新增加的数据结构。

Redis Stream 主要用于消息队列（MQ，Message Queue），Redis 本身是有一个 Redis 发布订阅 (pub/sub) 来实现消息队列的功能，但它有个缺点就是消息无法持久化，如果出现网络断开、Redis 宕机等，消息就会被丢弃。

简单来说发布订阅 (pub/sub) 可以分发消息，但无法记录历史消息。

而 Redis Stream 提供了消息的持久化和主备复制功能，可以让任何客户端访问任何时刻的数据，并且能记住每一个客户端的访问位置，还能保证消息不丢失。

Redis Stream 的结构如下所示，它有一个消息链表，将所有加入的消息都串起来，每个消息都有一个唯一的 ID 和对应的内容：

![img](../image/en-us_image_0167982791.png)

每个 Stream 都有唯一的名称，它就是 Redis 的 key，在我们首次使用 xadd 指令追加消息时自动创建。

上图解析：

- **Consumer Group** ：消费组，使用 XGROUP CREATE 命令创建，一个消费组有多个消费者(Consumer)。
- **last_delivered_id** ：游标，每个消费组会有个游标 last_delivered_id，任意一个消费者读取了消息都会使游标 last_delivered_id 往前移动。
- **pending_ids** ：消费者(Consumer)的状态变量，作用是维护消费者的未确认的 id。 pending_ids 记录了当前已经被客户端读取的消息，但是还没有 ack (Acknowledge character：确认字符）。

**消息队列相关命令：**

- **XADD** - 添加消息到末尾

- **XTRIM** - 对流进行修剪，限制长度

- **XDEL** - 删除消息

- **XLEN** - 获取流包含的元素数量，即消息长度

- **XRANGE** - 获取消息列表，会自动过滤已经删除的消息 

- **XREVRANGE** -  反向获取消息列表，ID 从大到小

- **XREAD** - 以阻塞或非阻塞方式获取消息列表

  **消费者组相关命令：**

- **XGROUP CREATE** - 创建消费者组

- **XREADGROUP GROUP** - 读取消费者组中的消息

- **XACK** - 将消息标记为"已处理"

- **XGROUP SETID** - 为消费者组设置新的最后递送消息ID

- **XGROUP DELCONSUMER** - 删除消费者

- **XGROUP DESTROY** - 删除消费者组

- **XPENDING** - 显示待处理消息的相关信息

- **XCLAIM** - 转移消息的归属权

- **XINFO** - 查看流和消费者组的相关信息；

- **XINFO GROUPS** - 打印消费者组的信息；

- **XINFO STREAM** - 打印流信息



### Bitmaps

对于可以使用0，1两种状态表示的数据

| 序号 | 命令及描述                                                   |
| ---- | ------------------------------------------------------------ |
| 1    | SETBIT key offset value<br/> 对 key 所储存的字符串值，设置或清除指定偏移量上的位(bit)。 |
| 2    | GETBIT key offset<br>对 key 所储存的字符串值，获取指定偏移量上的位(bit)。 |
| 3    | BITCOUNT key<br/>统计key下面的所有标记了为1的位数量          |





# 事务



# 发布订阅



# 持久化（AOF,RDB）

## RDB

RDB: redis database

redis.conf中默认配置为 dump.rdb

> 优点



> 缺点



## AOF

AOF：append of file

redis.conf中默认配置不开启

> 优点



> 缺点

