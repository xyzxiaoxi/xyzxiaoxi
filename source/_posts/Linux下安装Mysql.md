---
title: Linux(Centos)下安装Mysql
description: 安装Mysql教程
date: '2020-12-24'
keywords: 'linux,mysql,熙文说'
categories:
  - 安装教程
tags:
  - linux
  - mysql
abbrlink: f63cb2cd
---
# 前言
Mysql数据库的安装对于开发者来说必会的技能。刚好我要迁移测试环境的mysql，下面记录我安装msyql的过程。如有错误，欢迎指正!

# 安装前准备
1. 查检是否已经安装过Mysql,执行命令
```
rpm -qa | grep mysql
```
如果有安装就执行删除命令
```
rmp -e --nodeps mysql-xxx
```
我这台机器没有安装过，所以我执行命令显示
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608779331682-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087792958073.png)

2. 查询所有Mysql对应的文件夹
```
whereis mysql
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608779451066-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087794234716.png)
删除相关目录或文件
```
rm -rf /usr/lib64/mysql/ /usr/share/mysql/
```
再次验证是否删除完了
```
whereis mysql
find / -name mysql
```
3. 检查mysql用户组和用户是否存在
```
cat /etc/group | grep mysql
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608779763145-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087797444958.png)
```
cat /etc/passwd | grep mysql
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608779844620-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087798223453.png)
4. 添加用户组和用户
```
groupadd mysql
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608779966059-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087799411830.png)
```
useradd -r -g mysql mysql
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608780040179-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087800191799.png)
5. 安装wget
```
yum -y install wget
```
6. 下载Mysql安装包
```
wget https://dev.mysql.com/get/Downloads/MySQL-5.7/mysql-5.7.24-linux-glibc2.12-x86_64.tar.gz
```
7. 解压安装包
```
 tar -zxvf mysql mysql-5.7.24-linux-glibc2.12-x86_64.tar.gz
```
8. 重命名mysql文件
```
 mv mysql-5.7.24-linux-glibc2.12-x86_64 mysql
```
9. 在/usr/local/mysql目录下创建data目录
```
cd /usr/local/mysql
mkdir data

```
10. 更改mysql目录下所有的目录及文件夹所属的用户组和用户，以及权限
```
chown -R mysql:mysql /usr/local/mysql
chmod -R 755 /usr/local/mysql
```
# 安装Mysql
1. 编译安装并初始化mysql
```
cd /usr/local/mysql/bin
```
执行命令
```
./mysqld --initialize --user=mysql --datadir=/usr/local/mysql/data --basedir=/usr/local/mysql
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608782085588-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087820655039.png)

记录日志最末尾位置root@localhost:后的字符串，此字符串为mysql管理员临时登录密码。
2. 编辑my.cnf文件
```
vi /etc/my.cnf
```
添加以下配置
```
[mysqld]
basedir=/usr/local/mysql
datadir=/usr/local/mysql/data
socket=/tmp/mysql.sock
# Disabling symbolic-links is recommended to prevent assorted security risks
symbolic-links=0
max_connections=500
# Settings user and group are ignored when systemd is used.
# If you need to run mysqld under a different user or group,
# customize your systemd unit file for mariadb according to the
# instructions in http://fedoraproject.org/wiki/Systemd

[mysqld_safe]
log-error=/usr/local/mysql/data/mariadb.log
pid-file=/usr/local/mysql/data/mariadb.pid

#
# include all files from the config directory
#
!includedir /etc/my.cnf.d
character_set_server=utf8mb4_unicode_ci
```
按下ESC键，运行wq保存退出
```
wq
```
3. 测试启动mysql服务器
```
/usr/local/mysql/support-files/mysql.server start
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608782980149-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087829602630.png)
4. 添加软连接并停止Mysql服务
```
ln -s /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql
service mysql stop
ln -s /usr/local/mysql/bin/mysql /usr/bin/mysql

```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608784823168-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087848024879.png)
5. 登录mysql，修改密码
```
service mysql start
mysql -uroot -p
```
密码是安装mysql第1步中生成的密码
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608786849829-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087868319401.png)
修改密码
```
set password for root@localhost = password('yourpass');
```
5. 开放远程连接
```
show databses;
use mysql;
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'yourpass' WITH GRANT OPTION;
flush privileges;
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608787288813-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087872693106.png)
6. 用客户端连接mysql试一下，如果遇到mysql的10060错误。需要检查下防火墙是不是开放了3306端口
```
firewall-cmd --zone=public --list-ports  //查看所有打开的端口
firewall-cmd --zone=public --add-port=3306/tcp --permanent firewall开启3306端口
firewall-cmd --reload
```
7. 设置开机自动启动
```
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysqld
chmod +x /etc/init.d/mysqld
chkconfig --add mysqld
chkconfig --list
```
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2020-12-24/1608789119771-%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16087890975768.png)

至此，Mysql已经安装成功了！

# 欢迎关注作者公众号
![](https://gitee.com/xyzxiaoxi/picture/raw/master/2021-1-7/1610018774805-qrcode_for_gh_c467e04f3857_258.jpg)