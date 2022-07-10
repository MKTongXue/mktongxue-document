# 1 包含课程章节

* 《【号外011】.分布式事务seata-tcc模式简介_TienChin》
* 《【号外012】.分布式事务seata-tcc模式实战-1_TienChin》
* 《【号外013】.分布式事务seata-tcc模式实战-2_TienChin》
* 《【号外014】.分布式事务seata-tcc模式实战-3_TienChin》
* 《【号外015】.分布式事务seata-tcc模式实战-4_TienChin》
* 《【号外016】.分布式事务seata-tcc总结_TienChin》


# 2 分布式事务 Seata TCC 模式

## 2.1 Seata Tcc 模式简介

（1）Try Confirm Cancel（TCC），也是基于两阶段提交发展出来的分布式事务处理方案
```text
Seata TCC 模式
https://seata.io/zh-cn/docs/dev/mode/tcc-mode.html
```

## 2.2 案例

（1）如果未成功识别子项目，打开对应 `pom.xml` 文件，右键选择 `Add as Maven Project` 项

![IDEA 未识别项目](http://image.mktongxue.com/202207/002-01.png)

![添加进 Maven Project](http://image.mktongxue.com/202207/002-02.png)

（2）启动 `Seata-Server` 服务
```text
启动项目，（以管理员身份）进入目录，执行 seata-server.sh

查看服务进程命令 jps
关闭 seata-server 服务命令 taskkill /F /pid 1852（进程Id）

访问 http://localhost:7091/#/login
```

（3）测试请求
```text
http://127.0.0.1:1112/order?account=MK01&productId=001&count=5
```

# 3 结束
