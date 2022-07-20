# 1 包含课程章节

* 《【号外023】.动态代理的两种实现方式_TienChin》
* 《【号外024】.解决多数据源注解失效问题_TienChin》


# 2 AOP 与动态代理

（1）多数据源注解和事务注解，如果**实现类内部方法相互调用**，就会出现相关注解失效问题！
理论上，通过 `AOP` 实现的注解功能，全部都会失效！

（2）`AOP` 面向切面编程，底层是动态代理，Java 中的动态代理有两种

* JDK 动态代理：被代理的对象要有接口，才能使用 JDK 动态代理
* CGLIB 动态代理：所有的对象都能代理，无论被代理的对象有没有接口 `interface`

（3）示例项目
```text
D:\015-MyDocument\03-CodeMK\tienchin-example\proxy-demo
```

（4）解决办法
```text
// 示例项目
D:\015-MyDocument\03-CodeMK\tienchin-example\dynamic-data-source
```

`UserService.java` 文件
```java
// 指定数据源
// DataSourceAspect 后执行，当注解指定了数据源，GlobalDataSourceAspect 失效！
@DataSource("slave")
// 处理本地事务，存在多数据源，即失效
@Transactional
public List<User> getAllUsers() {
    return userMapper.getAllUsers();
}

@SuppressWarnings("all")
@Autowired
UserService userService;

// 测试自调用
// 在 getAllUsers2() 方法里调用 getAllUsers()
// 看 @DataSource("slave") 注解是否还生效？
// 失效了，因为没有调用到 getAllUsers() 的 UserService 动态代理生成的子类
public List<User> getAllUsers2() {
    // 解决自调用方法，注解失效
    // 方法一
    // return userMapper.getAllUsers();

    // 方法二
    // 注入 userService 类，调用自己的方法
    // 注意要开启允许循环依赖 spring.main.allow-circular-references=true
    return userService.getAllUsers();
    // User{id=1, username='Test05', age=200} 成功！

    // return getAllUsers();
}
```

`test.java` 单元测试文件
```java
// 动态数据源测试
@Test
void contextLoads() {
    // List<User> list = userService.getAllUsers();
    // User{id=1, username='Test05', age=200}
    // 多数据源注解 @DataSource("slave") 有效！

    List<User> list = userService.getAllUsers2();
    // User{id=1, username='Test01', age=200}
    // 发现多数据源注解失效 @DataSource("slave")

    for (User user : list) {
        System.out.println(user);
    }
}
```


# 3 结束
