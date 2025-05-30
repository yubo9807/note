# docker

## 安装
```bash
# 安装必要的软件包
yum install -y yum-utils device-mapper-persistent-data lvm2

# 添加 Docker 存储库
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo

# 更新软件包列表并安装 Docker
yum update -y
yum install -y docker-ce docker-ce-cli containerd.io

# 修改镜像源地址
vi /etc/docker/daemon.json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}

# 启动Docker服务并设置开机启动
systemctl start docker
systemctl enable docker
```

```bash
docker pull nginx  # 拉取一个镜像

docker run --name nginx -p 80:80 -d nginx  # 创建并运行一个容器

docker ps  # 查看所有容器

docker images  # 查看所有镜像

docker push  # 推送一个镜像

docker rm nginx  # 删除容器

docker rmi id  # 删除镜像

docker logs nginx  # 查看容器日志  -f 实时查看

docker inspect nginx  # 查看容器配置信息

docker build

docker save

docker load

docker exec
```

## 数据卷挂载

```bash
docker volume ls
```
