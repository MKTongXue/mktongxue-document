# 1 Java 关键字

## 1.1 关键字列表

| **关键字**   | **含义**                                                     |
| :----------- | :---------------------------------------------------------- |
| abstract     | 表明类或者成员方法具有抽象属性                                 |
| assert       | 断言，用来进行程序调试                                        |
| boolean      | 基本数据类型之一，声明布尔类型的关键字                          |
| break        | 提前跳出一个块                                               |
| byte         | 基本数据类型之一，字节类型                                   |
| case         | 用在 switch 语句之中，表示其中的一个分支                     |
| catch        | 用在异常处理中，用来捕捉异常                                 |
| char         | 基本数据类型之一，字符类型                                   |
| class        | 声明一个类                                                   |
| const        | 保留关键字，没有具体含义                                     |
| continue     | 回到一个块的开始处                                           |
| default      | 默认，例如，用在 switch 语句中，表明一个默认的分支。Java8 中也作用于声明接口函数的默认实现 |
| do           | 用在 do-while 循环结构中                                     |
| double       | 基本数据类型之一，双精度浮点数类型                           |
| else         | 用在条件语句中，表明当条件不成立时的分支                     |
| enum         | 枚举                                                         |
| extends      | 表明一个类型是另一个类型的子类型。对于类，可以是另一个类或者抽象类；对于接口，可以是另一个接口 |
| final        | 用来说明最终属性，表明一个类不能派生出子类，或者成员方法不能被覆盖，或者成员域的值不能被改变，用来定义常量 |
| finally      | 用于处理异常情况，用来声明一个基本肯定会被执行到的语句块     |
| float        | 基本数据类型之一，单精度浮点数类型                           |
| for          | 一种循环结构的引导词                                         |
| goto         | 保留关键字，没有具体含义                                     |
| if           | 条件语句的引导词                                             |
| implements   | 表明一个类实现了给定的接口                                   |
| import       | 表明要访问指定的类或包                                       |
| instanceof   | 用来测试一个对象是否是指定类型的实例对象                     |
| int          | 基本数据类型之一，整数类型                                   |
| interface    | 接口                                                         |
| long         | 基本数据类型之一，长整数类型                                 |
| native       | 用来声明一个方法是由与计算机相关的语言（如 C/C++/FORTRAN 语言）实现的 |
| new          | 用来创建新实例对象                                           |
| package      | 包                                                           |
| private      | 一种访问控制方式：私用模式                                   |
| protected    | 一种访问控制方式：保护模式                                   |
| public       | 一种访问控制方式：共用模式                                   |
| return       | 从成员方法中返回数据                                         |
| short        | 基本数据类型之一，短整数类型                                 |
| static       | 表明具有静态属性                                             |
| strictfp     | 用来声明 FP_strict（单精度或双精度浮点数）表达式遵循 IEEE754 算术规范 |
| super        | 表明当前对象的父类型的引用或者父类型的构造方法               |
| switch       | 分支语句结构的引导词                                         |
| synchronized | 表明一段代码需要同步执行                                     |
| this         | 指向当前实例对象的引用                                       |
| throw        | 抛出一个异常                                                 |
| throws       | 声明在当前定义的成员方法中所有需要抛出的异常                 |
| transient    | 声明不用序列化的成员域                                       |
| try          | 尝试一个可能抛出异常的程序块                                 |
| void         | 声明当前成员方法没有返回值                                   |
| volatile     | 表明两个或者多个变量必须同步地发生变化                       |
| while        | 用在循环结构中                                               |


## 1.2 关键字分组
1. 用于数据类型
``` java
boolean、byte、char、double、float、int、long、new、short、void、instanceof
```

2. 用于语句
```java
break、case、catch、continue、default、do、else、for、if、return、switch、try、while、finally、throw、this、super
```

3. 用于修饰
```java
abstract、final、native、private、protected、public、static、synchronized、transient、volatile
```

4. 用于方法、类、接口、包和异常
```java
class、extends、implements、interface、package、import、throws
```

5. Java 保留字
```java
// 保留的没有意义的关键字
future、generic、operator、outer、rest、var

// 不是关键字，而是文字
goto、const、null
```


# 2 Java 标识符规则
- 所有标识符都应该以字母（ A-Z a-z ），美元符号（ $ ），或者下划线（ _ ）开始。
- 首字符之后可以是字母（ A-Z a-z ），美元符号（ $ ），下划线（ _ ），或者数字的任何字符组合。
- 不能使用**关键字**作为变量名或方法名。
- 标识符大小写敏感。
- 合法标识符示例：age、$salary、_value、_1_value
- 非法标识符示例：123abc、-salart、#abc
- 可以使用中文命名，但是不建议这么使用，一般也不要使用拼音命名。


