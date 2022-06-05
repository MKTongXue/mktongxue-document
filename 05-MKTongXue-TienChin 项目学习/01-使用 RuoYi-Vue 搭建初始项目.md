# 1 包含课程章节

* 《00.开篇_TienChin》
* 《01.运行RuoYi-Vue_TienChin》
* 《02.代码格式化_TienChin》
* 《03.项目结构大改造_TienChin》


# 2 TienChin 项目初始化

## 2.1 获取项目

（1）
```text
// 参考 RuoYi-Vue 项目，地址
https://gitee.com/y_project/RuoYi-Vue

// 克隆项目到本地
git clone https://gitee.com/y_project/RuoYi-Vue.git

// 导入 mysql 数据库
项目里 /sql/ry_20210908.sql 文件里有创建表结构 Sql 语句，和基础数据。
创建数据库 mktongxue_tienchin，字符集 utf8mb4，排序规则 utf8mb4_general_ci

// 启动 Redis 数据库
// 进入 Redis 解压文件夹
redis-server.exe redis.windows.conf
// 在 Redis 解压的文件夹，打开新的命令窗口
redis-cli.exe -h 127.0.0.1 -p 6379
set myKey MKTongXue
get myKey

// 修改 ruoyi-admin 模块配置文件，有关 Mysql 和 Redis 的配置信息
```

（2）
```text
// Ctrl + Alt + L 可以格式化代码
// 选中整个项目，可以整理所有 .java 文件
```
![格式化代码](http://image.mktongxue.com/202206/001.png)

## 2.2 项目修改

（1）
```text
Ctrl + Shift + R 可以全局查找替换
第一步：全局查找替换 com.ruoyi --> com.mktongxue

第二步：全局查找替换 3.8.2 --> 0.0.1

第三步：ruoyi --> tienchin 要注意大小写（Match case）

第四步：若依 --> TienChin健身

第五步：Shift + F6 修改模块名，修改项目名

第六步：修改包名 com.mktongxue.tienchin

第七步：全局搜索 com.mktongxue.common，改为 com.mktongxue.tienchin.common

第八步：com.mktongxue.tienchin.framework.config.CaptchaConfig 类中修改 KaptchaTextCreator 类的引用地址

// 如果发现启动时报错：主启动类错误，那么重新编译一下项目

// 启动项目前端，后端成功，标志修改成功！
```

（2）注意大小写的查找替换
![注意大小写的查找替换](http://image.mktongxue.com/202206/002.png)

（3）修改模块名
![修改模块名A](http://image.mktongxue.com/202206/003-1.png)
![修改模块名B](http://image.mktongxue.com/202206/003-2.png)

（4）修改包名
![修改包名A](http://image.mktongxue.com/202206/005-1.png)
![修改包名B](http://image.mktongxue.com/202206/005-2.png)

（5）修改 CaptchaConfig 配置文件
![修改 CaptchaConfig 配置文件](http://image.mktongxue.com/202206/006.png)

（6）Maven 重新编译项目
![Maven 重新编译项目](http://image.mktongxue.com/202206/007.png)


# 3 结束
