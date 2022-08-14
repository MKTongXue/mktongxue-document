# 1 包含的课程

* 《069.前端回调地狱_TienChin》
* 《070.Promise初体验_TienChin》


# 2 什么是回调地狱

（1）经常遇到的流程：登录 -> 获取用户信息 -> 获取用户菜单。
如果使用 Ajax 实现
```javaScript
$.ajax({
    url: '/login',
    data: loginForm,
    ...
    success: function (data) {

        // 登录成功
        $.ajax({
            url: '/getInfo',
            ...
            success: function (data) {

                // 获取用户信息成功
                $.ajax({
                    url: '/getMenus',
                    ...
                    success: function (data) {
                        
                        // 获取用户菜单成功
                        ...
                    }
                })
            }
        })
    }
})
```
原生的 `Ajax`，异步任务执行的逻辑和处理的逻辑写在了一起，导致如果有多个网络请求，并且多个请求存在依赖关系，就会造成回调地狱。
我们希望能够将异步任务执行的代码和处理的代码分离开，能够实现这一需求的工具就是 `Promise`


# 3 Promise 工具

（1）登录 -> 获取用户信息 -> 获取用户菜单。使用 `Promise` 实现。
```javaScript
// 登录
function login(resolve, reject) {
    setTimeout(() => {
        // 生成一个随机数
        let number = Math.random();
        if (number > 0.5) {
            // 登录成功，利用 resolve 函数将登录成功的结果扔出去
            resolve("login success");
        } else {
            // 登录失败，利用 reject 函数将登录失败的结果扔出去
            reject("login error")
        }
    }, 1000);
}

// 获取用户信息
function getInfo(resolve, reject) {
    setTimeout(() => {
        let number = Math.random();
        if (number > 0.5) {
            resolve("getInfo success");
        } else {
            reject("getInfo error")
        }
    }, 1000);
}

// 获取菜单信息
function getMenus(resolve, reject) {
    setTimeout(() => {
        let number = Math.random();
        if (number > 0.5) {
            resolve("getMenus success");
        } else {
            reject("getMenus error")
        }
    }, 1000);
}

new Promise(login).then(data => {
    // 如果 login 将来执行成功（就是 resolve 方法抛出执行结果的时候）
    console.log("login: ", data);

    return new Promise(getInfo);
}).then(data=>{
    // getInfo 执行成功，会进入到这里
    console.log("getInfo: ", data);

    return new Promise(getMenus);
}).then(data=>{
    // getMenus 执行成功
    console.log("getMenus: ", data);
}).catch(err=>{
    // 如果上面任意一个出异常了，都会进入到最近的 catch 代码块中
    console.error("err: ", err);
})
```
`Promise` 中，执行成功，就通过 `resolve` 将成功的结果抛出去；执行失败，就通过 `reject` 将失败的结果抛出去。在 `Promise` 中，只管抛出执行结果即可。
如果是 `resolve` 执行了，则进入到接下来的 `then` 中对异步任务的执行结果进行处理；如果是 `reject` 执行了，则进入到 `catch` 代码块中对异常的结果进行处理。


# 4 new Promise().then 函数

（1）



# 5 结束
