---
title: centos中nginx快速安装
date: 2020-02-19 13:09:45
tags:
  - Deploy
header-img: wallhalla-Bwxp3rLhQnl.jpg
---

# 依赖安装

```sh
yum install -y gcc-c++
yum install -y pcre pcre-devel
yum install -y zlib zlib-devel
yum install -y openssl openssl-devel
```

# 下载 nginx

下载地址：https://nginx.org/en/download.html

```sh
wget -c https://nginx.org/download/nginx-1.16.1.tar.gz
tar zxvf nginx-1.16.1.tar.gz
```

# 配置编译

```sh
./configure --prefix=/usr/local/nginx --with-http_ssl_module
```

# 编译安装

```sh
make && make install
```

# 写入环境中

```sh
vi ~/.bashrc
```

添加以下内容

```
export PATH="/usr/local/nginx/sbin/:$PATH"
```

保存`:wq`

```sh
source ~/.bashrc
```

# 配置 nginx

```
vi /usr/local/nginx/conf/nginx.conf
```

在`http`中添加以下内容

```
include /usr/local/nginx/conf/conf.d/*.conf;
```

保存`:wq`
创建 conf 文件

```sh
mkdir -p /usr/local/nginx/conf/conf.d/
cd /usr/local/nginx/conf/conf.d/
vi index.conf
```

写入以下配置（根据情况自行修改）

```
server{
    listen 80;
    listen 443 ssl;
    server_name localhost;


    ssl_certificate /usr/local/nginx/conf/conf.d/ca/ca.crt;
    ssl_certificate_key /usr/local/nginx/conf/conf.d/ca/ca.key;

    location / {
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forward-For $proxy_add_x_forwarded_for;
        proxy_set_header Host $http_host;
        proxy_set_header X-Nginx-Proxy true;
        proxy_set_header X-Forwarded-Proto $scheme;
        proxy_pass http://127.0.0.1:7001;
        proxy_http_version 1.1;
        proxy_set_header Upgrade $http_upgrade;
        proxy_set_header Connection "upgrade";
    }
}

```

# 运行 nginx

```sh
nginx # 运行
nginx -s stop # 停止
nginx -s quit
nginx -s reload # 重新载入配置
```
