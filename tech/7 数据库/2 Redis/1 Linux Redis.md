# Linux 下安装 redis

1. 安装 gcc ： `yum install gcc-c++`
2. 下载 redis

```bash
cd /usr/local  # 安装目录

wget https://download.redis.io/releases/redis-6.0.9.tar.gz

tar xzf redis-6.0.9.tar.gz

cd redis-6.0.9

make  # 编译
```

> 这里遇到一个问题：在安装 6.0 版本 make 时会遇到这样一个错误：server.c:xxxx:xx: error: ‘xxxxxxxx’ has no member named ‘xxxxx’，原因：gcc编译工具版本的问题，centos7 默认安装的版本是 4.8.5，但是要求对应版本要在 5.3 以上

```bash
gcc -v  # 查看 gcc 版本命令

yum -y install centos-release-scl

yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils

scl enable devtoolset-9 bash

echo "source /opt/rh/devtoolset-9/enable" >>/etc/profile  # 使永久生效

make
```

3. 配置文件：

```bash
vim /usr/local/redis-6.0.9/redis.conf

maxmemory 10mb  # 最大内存限制
bind 0.0.0.0  # 设置远程连接，默认是 127.0.0.1（记得开放端口号 6379）
```

4. 启动

```bash
./src/redis-server redis.conf &  # 运行服务

./src/redis-cli  # 运行客户端
./src/redis-cli shutdown  # 结束运行

quit  # 退出 redis
```
