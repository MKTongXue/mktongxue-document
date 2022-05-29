# 1 Java 概述

## 1.1 Java 三大版本
- JavsSE：标准版（桌面程序，控制台开发）
- JavaME：嵌入式开发（手机，小家电）（死亡）
- JavaEE：企业级开发（Web 端，服务器开发）


## 1.2 跨平台
**Write Once Run Anywhere** 一次编写，多环境运行。


## 1.3 框架
* JDK：Java Development Kit（Java 开发工具包）
* JRE：Java Runtime Environment（Java 运行时环境）
* JVM：Java Virtual Machine（Java 虚拟机）


## 1.4 Oracle 官网
[Oracle 官网](https://www.oracle.com)  
[JDK 8 下载地址](https://www.oracle.com/java/technologies/downloads)


## 1.5 卸载 JDK
1. 删除 Java 安装目录（环境变量 JAVA_HOME 可以查看）
2. 删除 JAVA_HOME（此电脑 - 属性 - 高级系统设置 - 环境变量 - 系统变量 - JAVA_HOME）
3. 删除 Path 下关于 JAVA_HOME 两个目录
4. Win + R 后 cmd 输入命令 java -version 显示非法命令（下次安装，无视其它直接安装即可）


## 1.6 安装 JDK

### 1.6.1 下载 JDK8
百度搜索 JDK8，oracle 官网登录，同意协议，下载电脑对应的版本。
双击安装 JDK 即可，**记住安装的路径。**


### 1.6.2 配置环境变量
```text
（1）此电脑 - 属性 - 高级系统设置 - 环境变量 - 系统变量

（2）新增 JAVA_HOME 变量
JAVA_HOME
D:\Environment\java\jdk1.8.0_251 // 视个人情况

（3）配置 Path 变量
%JAVA_HOME%\bin
%JAVA_HOME%\jre\bin

（4）测试 JDK 是否安装成功
Win + R 后 cmd 输入命令 java -version 显示 JDK 版本信息
```

## 1.7 Hello World

1.7.1 在文件夹创建文件 `HelloWorld.java` 输入以下代码
```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

1.7.2 文件夹前输入 cmd 到此路径下
```java
// 编译
javac HelloWorld.java
// 运行
java HelloWorld
```

1.7.3 运行结果  
![运行结果](https://mktongxue-document.oss-cn-hangzhou.aliyuncs.com/202205/003.png)


## 1.8 Java 程序运行机制
1. 源代码（.java）
2. 通过（Java 编译器）编译为字节码文件（.class）
3. 通过 JVM 解释执行字节码文件


## 1.9 IDEA 安装
1.9.1 [IDEA 官网地址](https://www.jetbrains.com)

1.9.2 安装时配置截图  
![配置截图](https://mktongxue-document.oss-cn-hangzhou.aliyuncs.com/202205/005.png)

# 2 结束
