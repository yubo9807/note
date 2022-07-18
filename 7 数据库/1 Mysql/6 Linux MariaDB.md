# Linux MariaDB

1. 安装 ： `yum -y install mariadb mariadb-server`
2. 启动 ： `systemctl start mariadb`
3. 设置开机启动 ： `systemctl enable mariadb`
4. MariaDB 相关配置 ： `mysql_secure_installation`

```sql
Enter current password for root (enter for none): -- 初次运行直接回车

Set root password? [Y/n]  -- 是否设置root用户密码，回车

New password: 设置 root  -- 用户的密码

Re-enter new password:  -- 再次输入密码

Remove anonymous users? [Y/n]  -- 是否删除匿名用户，回车

Disallow root login remotely? [Y/n]  -- 是否禁止root远程登录,回车

Remove test database and access to it? [Y/n]  -- 是否删除 test 数据库，回车

Reload privilege tables now? [Y/n]  -- 是否重新加载权限表，回车
```

登录 ： `mysql -uroot -p`

```sql
create user username@localhost identified by 'password';  -- 创建用户

select user,host from mysql.user;  -- 查看用户

DROP USER 'username'@'localhost';  -- 删除用户

UPDATE mysql.user SET password = PASSWORD('newpassword') WHERE user = 'username';  -- 更改用户密码

show global variables like 'port';  -- 查看端口

show databases;  -- 查看已有数据库

grant all privileges on *.* to username@'%' identified by 'password' with grant option;  -- 授予权限并且可以授权

flush privileges;  -- 刷新权限
```

> 记得开放端口 3306 哦
