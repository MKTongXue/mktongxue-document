# 1 Linux 系统如何运行 Jar 包

## 1.1 在 Linux 后台运行 Jar 包

（1）运行
```java
// 在 linux 后台运行 jar 包，并把日志输出到 mktongxue-portal.log 文件
nohup java -jar mktongxue-portal.jar > mktongxue-portal.log 2>&1 &
```

（2）关闭
```java
// 关闭 linux 后台运行的 jar 包

// 查询出进程号 pid
// 根据 jar 所占用端口
netstat -nlp | grep :8003

// 根据 java 程序查找
ps -ef | grep java

// 根据 jar 包查询进程号
ps aux | grep mktongxue-portal.jar

// 根据进程号 pid，结束进程
kill -9 5509
```


## 1.2 参考文档

（1）暂无


# 2 结束
