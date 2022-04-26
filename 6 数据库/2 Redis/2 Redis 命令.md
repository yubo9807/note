# redis 命令

## 基本命令

```bash
keys <pattern>  # 得到满足条件的所有 key

exists <keys...>  # 确认指定的多个 key 有几个是存在的

type <key>  # 得到 key 的类型

dbsize  # 得到 key 的数量

ttl <key>  # 得到一个 key 的过期时间，-1 永不过期，-2 不存在

expire <key> <seconds>  # 重新设置一个 key 的过期时间，单位 s

rename <oldkey> <newkey>  # 重命名一个 key

del <key>  # 删除 key

flushdb  # 删除当前数据库

flushall  # 删除所有数据库
```

## 字符串

```bash
set <key> <value> [<TTL>]  # 设置键值对，TTL 为过期时间，单位 s，默认为 -1（不过期）

get <key>  # 获取某个 key 的值

mget <key...>  # 获取多个 key 的值

incr <key>  # 将某个 key 的值自增 1，前提该 key 的值必须输数字

incrby <key> <number>  # 将某个键的值自增指定的数量

decr <key>  # 将某个 key 的值自减 1

decrby <key> <number>  # 将某个键的值自减指定的数量
```

## List 链表数组

```bash
rpush <key> <value>  # 向指定的 key 对应的链表尾部加入一个值

lpush <key> <value>  # 向指定的 key 对应的链表头部加入一个值

llen <key>  # 得到链表的长度

lrange <key> <start> <end>  # 得到链表指定范围的值

lindex <key> <index>  # 返回链表 key 中下标为 index 的值

lset <key> <index> <value>  # 设置链表 key 下标为index 的值

lrem <key> <count> <value>  # 删除链表 key 中值为 value 的项，删除 count 个

lpop <key>  # 删除链表的首元素

rpop <key>  # 删除链表的尾元素
```

## hash 链表对象

```bash
hset <key> <field> <value>  # 设置对象 key 的属性

hget <key> <field>  # 返回对象 key 的 field 属性值

hkeys <key>  # 返回对象 key 中所有的键

hvals <key>  # 返回对象 key 中所有的字段值

hgetall <key>  # 返回对象 key 中所有的键值对

hexists <key> <field>  # 对象 key 中是否存在指定的字段

hdel <key> <field>  # 删除对象 key 中的指定字段

hlen <key>  # 返回对象 key 中的字段数量
```
