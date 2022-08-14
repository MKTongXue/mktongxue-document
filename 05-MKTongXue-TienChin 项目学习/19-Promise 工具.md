# 1 包含的课程

* 《069.前端回调地狱_TienChin》
* 《070.Promise初体验_TienChin》
* 《071.then方法的各种情况_TienChin》
* 《072.Promise中的catch代码块_TienChin》
* 《073.Promise中的finally代码块_TienChin》


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


# 4 new Promise().then() 函数

（1）`then()` 方法的参数
`then()` 方法中，可以传递两个回调函数，第一个是成功的回调函数，第二个是失败的回调函数，如果没有传递第二个参数，那么可以在 `catch` 中处理失败回调函数。

```javaScript
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

new Promise(login).then(data => {
    // 如果 login 将来执行成功（就是 resolve 方法抛出执行结果的时候）
    console.log("login: ", data);
}, err => {
    console.error("err: ", err);
})
```

（2）`then()` 方法返回值
- 返回 `new Promise()`，下一个 `then()` 他的主语其实就是上一个 `then()` 返回的 `new Promise()`

```javaScript
A.then(data => {xxx; return B}).then( data => {xxx})
```

由于在 `A` 的 `then` 中返回了 `B`，所以第二个 `then` 的主语，其实是 `B`，不是 `A`（假设 `A` 和 `B` 都是 `Promise` 对象）

- 返回字符串，`then` 方法中可以就返回一个字符串，此时可以一直 `then` 下去，所有的 `then` 方法此时都是同一个主语。

```javaScript
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

new Promise(login).then(data => {
    // 如果 login 将来执行成功（就是 resolve 方法抛出执行结果的时候）
    console.log("then1: ", data);

    return data;  
}).then(data=>{
    console.log("then2: ", data);

    return data;
}).then(data=>{
    console.log("then3: ", data);
}).catch(err=>{
    console.error("err: ", err);
})
```

此时，三个 `then` 都是同一个主语，因为在 `then` 中没有返回新的 `Promise` 对象。每一个 `then` 的参数，都是上一个 `then` 的返回值。

- 抛出异常，可以在 `then` 方法中抛出异常。

```javaScript
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

new Promise(login).then(data => {
    // 如果 login 将来执行成功（就是 resolve 方法抛出执行结果的时候）
    console.log("then1: ", data);

    return data;
}).then(data=>{
    console.log("then2: ", data);

    return data;
}).then(data=>{
    throw new Error("出错啦！");
}).catch(err=>{
    console.error("err: ", err);
})
```

`then` 中还可以直接抛出异常，抛出异常就进入到 `catch` 中了。


# 5 new Promise().catch() 函数

（1）`catch()` 并不是必须的，也可以直接在 `then` 中写两个回调函数，第二个回调函数就是用来处理 `catch` 的，不过更多情况下，都是单独写 `catch` 的。

进入到 `catch` 中，分为两种情况
- `Promise` 在执行过程中，通过 `reject` 返回数据内容
- `then` 中抛出异常
进入 `catch` 的时候，都是就近进入原则。


# 6 new Promise().finally() 函数

（1）无论是最终执行了 `then` 还是 `catch`，都会进入到 `finally` 代码块中。

```javaScript
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

new Promise(login).then(data => {
    // 如果 login 将来执行成功（就是 resolve 方法抛出执行结果的时候）
    console.log("then1: ", data);

    return data;
}).then(data=>{
    console.log("then2: ", data);

    return data;
}).then(data=>{
    // throw new Error("出错啦！");
}).catch(err=>{
    console.error("err1: ", err);
}).finally(()=>{
    console.log("finally 执行！")
}).then(()=>{
    console.log("finally 之后还可以 then 或者 catch 方法")
})
```

无论是 `catch` 还是 `then`，反正 `finally` 都会执行！
`finally` 之后还可以 `then` 或者 `catch` 方法。


# 7 静态方法

（1）


# 8 结束
