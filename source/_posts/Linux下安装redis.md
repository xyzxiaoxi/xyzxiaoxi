---
title: Linux(Centos)下安装redis
description: 安装redis教程
keywords: 'linux,redis,熙文说'
categories:
  - 安装教程
tags:
  - linux
  - redis
abbrlink: d9f855e4
---
# 安装

1. 下载安装包

```
wget https://download.redis.io/releases/redis-6.0.9.tar.gz
```

2. 解压安装包

```
tar -zxvf redis-6.0.9.tar.gz
```

3. 重命名

```
mv redis-6.0.9 redis
```

4. 安装 make 所需要的包

```
 yum -y install gcc automake autoconf libtool make
```

5. 编译安装 redis

```
make
```

如果出现了“Error jemalloc/jemalloc.h: No such file or directory” 。运行

```
make MALLOC=libc
```

如果出现了“error: ‘struct redisServer’ has no member named ‘maxmemory’”

```
yum -y install centos-release-scl
yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils
scl enable devtoolset-9 bash
```

然后再运行‘make’命令

6. 配置 redis 服务

```
cp /usr/local/redis/utils/redis_init_script /etc/init.d/redis
```

7. 将 redis-server redis-cli 拷到/user/local/bin

```
cp /usr/local/redis/src/redis-server /usr/local/redis/src/redis-cli /usr/local/bin/
```

8. 复制 redis 的配置文件到/etc/redis/目录下

```
mkdir /etc/redis
cp /usr/local/redis/redis.conf /etc/redis/6379.conf
```

编辑 6379.conf 文件
将 daemonize 的值改为 yes
将 requirepass 注释放开
将 bind 改为机器的 ip 地址

9. 启动 redis

```
service redis start
```

10. 测试 redis

```
redis-cli -a  foobared
select 1
```

![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608800750214-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16088007214004.png)

11. 打开 6379 端口让远程也可以访问

```
firewall-cmd --zone=public --add-port=6379/tcp --permanent
firewall-cmd --reload
```

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)