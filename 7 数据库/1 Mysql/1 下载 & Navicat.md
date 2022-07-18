# MySQL

MySQL 下载地址：[官方地址](https://dev.mysql.com/downloads/mysql/)、[腾讯云下载](https://pc.qq.com/detail/3/detail_1303.html)

## MySQL 命令

#### windows 编码设置

```sql
mysql -uroot -p  -- 管理员密码登录
show variables like 'character\_set\_%';  -- 显示编码
```

1. 文件 C:\ProgramData\MySQL\MySQL Server 8.0 下 my.ini 文件设置

```sql
default-character-set=utf8mb4  -- 默认编码
character-set-server=utf8mb4  -- 服务器编码
```

2. 复制 my.ini 文件放入安装目录
3. win 重新启动 mysql

```sql
net stop mysql80
net start mysql80
```

```sql
show databases;  -- 查看已有数据库
```

## Navicat 数据库管理工具

[ Navicat 下载 ](http://www.navicat.com.cn/download/navicat-for-mysql)

### 管理库

```sql
CREATE DATABASE test;  -- 创建数据库
DROP DATABASE test;  -- 删除数据库
show global variables like "%datadir%";  -- 数据库存放位置
show variables like 'port';  -- 查看连接端口
show variables like 'skip_networking';  -- 
select user,host from mysql.user;  -- 查看权限
use test;  -- 切换当前数据库
```

### 管理表

- bit ： 占 1 位，0 或 1，true 或 false
- int ： 占 32 位，整数
- decimal(m, n) ： 能精确计算的实数，m 是总的数字位数，n 是小数位数
- char(n) ： 固定长度位 n 的字符
- varchar(n) ： 长度可变，最大长度位 n 的字符
- text ： 大量的字符
- date ： 仅日期
- time ： 仅时间
- datetime ： 日期和时间

### 建表

```sql
CREATE TABLE `test`.`student`  (
    `name` varchar(10) NOT NULL,
    `birthday` date NOT NULL,
    `sex` bit(1) NOT NULL DEFAULT 0,
    `stuno` int NOT NULL AUTO_INCREMENT,
    `phone` varchar(11) NOT NULL,
    PRIMARY KEY (`stuno`)
);
```

### 删表

```sql
DROP TABLE `test`.student;
```
