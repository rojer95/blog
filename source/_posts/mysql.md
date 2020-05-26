title: centos中mysql快速安装
tags:
  - Deploy
header-img: wallhalla-Bwxp3rLhQnl.jpg
categories: []
date: 2020-04-28 13:09:00
---

# 下载并安装 MySQL 官方的 Yum Repository

```sh
wget -i -c http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm
yum -y install mysql57-community-release-el7-10.noarch.rpm
```

# 安装 mysql

```sh
yum -y install mysql-community-server
```

# 启动 MySQL

```sh
systemctl start  mysqld.service
```

# 查看状态

```sh
systemctl status mysqld.service
```

# 查看密码

```sh
cat /var/log/mysqld.log | grep password
```

# 修改密码

```sql
ALTER USER 'root'@'localhost' IDENTIFIED BY 'new password';
```

# 配置 my.cnf

```sh
vi /etc/my.cnf
```

```
bind-address=127.0.0.1 # 限制本地登录
sql_mode=STRICT_TRANS_TABLES,NO_ZERO_IN_DATE,NO_ZERO_DATE,ERROR_FOR_DIVISION_BY_ZERO,NO_AUTO_CREATE_USER,NO_ENGINE_SUBSTITUTION

```

# 重启 mysql

```sh
systemctl restart mysqld
```

# 创建数据库

```sql
CREATE DATABASE  `database_name` DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
