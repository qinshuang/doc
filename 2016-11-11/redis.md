## Redis 学习

# 安装和配置

* 安装

    sudo apt-get install redis-server

* 配置

    (暂无。。。)

# 适用场景


1.  Counting（计数）
2.  Reverse cache（反向cache）
3.  Top 10 list
4.  Last Index(登录信息)
...


# 数据类型

* String (字符串)

string是redis最基本的类型，你可以理解成与Memcached一模一样的类型，一个key对应一个value。
string类型是二进制安全的。意思是redis的string可以包含任何数据。比如jpg图片或者序列化的对象 。
string类型是Redis最基本的数据类型，一个键最大能存储512MB。

    set key value #设置值
    get key;#获取值
    
* Hash（哈希）

Redis hash 是一个键值对集合。
Redis hash是一个string类型的field和value的映射表，hash特别适合用于存储对象。
每个 hash 可以存储 232 -1 键值对（40多亿）

    HSET user:1 aged 2 #单个赋值
    HMSET user:1 username runoob password runoob points 200 # 多个赋值

* List（列表）

Redis 列表是简单的字符串列表，按照插入顺序排序。你可以添加一个元素到列表的头部（左边）。
列表最多可存储 232 - 1 元素 (4294967295, 每个列表可存储40多亿)。

    LPUSH key value # 添加元素到列表头部
    LRANGE key  start stop  #获取范围内的列表

* Set（集合）

Redis的Set是string类型的无序集合。
集合是通过哈希表实现的，所以添加，删除，查找的复杂度都是O(1)。
集合中最大的成员数为 232 - 1(4294967295, 每个集合可存储40多亿个成员)。

    sadd key value # 添加值到集合
    SMEMBERS key # 获取集合中的值
    

* zset(sorted set：有序集合)

Redis zset 和 set 一样也是string类型元素的集合,且不允许重复的成员。
不同的是每个元素都会关联一个double类型的分数。redis正是通过分数来为集合中的成员进行从小到大的排序。
zset的成员是唯一的,但分数(score)却可以重复。

    zadd key value # 添加值到集合
    ZRANGEBYSCORE runoob 0 1000 # 获取结合中的值


# 常用命令

* key 操作


    DEL key # 该命令用于在 key 存在时删除 key。
    EXISTS key #检查给定 key 是否存在。
    EXPIRE key seconds #为给定 key 设置过期时间。
    EXPIREAT key timestamp #EXPIREAT 的作用和 EXPIRE 类似，都用于为 key 设置过期时间。 不同在于 EXPIREAT 命令接受的时间参数是 UNIX 时间戳(unix timestamp)。
    PEXPIRE key milliseconds #设置 key 的过期时间以毫秒计。
    KEYS pattern #查找所有符合给定模式( pattern)的 key 。
    PERSIST key  #移除 key 的过期时间，key 将持久保持。
    PTTL key #以毫秒为单位返回 key 的剩余的过期时间。
    TTL key #以秒为单位，返回给定 key 的剩余生存时间(TTL, time to live)。
    RENAME key newkey  # 修改 key 的名称
    RENAMENX key newkey #仅当 newkey 不存在时，将 key 改名为 newkey 。
    TYPE key #返回 key 所储存的值的类型。
    
* String 类型操作


    SET key value #设置指定 key 的值
    GET key # 获取指定key 的值
    GETRANGE key start end #返回 key 中字符串值的子字符
    GETSET key value #将给定 key 的值设为 value ，并返回 key 的旧值(old value)。
    MGET key1 [key2..] #获取所有(一个或多个)给定 key 的值
    SETEX key seconds value #将值 value 关联到 key ，并将 key 的过期时间设为 seconds (以秒为单位)。
    SETNX key value #只有在 key 不存在时设置 key 的值。
    STRLEN key #返回 key 所储存的字符串值的长度。
    MSET key value [key value ...] #同时设置一个或多个 key-value 对。
    MSETNX key value [key value ...] #同时设置一个或多个 key-value 对，当且仅当所有给定 key 都不存在。
    INCR key #将 key 中储存的数字值增一。
    INCRBY key increment #将 key 所储存的值加上给定的增量值（increment） 。
    DECR key #将 key 中储存的数字值减一。
    DECRBY key decrement #key 所储存的值减去给定的减量值（decrement） 
    APPEND key value # 如果 key 已经存在并且是一个字符串， APPEND 命令将 value 追加到 key 原来的值的末尾。
    
    
