# 1 包含课程章节

* 《【号外017】.分布式事务seata-xa简介_TienChin》
* 《【号外018】.MySQL中的XA事务实践_TienChin》
* 《【号外019】.分布式事务seata-xa模式实战-1_TienChin》
* 《【号外020】.分布式事务seata-xa模式实战-2_TienChin》


# 2 分布式事务 Seata-XA 模式

## 2.1 Seata-XA 模式简介

（1）XA 模式是 X/Open 组织定义的分布式事务处理标准。

XA 规范描述了全局的事务管理器与局部的资源管理器之间的接口，利用 XA 规范可以实现多个资源，例如数据库、MQ 等，在同一个事务中进行访问，这样就可以使得数据库的 ACID 属性在跨应用程序的时候依然有效。

目前所有主流的数据库基本上都支持 XA 协议，包括 MySQL 数据库。

（2）MySQL 中的 XA 事务分为两种
* 内部 XA 事务，内部 XA 可以用作同一个 MySQL 实例下，跨多引擎的事务，这种一般使用 binlog 作为协调者。
* 外部 XA 事务，外部 XA 可以参与到外部的分布式事务中，这种一般需要应用层介入作为协调者。

（3）MySQL 中 XA 事务实践
```sql
-- 开启 XA 事务
xa start "transaction_mktongxue";
-- 更新语句
update `account_tbl` set money = money-20 where id = 1;
-- 结束事务
xa end "transaction_mktongxue";
-- 事务准备
xa prepare "transaction_mktongxue";
-- 事务提交
xa commit "transaction_mktongxue";
-- 到此，数据库内容更新成功！
```

```sql
-- 可以不执行 xa prepare 事务准备
-- 直接执行提交，需要 one phase 修饰
xa commit "transaction_mktongxue" one phase;
```

```sql
-- 事务回滚
xa rollback "transaction_mktongxue";
-- 查询事务状态
xa recover;
-- 事务回滚，事务名称，减去 gtrid_length 剩余长度，format_ID 值
xa rollback "transaction_mktongxue", "", 1;
```

![xa recover 查询结果](http://image.mktongxue.com/202207/005.png)

（4）
![Seata-XA 示意图](http://image.mktongxue.com/202207/003.png)

* 首先 `TM` 开启全局的分布式事务。
* 不同的微服务开始执行，各个微服务（RM）依次执行 `xa start -> SQL -> xa end -> xa prepare` 这是一阶段的操作。
* 在一阶段的操作中，`xa prepare` 会将当前分支事务的状态报告给 `TC`
* `TC` 判断一下，各个分支事务都执行成功了，此时就通知各个分支事务提交；如果分支事务中有人执行失败，那么此时就通知各个分支事务一起回滚。


## 2.2 Seata-XA 演示项目

（1）`seata-xa` 项目名称
```text
<!-- 数据库驱动 -->
<dependency>
    <groupId>mysql</groupId>
    <artifactId>mysql-connector-java</artifactId>
    <scope>runtime</scope>
    <!--
        数据库驱动版本必须是 8.0.11
        默认 8.0.22 可能会报错！！！
    -->
    <version>8.0.11</version>
</dependency>

# 关闭数据源代理
seata.enable-auto-data-source-proxy=false

// 不要引入 com.alibaba.druid 数据库驱动，seata 自己依赖内有，可能冲突！
```

```text
// 配置数据源
package com.mktongxue.account.config;
DataSourceConfig 类

// 启动类上，不使用自动配置数据源
@SpringBootApplication(scanBasePackages = "com.mktongxue", exclude = DataSourceAutoConfiguration.class)

// 表示使用 seata-xa 模式，完成分布式事务提交！
branchType=XA
```


# 3 结束
