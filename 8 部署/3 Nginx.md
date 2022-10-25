# Nginx

## yum 安装

```bash
yum -y install nginx   # 安装 nginx
yum remove nginx  # 卸载 nginx
```

> 使用 yum 进行 Nginx 安装时，Nginx 配置文件在 /etc/nginx 目录下

### 配置 Nginx 服务

```bash
systemctl enable nginx  # 设置开机启动 
service nginx start  # 启动 nginx 服务
service nginx stop  # 停止 nginx 服务
service nginx restart  # 重启 nginx 服务
nginx -t -q  # 配置校验
service nginx reload  # 重新加载配置，一般是在修改过 nginx 配置文件时使用。
```

### 依赖库安装

```bash
yum -y install gcc gcc-c++ # nginx 编译时依赖 gcc 环境

yum -y install pcre pcre-devel # 让 nginx 支持重写功能

yum -y install zlib zlib-devel # zlib 库提供了很多压缩和解压缩的方式，nginx 使用 zlib 对 http 包内容进行 gzip 压缩

yum -y install openssl openssl-devel  # 安全套接字层密码库，用于通信加密
```

## 源码包安装 Nginx

```bash
cd /usr/local/nginx

wget https://nginx.org/download/nginx-1.18.0.tar.gz

tar -zxvf  nginx-1.18.0.tar.gz # 解压缩

cd nginx-1.18.0

./configure --prefix=/usr/local/nginx # 检查平台安装环境
# --prefix=/usr/local/nginx  是 nginx 编译安装的目录（推荐），安装完后会在此目录下生成相关文件

make # 编译
make install # 安装
```

### 启动服务

```bash
/usr/local/nginx/sbin/nginx  # 启动服务

/usr/local/nginx/sbin/nginx -s reload  # 重新加载服务

/usr/local/nginx/sbin/nginx -s stop # 停止服务

ps -ef | grep nginx # 查看服务进程
```

### 端口映射

```bash
vim /etc/nginx/nginx.conf
```

### nginx.conf