# 3 Java 数据类型
Java 是强类型语言，要求变量的使用要严格符合规定，所有变量都必须先定义后才能使用。弱类型语言有 JavaScript 等。

## 3.1 基本类型
一个字节的二进制位数：8 位（ 8 个 0 或者 1，示例：0101 1100 ）

1. 整数类型（数值类型）
    - byte 类型，1个字节，-128 到 127
    - short 类型，2个字节，-32768 到 32767
    - int 类型，4个字节，-2147483648 到 2147483647
    - long 类型，8个字节，-9223372036854775808 到 9223372036854775807
2. 浮点类型（数值类型）
    - float 类型，4个字节
    - double 类型，8个字节
3. 字符类型（数值类型）
    - char 类型，8个字节，0 到 65535
4. boolean 类型，1个 bit 位，true 或者 false

## 3.2 引用类型
类，接口，数组等


# 4 什么是字节？
1. 位（bit）是计算机内部数据储存的最小单位，1100 1100 是一个八位二进制数。
2. 字节（byte）是计算机中数据处理的基本单位，习惯上用大写 B 来表示。
3. 1B（byte，字节）= 8 bit（位）
4. 字符是指计算机中使用的字母、数字、字和符号。

```text
1bit 表示 1 位
1Byte 表示一个字节，1B = 8bit
1024B = 1KB
1024KB = 1MB
1024MB = 1GB

32位=4个字节
64位=8个字节
```


# 5 类型转换
由于 Java 是强类型语言，所以进行运算时候，需要用到类型转换。

```text
byte short char -> int -> long -> float -> double
低 --------------------------------------> 高

运算中，不同类型数据先转换成同一类型，然后进行运算
低 到 高，自动类型转换
高 到 低，需要强制类型转换
```


# 6 变量和常量

## 6.1 变量
1. 变量是可以变化的量。
2. Java 是一种强类型语言，每个变量都必须声明其类型。
3. Java 变量是程序中最基础的存储单元，其要素包括：变量名、变量类型、作用域。
4. 注意事项
``` text
（1）每个变量都有类型，类型可以是基础类型、引用类型。
（2）变量名必须是合法的标识符。
（3）变量声明是一条完整的语句、因此每一个声明都必须以分号结束。
（4）按照作用域可以分为：类变量，实例变量，局部变量。
```

## 6.2 常量
常量（Constant）：初始化后不可再改变的值！不会变动的值！  
所谓常量可以理解为一种特殊的变量，它的值被设定后，在程序运行过程中不允许被改变。  
常量名一般使用大写字符。  
```text
final 常量名 = 值 ;
例子：final double PI = 3.14;
```

## 6.3 命名规范
1. 所有变量、方法、类名：**见名知意**
2. 类成员变量：首字母小写和驼峰原则：monthSalary
3. 局部变量：首字母小写和驼峰原则
4. 常量：大写字母和下划线：MAX_VALUE
5. 类名：首字母大写和驼峰原则：Man，GoodMan
6. 方法名：首字母小写和驼峰原则：run() getName()


# 7 运算符
Java 运算符
```text
算术运算符 + - * / % ++ --
赋值运算符 =
关系运算符 > < >= <= !=
逻辑运算符 && || !
位运算符 & | ^ ~ >> << >>>
条件运算符 ? ：
拓展运算符 += -= *= /=
```


# 8 包机制
为了更好的组织类，Java 提供包机制，用于区别类名的命名空间。
```text
package com.mktongxue.packagetest

一般使用公司域名倒置，作为包名。
为了能够使用某一个包的成员，我们需要在 java 程序中明确导入该包，使用 import 即可。
```


# 9 其它
1. 快捷键
```java
// Ctrl + 鼠标左键，可以查看 String 引用类型定义
String s = "MKTongXue";

// 报错处，按住 Alt + 回车键，自动处理错误信息
Date
```

2. 书籍：《阿里巴巴Java开发手册》

3. JavaDoc 生成帮助文档，命令实现
```text
参数信息
@author 作者名
@version 版本号
@since jdk 版本
@param 参数名
@return 返回值
@throws 异常情况
```

```text
cmd 文件夹路径

执行命令，生成java帮助文档
javadoc -encoding UTF-8 -charset UTF-8 Doc01.java
```
4. JavaDoc 生成帮助文档，IDEA 中实现

![Tools](http://image.mktongxue.com/202205/008.png)

![JavaDoc](http://image.mktongxue.com/202205/009.png)


# 10 结束
