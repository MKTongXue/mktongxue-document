# 1 包含课程章节

* 《035.自定义注解+AOP整理_TienChin》


# 2 自定义注解

（1）在系统运行的时候，动态的向系统中添加代码的行为，就是面向切面编程 AOP

* 前置通知，在目标方法执行之前执行
* 后置通知，在目标方法执行之后执行
* 异常通知，当目标方法抛出异常的时候执行
* 返回通知，当目标方法有返回值的时候执行
* 环绕通知，这是一个集大成者，包含了上面的四种情况

（2）在实际项目中，更多的是通过自定义注解和 AOP 解决各种项目问题

* 事务处理
* 接口限流处理：通过一个前置通知，在目标方法执行之前，统计目标方法在给定的时间窗内已经被调用了多少次了，如果超过流量限制，就禁止通行
* 接口幂等性处理：通过一个前置通知，在目标方法执行之前，先去统计当前请求在给定的时间内是否已经执行过了，如果已经执行过了，那么本次就拒绝执行
* 多数据源切换：通过一个前置通知，在目标方法执行之前，切换系统的数据源，这样，当目标方法执行的时候，就能够获取到切换之后的数据源了
* 日志记录：通过一个返回通知或者异常通知，当目标方法执行出错的时候或者执行有返回值的时候，通过一个异步任务，将日志记录下来
* 数据权限的处理：通过一个前置通知，在目标方法执行之前，添加 SQL 条件，这些条件最终会被添加到 SQL 语句中，进而实现数据过滤
* JDBC Template 等各种 XXX Template


# 3 AOP 原理

（1）`AOP` 就是基于动态代理，但是动态代理有两种实现方式

* 基于 JDK 的动态代理：要求被代理的对象要有接口
* 基于 CGLIB（Library） 的动态代理：不需要被代理的对象有接口

（2）在 `Spring` 中

* 如果被代理的对象有接口，那么默认就是用 JDK 动态代理
* 如果被代理的对象没有接口，那么就使用 CGLIB 动态代理

（3）在 `Spring Boot` 中

* 在 Spring Boot 2.0 之前，如果开发者没有配置 `spring.aop.proxy-target-class` 属性，默认会使用 JDK 动态代理
* 在 Spring Boot 2.0 之后，默认情况下，就是使用 CGLIB 动态代理，无论被代理的对象是否有接口，都使用 CGLIB 动态代理
* 如果 `spring.aop.proxy-target-class` 属性设置为 true，那么对于有接口的对象，也会使用 CGLIB 动态代理
* 如果 `spring.aop.proxy-target-class` 属性为 false，对于有接口的属性，会使用 JDK 动态代理

（4）小结

* Spring 中，有接口用 JDK 动态代理，没接口，用 CGLIB 动态代理
* Spring Boot 中，2.0 之前，和 Spring 一样；2.0 之后，首选 CGLIB，如果想用 JDK 动态代理，需要开发者手动配置


# 4 结束
