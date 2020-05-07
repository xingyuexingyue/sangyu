Redis 是一个开源（BSD许可）的，内存中的数据结构存储系统，它可以用作数据库、缓存和消息中间件

它通常被称为数据结构服务器，因为 value 可以是 String，Hash，list，sets，sorted sets

## 一 Redis 数据类型

#### 1.1 String 

string 类型是二进制安全的，意味着 redis 的 string 可以包含任何数据，比如 jpg 图片或者序列化的对象

string 类型的 value 最大能存储512MB

#### 1.2 Hash

Redis Hash 是一个 string 类型的 field 和 value 的映射表，适合存储对象

#### 1.3 List

Redis 列表按照插入顺序排序，可以添加一个元素到列表的头部或者尾部

#### 1.4 set

Redis 是无序集合，并且集合内的元素具有唯一性。集合是通过哈希表实现的

#### 1.5 zset 

zset 和 set 类似，不同的是 zset 每个元素都关联一个 double 类型的分数，通过这个分数为集合中的成员进行从小到大的排序，分数是可以重复的

## 二 连接 Redis 服务

#### 2.1 连接本地的 redis 服务

第一步：启动本地的 redis 服务

```
/usr/local/bin/redis-server /usr/local/etc/redis.conf
```

第二步：连接本地的 redis 服务

```
redis-cli
```

#### 2.2 连接远程的 redis 服务

```
redis-cli -h host -p port -a password
```

## 三 key 命令


3.1 删除指定的 key

```
DEL key
```
3.2 检查 key 是否存在

```
exists key
```

3.3 给 key 设置过期时间，单位秒

```
expire key seconds
```

3.4 以秒为单位，返回给定 key 的剩余生存时间

```
TTL key
```

3.5 返回 key 所储存的值的类型

```
TYPE key
```

3.5 修改 key 的名称

```
rename key newkey
```

## 四 String 命令

用于管理 redis 字符串值

4.1 设置指定 key 的值

```
set key value
```

4.2 获得指定 key 的值

```
get key
```

4.3 返回 key 中字符串值的区间，从0开始

```
getrange key start end
```

4.4 给指定的 key 设置字符串，并返回旧值，如果没有旧值不返回

```
getset key value
```

4.5 获取1个/多个 key 的值

```
mget key[...] 
```
4.6 将值 value 关联到 key，并设置 key 的过期时间，以秒为单位

```
setex key seconds value
```

4.7 只有 在 key 不存在时设置 value

```
setnx key value
```

4.8 返回 key 所储存的字符串值的长度

```
strlen key
```

4.9 同时设置1个/多个 key-value

```
mset key value[...]
```

4.10 同时设置1个/多个 key-value，仅当 key 都不存在时

```
msetnx key value[...]
```

4.11 数字值 value + 1

```
incr key
```

4.12 数字值 value + 指定值

```
incrby key increment
```

4.13 数字值 value - 1

```
decr key
```

4.14 数字值 value - 指定值

```
decrby key increment
```

4.15 字符串值追加 value

```
append key value
```

## 五 Hash 命令

5.1 删除1个/多个哈希表字段

```
hdel key field[...]
```

5.2 检查字段是否存在

```
hexists key field
```

5.3 获得指定字段的值

```
hget key field
```

5.4 获取 key 所有字段和值

```
hgetall key
```

5.5 给字段 value + 指定的值

```
hincrby key field increment
```

5.6 获取所有 key

```
hkeys key
```

5.7 获取 key 的数量

```
hlen key
```

5.8 获得1个/多个字段的值

```
hmget key field1[...]
```

5.9 设置 key filed value

```
hset key filed value
```

5.10 设置 key 多个 field value

```
hmset key field value[...]
```

5.11 字段 field 不存在时，设置 value

```
hsetnx key field value
```

## 六 List 命令


6.1 通过索引获得元素

```
lindex key index
```

6.2 获得长度

```
llen key
```

6.3 移除并获取第一个元素

```
lpop key
```

6.4 插入1个/多个值到头部

```
lpush key value[...]
```


6.5 插入到已存在列表的头部

```
lpushx key value
```

6.6 获得指定范围内的元素

```
lrange key start stop
```

6.7 按照 count 的值，

大于0 从表尾开始搜索，移除等于 value 的值，数量为 COUNT
小于0 从表头开始搜索，移除等于 value 的值，数量为 COUNT 
等于0 移除表中所有与 value 相等的值

```
lrem key count value
```

6.8 通过索引设置 value

```
lset key index value
```

6.9  移除最后一个元素并返回

```
rpop key
```

## 七 set

7.1 set 添加1个/多个成员

```
sadd key member1[...]
```

7.2 获取集合的成员数

```
scard key
```

7.3 返回差集

```
sdiff key[key2]
```

7.4 返回交集

```
sinter key1[key2]
```

7.5 判断元素是否在集合 key 中

```
sismember key member
```

7.6 返回集合中的成员

```
smembers key
```

7.7 返回并集

```
sunion key1[key2]
```

## 八 sorted set

8.1 添加或更新1个/多个成员

```
zadd key score1 member1
```

8.2 获取有序集合的成员数

```
zcard key
```

## 九 Java 使用 redis















