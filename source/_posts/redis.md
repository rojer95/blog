---
title: centos中redis快速安装
date: 2020-04-28 13:09:45
tags:
  - Deploy
header-img: wallhalla-Bwxp3rLhQnl.jpg
---

# 下载 nvm

```sh
wget http://download.redis.io/releases/redis-5.0.8.tar.gz
```

# 解压

```sh
tar -zxvf redis-5.0.8.tar.gz
```

# 安装 gcc

```sh
yum install -y gcc
```

# 编译安装

```sh
cd redis-5.0.8
make MALLOC=libc
mv redis-5.0.8 /usr/local/redis
cd /usr/local/redis/src
make install
```

# 配置环境

```
vi ~/.bashrc
export PATH="/usr/local/redis/src/:$PATH"
source ~/.bashrc
```

# 配置 redis

```
daemonize yes
requirepass ****
```
