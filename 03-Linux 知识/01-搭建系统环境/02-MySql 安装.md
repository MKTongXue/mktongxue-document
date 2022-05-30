# 1 Linux 安装 MySql

## 1.1 下载

[MySql 官网](https://dev.mysql.com)
[MySql 5.7 下载地址](https://downloads.mysql.com/archives/community)

## 1.2 安装

（1）
```java
// 解压
// 新建文件夹 mkdir mktongxue
// 进入 mktongxue 文件夹，我一般是在 /usr/mktongxue
cd /
cd /usr/mktongxue

// 将 mysql 安装包上传到服务器
// mysql-5.7.36-linux-glibc2.12-x86_64.tar.gz
// 解压
tar -xvf mysql-5.7.36-linux-glibc2.12-x86_64.tar.gz

// 移动并重新命名
mv mysql-5.7.36-linux-glibc2.12-x86_64 /usr/local/mysql

// 创建 mysql 用户组和用户并修改权限
cd /usr/local/mysql

groupadd mysql
useradd -r -g mysql mysql
// 创建数据目录，并赋予权限
mkdir -p  /data/mysql
chown mysql:mysql -R /data/mysql

// 配置 my.cnf
vim /etc/my.cnf
```


（2）my.cnf 配置文件内容
```text
i 插入
ESC 键 + :wq 保存并退出
```

```text
[mysqld]
bind-address=0.0.0.0
port=3306
user=mysql
basedir=/usr/local/mysql
datadir=/data/mysql
socket=/tmp/mysql.sock

# safe
log-error=/data/mysql/mysql.err
pid-file=/data/mysql/mysql.pid

# character config
character_set_server=utf8mb4
symbolic-links=0
explicit_defaults_for_timestamp=true 
lower_case_table_names=1
```

（3）
```java
// 初始化数据库
cd /usr/local/mysql/bin/
./mysqld --defaults-file=/etc/my.cnf --basedir=/usr/local/mysql/ --datadir=/data/mysql/ --user=mysql --initialize

// 如果报错，缺少 libaio，那么就安装它
yum install -y libaio

// 查看密码
cat /data/mysql/mysql.err
// 密码 rpNs)3j<*SX>

// 启动 mysql
// 将 mysql.server 放置到 /etc/init.d/mysql 中
cp /usr/local/mysql/support-files/mysql.server /etc/init.d/mysql
// 启动服务
service mysql start
// 查看服务
ps -ef|grep mysql
// 关闭服务
// service mysql stop

// 登录
./mysql -u root -p
// 输入密码 rpNs)3j<*SX>

// 更改密码
SET PASSWORD = PASSWORD('123456');
ALTER USER 'root'@'localhost' PASSWORD EXPIRE NEVER;
FLUSH PRIVILEGES;

// 如果想使用 navicat 连接，还需要使用执行以下命令
use mysql      
update user set host = '%' where user = 'root';
FLUSH PRIVILEGES;

// 退出 mysql
exit;
```

（4）查看密码

![查看密码](http://image.mktongxue.com/202205/015.png)

（5）远程连接 mysql 数据库

![开放云服务器防火墙 3306 端口](http://image.mktongxue.com/202205/016.png)

![使用 Navicat 远程连接](http://image.mktongxue.com/202205/017.png)

## 1.3 参考文档

（1）[linux笔记：极简方式安装mysql，建议收藏](https://juejin.cn/post/6999798922759634951)


# 2 结束
