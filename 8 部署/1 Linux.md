# Linux 命令

```bash
hostname  # 查看计算机名
sudo hostnamectl set-hostname <hostname>  # 重新设置计算机名
```

## 账户

```bash
adduser username  # 新建账户
userdel username  # 删除账户
usermod -l <newusername> <username>  # 更改用户名
passwd username  # 给账户设置密码
New password:  # 新密码
Retype new password:  # 再次输入
su username  # 切换账户
```

```bash
chown -R username:username /test  # 允许该用户操作这个文件
```

### 密码重置

```bash
ssu -  # 输入密码
sudo passwd root  # 重置密码
```

## 连接服务器

```bash
ssh root@IP  # cmd 远程连接服务器
ssh -p xx root@IP  # 指定端口
scp -r test/ root@ip:/test/   # 传输文件夹
exit  # 退出
```

## 路径操作

```bash
ls  # 查看文件目录
ll  # 查看文件夹详细信息
ll test.txt  # 查看指定文件详细信息
cd home  # 进入 home 文件夹下
cd ..  # 返回上级目录
cd ~ # 回到 root 目录
pwd  # 查看自己所在的文件目录地址
du -sh filename  # 查看文件大小
```

- root  # 用户目录
- home  # 其他用户目录
- bin  # 命令存放目录
- usr  # 软件存放目录
- etc  # 配置文件目录

## 文件增删

```bash
mkdir server  # 创建文件夹 server
rm -r server/*  # 删除 server 目录下所有文件
rm -rf server  # 删除文件夹
touch server.js  # 创建文件
mv index.html test.html  # 文件重命名
```

## 压缩
```bash
yum install -y unzip zip

zip -r file.zip file
unzip file.zip -d file
```

## yum

```bash
yum install nodejs  # 下载 nodejs
yum install git

yum remove nodejs -y  # 卸载
```

### 更新 node

```bash
npm cache clean -f  # 清除缓存
npm install -g n
vim ~/.bash_profile
	# 添加配置语句
	export N_PREFIX=/usr/local/node-v7.10.0-linux-x64  # node实际安装位置
	export PATH=$N_PREFIX/bin:$PATH
n latest
n stable  # 更新node
```

## 压缩

```bash
yum install lrzsz
rz  # 上传
sz test.zip  # 下载到远程操作计算机

yum install unrar
unzip test.zip  # 解压
```

## wget

```bash
wget 下载地址  # 下载
```

## 进程

```bash
ps -le  # 查看进程
kill pid  # 杀死进程 pid

netstat -nultp  # 查看端口
netstat -ntlp  # 查看开放端口
```

## 后台运行服务

```bash
nohup ./server &  # 后台运行一个服务
jobs  # 查看 nohub 启动的应用
kill %1  # 杀掉 nohub 应用1
```

```bash
npm install forever -g  # 安装 forever
forever start server.js  # 启动服务
forever stop server.js  # 停止服务

pm2 start --name 'myName' npm -- run start  # 运行 next 项目
```