```bash
http {
    sendfile            on;  # 开启高效传输模式
    tcp_nopush          on;  # 减少网络报文段的数量
    tcp_nodelay         on;
    keepalive_timeout   65;  # 保持连接的时间，也叫超时时间，单位秒
    types_hash_max_size 2048;

    include             /etc/nginx/mime.types;  # 文件扩展名与类型映射表
    default_type        application/octet-stream;  # 默认文件类型

    include             /etc/nginx/conf.d/*.conf;  # 加载子配置项
    
    upstream myserver {
  	    # ip_hash;  # ip_hash 方式
        # fair;   # fair 方式
        server 127.0.0.1:8081;  # 负载均衡目的服务地址
        server 127.0.0.1:8080;
        server 127.0.0.1:8082 weight=10;  # weight 方式，不写默认为 1
    }
    
    gzip on;  # 默认off，是否开启gzip
    gzip_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;  # 进行压缩的文件类型
    gzip_min_length 1k;  # gizp压缩起点，文件大于1k才进行压缩
    gzip_buffers 4 16k;  # 设置压缩所需要的缓冲区大小，以4k为单位，如果文件为7k则申请2*4k的缓冲区 
    gzip_static on;  # nginx对于静态文件的处理模块，开启后会寻找以.gz结尾的文件，直接返回，不会占用cpu进行压缩，如果找不到则不进行压缩
    gzip_http_version 1.1;  # 识别http协议的版本，早期浏览器可能不支持gzip自解压，用户会看到乱码
    gzip_comp_level 1;  # gzip 压缩级别，1-9，数字越大压缩的越好，也越占用CPU时间
    gzip_vary on;  # 启用应答头"Vary: Accept-Encoding"
    gzip_proxied expired no-cache no-store private auth;
    # nginx做为反向代理时启用,off(关闭所有代理结果的数据的压缩),
    # expired(启用压缩,如果header头中包括"Expires"头信息),
    # no-cache(启用压缩,header头中包含"Cache-Control:no-cache"),
    # no-store(启用压缩,header头中包含"Cache-Control:no-store"),
    # private(启用压缩,header头中包含"Cache-Control:private"),
    # no_last_modefied(启用压缩,header头中不包含"Last-Modified"),
    # no_etag(启用压缩,如果header头中不包含"Etag"头信息),
    # auth(启用压缩,如果header头中包含"Authorization"头信息)
    
    brotli on;  # 是否启用在on-the-fly方式压缩文件，启用后，将会在响应时对文件进行压缩并返回（仅支持https）
    brotli_static always;  # 检查是否存在带有br扩展的预先压缩过的文件。always总是使用压缩过的文件，不判断浏览器是否支持
    brotli_comp_level 6;  # 设置压缩质量等级。取值范围是0到11
    brotli_buffers 16 8k;  # 设置缓冲的数量和大小。大小默认为一个内存页的大小，也就是4k或者8k
    brotli_min_length 20;  # 设置需要进行压缩的最小响应大小
    brotli_types text/plain text/css application/json application/x-javascript text/xml application/xml application/xml+rss text/javascript;  # 指定对哪些内容编码类型进行压缩。text/html内容总是会被进行压缩

    server {
        listen       80;  # 配置监听的端口
        server_name  _;  # 配置的域名
        
        add_header 'Access-Control-Allow-Origin' $http_origin;   # 全局变量获得当前请求origin，带cookie的请求不支持*
        add_header 'Access-Control-Allow-Credentials' 'true';    # 为 true 可带上 cookie
        add_header 'Access-Control-Allow-Methods' 'GET, POST, OPTIONS';  # 允许请求方法
        add_header 'Access-Control-Allow-Headers' $http_access_control_request_headers;  # 允许请求的 header，可以为 *
        add_header 'Access-Control-Expose-Headers' 'Content-Length,Content-Range';
        add_header 'Access-Control-Max-Age' 1728000;   # OPTIONS 请求的有效期，在有效期内不用发出另一条预检请求
        add_header 'Content-Type' 'text/plain; charset=utf-8';
        add_header 'Content-Length' 0;
        add_header X-Frame-Options DENY;           # 减少点击劫持
        add_header X-Content-Type-Options nosniff; # 禁止服务器自动解析资源类型
        add_header X-Xss-Protection 1;             # 防 XSS 攻击

        location / {
            root         /usr/share/nginx/html;    # 跟路径
            index        index.html index.htm;     # 默认首页文件
            try_files    $uri $uri/ /404.html;     # 没有匹配到 uri 时，把它当成一个目录，还没有的话找 404.html
            
            allow        192.168.0.2； # 允许访问的ip地址
            deny         all;  # 禁止访问的ip地址
            
            proxy_pass   http://localhost:3000;  # 代理地址
        }
        
        # 图片防盗链
        location ~* \.(gif|jpg|jpeg|png|bmp|swf)$ {
            # 只允许本机 IP 外链引用，将百度和谷歌也加入白名单
            valid_referers none blocked server_names ~\.google\. ~\.baidu\. *.qq.com;
            if ($invalid_referer){
                return 403;
            }
        }
        
        # 图片缓存时间设置
        location ~ .*\.(css|js|jpg|png|gif|swf|woff|woff2|eot|svg|ttf|otf|mp3|m4a|aac|txt)$ {
            expires 10d;  # 为 -1 时不缓存
        }

        error_page 404 /404.html;  # 默认404对应的访问页面

        error_page 500 502 503 504 /50x.html;  # 默认50x对应的访问页面
        location = /50x.html {}

        return 301 http://hpyyb.cn$request_uri;  # 重定向
    }
    
    # https
    server {
        listen 443 ssl http2 default_server;   # SSL 访问端口号为 443
        server_name sherlocked93.club;         # 填写绑定证书的域名

        ssl_certificate /etc/nginx/https/1_sherlocked93.club_bundle.crt;   # 证书文件地址
        ssl_certificate_key /etc/nginx/https/2_sherlocked93.club.key;      # 私钥文件地址
        ssl_session_timeout 10m;

        ssl_protocols TLSv1 TLSv1.1 TLSv1.2;      #请按照以下协议配置
        ssl_ciphers ECDHE-RSA-AES128-GCM-SHA256:HIGH:!aNULL:!MD5:!RC4:!DHE; 
        ssl_prefer_server_ciphers on;
  
        location / {
            root         /usr/share/nginx/html;
            index        index.html index.htm;
        }

    }

}
```

### 正则匹配

1. `=` 精确匹配路径，用于不含正则表达式的 url 前，如果匹配成功，不再进行后续的查找；
2. `^~` 用于不含正则表达式的 url； 前，表示如果该符号后面的字符是最佳匹配，采用该规则，不再进行后续的查找；
3. `~` 表示用该符号后面的正则去匹配路径，区分大小写；
4. `~*` 表示用该符号后面的正则去匹配路径，不区分大小写。跟 `~` 优先级都比较低，如有多个location的正则能匹配的话，则使用正则表达式最长的那个；

> 如果 url 包含正则表达式，则必须要有 `~` 或 `~*` 标志。

