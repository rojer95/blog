title: centos中nvm快速安装
tags:
  - Deploy
header-img: wallhalla-Bwxp3rLhQnl.jpg
date: 2020-04-28 13:09:45
---

# 下载 nvm

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

# 生效环境

```sh
source ~/.bashrc
```

# 查看版本

```sh
nvm ls-remote
```

# 安装 node

```sh
nvm install 13.13.0
```

# 安装 yarn

```sh
npm install -g yarn
```

# yarn 镜像

## 查询当前镜像

```sh
yarn config get registry
```

## 设置为淘宝镜像

```sh
yarn config set registry https://registry.npm.taobao.org/
```

## 设置为官方镜像

```sh
yarn config set registry https://registry.yarnpkg.com
```
