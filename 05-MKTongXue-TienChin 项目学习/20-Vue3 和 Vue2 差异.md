# 1 包含的课程

* 《076.Vue3中的变量定义方式_TienChin》
* 《077.Vue3中方法的定义_TienChin》
* 《078.Vue3中钩子函数的定义_TienChin》
* 《079.Vue3中的计算属性_TienChin》
* 《080.Vue3中的watch函数_TienChin》


# 2 变量定义

（1）`Vue3` 中可以原封不动的使用 `Vue2` 中的方法（Options API）。但是 `Vue3` 中提供了一些语法糖。

（2）在 `Vue2` 中定义变量
```javaScript
<template>
    <!-- Vue2 用法 -->
    <div>hello 01!</div>
    <h1>{{msg}}</h1>
</template>

<script>
    export default {
        name: "My01",
        data(){
            return{
                msg: "hello mktongxue!"
            }
        }
    }
</script>

<style scoped>

</style>
```

（3）在 `Vue3` 中定义变量
```javaScript
<template>
    <!-- Vue3 用法 -->
    <div>
        <div>hello 01!</div>
        <h1>{{msg}}</h1>
        <input type="text" v-model="msg">
    </div>
</template>

<script>
    import {ref} from 'vue';

    export default {
        name: "My02",
        /**
         * 我们以前在 Vue2 中定义的各种变量、方法、生命周期钩子函数等等，现在统一都在 setup 中进行定义。
         *
         * 需要注意的是，所有定义的变量，方法等，都需要返回之后才可以使用。
         * 
         */
        setup() {
            // 注意，直接这样写，这个变量不是响应式数据
            // let msg = "hello vue3";

            // 响应式写法
            let msg = ref("hello vue3");
            return {msg};
        }
    }
</script>

<style scoped></style>
```

（4）注意点
*  变量定义，需要用到 `ref` 函数，该函数，直接从 `vue` 中导入，否则直接定义的变量不具备响应式的特性。
* 所有定义的变量、方法等，都需要 `return`，不 `return`，使用不了。


# 3 方法定义

（1）在 `Vue2` 中，我们一般是将方法定义在 `methods` 节点中，但是在 `Vue3` 中，我们将方法定义在 `setup` 方法中，尤其要注意，方法定义完成之后，必须要返回方法名，否则方法用不了。
像定义一个变量一样去定义方法，方法定义完成之后，一定要返回。

```html
<template>
    <div>
        <button @click="doLogin('zhangsan','123')">登录</button>
    </div>
</template>

<script>
export default{
    name:"TestFunction",
    setup() {
        // 定义方法
        const doLogin = (username, password) => {
            console.log(username);
            console.log(password);
        }
        return {doLogin};
    }
}
</script>
```


# 4 钩子函数

（1）在 `Vue2` 中，定义钩子函数，直接定义对应的方法名即可。
```javaScript
<template>
    <!-- Vue2 用法 -->
    <div>hello 01!</div>
    <h1>{{msg}}</h1>
</template>

<script>
    export default {
        name: "My01",
        data() {
            return{
                msg: "hello mktongxue!"
            }
        },

        // 钩子函数
        mounted() {
            console.log("Vue2 使用 mounted() 函数");
        }
    }
</script>

<style scoped>

</style>
```

（2）在 `Vue3` 中，所有的东西都是在 `setup` 中定义的，包括钩子函数。
```javaScript
<template>
    <div>
        <button @click="doLogin('zhangsan','123')">登录</button>
    </div>
</template>

<script>
// 使用钩子函数时，首先导入钩子函数
import {onMounted} from 'vue';

export default{
    name:"TestFunction",
    setup() {
        // 定义方法
        const doLogin = (username, password) => {
            console.log(username);
            console.log(password);
        }

        // 调用钩子函数，并传入回调函数
        // 另外需要注意，这个钩子函数不需要返回
        onMounted(() => {
            console.log("Vue3 使用 onMounted() 函数")
        })

        return {doLogin};
    }
}
</script>
```

（3）首先从 `vue` 中导入钩子函数。在 `setup` 方法中去定义钩子函数的逻辑。在 `return` 中，不需要返回钩子函数。

|  Vue2   | Vue3  |
|  :----  | :----  |
| mounted | onMounted |
| beforeUpdate | onBeforeUpdate |
| updated | OnUpdated |
| beforeUnmount | OnBeforeUnmounted |
| unmounted | OnUnmounted |
| errorCapture | OnErrorCapture |
| renderTracked | OnRenderTracked |
| renderTriggered | OnRenderTriggered |
| activated | OnActivated |
| deactivated | OnDeactivated |


# 5 计算属性 Computed

（1）计算属性和钩子函数比较类似，计算属性使用步骤：
* 从 `vue` 中导入计算属性函数
* 定义计算属性
* 在 `return` 中返回计算属性值

```javaScript
<template>
    <div>
        <button @click="doLogin('zhangsan','123')">登录</button>
    </div>

    <div> {{currentTime}} </div>
</template>

<script>
// 使用钩子函数时，首先导入钩子函数
// 计算属性的使用，也需要首先导入计算属性
import {onMounted, computed} from 'vue';

export default{
    name:"TestFunction",
    setup() {
        // 定义方法
        const doLogin = (username, password) => {
            console.log(username);
            console.log(password);
        }

        // 调用钩子函数，并传入回调函数
        // 另外需要注意，这个钩子函数不需要返回
        onMounted(() => {
            console.log("Vue3 使用 onMounted() 函数")
        })

        // 现在就可以通过计算属性去定义一个变量了
        const currentTime = computed(()=>{
            return Date.now()
        })

        // 注意，计算属性需要在 return 中返回
        return {doLogin, currentTime};
    }
}
</script>
```

（2）使计算属性内值更新

```javaScript
<template>
    <div>
        <button @click="doLogin('zhangsan','123')">登录</button>
    </div>

    <div> {{currentTime}} </div>

    <h2> {{msg}} </h2>
    <h2> {{age}} </h2>
</template>

<script>
// 使用钩子函数时，首先导入钩子函数
// 计算属性的使用，也需要首先导入计算属性
import {onMounted, computed} from 'vue';

import {ref} from 'vue';

export default{
    name:"TestFunction",
    setup() {
        let msg = ref("hello vue3");
        let age = ref(99);

        // 定义方法
        const doLogin = (username, password) => {
            console.log(username);
            console.log(password);

            age.value++;
            msg.value = 'hello MKTongXue';
        }

        // 调用钩子函数，并传入回调函数
        // 另外需要注意，这个钩子函数不需要返回
        onMounted(() => {
            console.log("Vue3 使用 onMounted() 函数")
        })

        // 现在就可以通过计算属性去定义一个变量了
        const currentTime = computed(()=>{
            // age 响应式数据值变化，才会更新计算属性
            age.value++;
            return Date.now()
        })

        // 注意，计算属性需要在 return 中返回
        return {doLogin, currentTime, age, msg};
    }
}
</script>
```

由于生成计算属性 `currentTime` 依赖 `age` 变量，所以当 `age` 变量发生变化的时候，计算属性会自动更新，否则计算属性将一直使用缓存中的数据（`age` 没有发生变化的情况）。
另外还有一点，就是定义的变量入 `age` 和 `msg` 等 ，在 `HTML` 节点中，直接使用 `age`、`msg`，但是如果是在方法中操作这些变量，则一定要使用 `age.value` 或者 `msg.value` 去操作这些变量。


# 6 Watch 函数

（1）`Vue3` 中 `watch` 函数写法
```javaScript
<template>
    <div>
        <button @click="doLogin('zhangsan','123')">登录</button>
    </div>

    <div> {{currentTime}} </div>

    <h2> {{msg}} </h2>
    <h2> {{age}} </h2>
</template>

<script>
// 使用钩子函数时，首先导入钩子函数
// 计算属性的使用，也需要首先导入计算属性
import {onMounted, computed, watch} from 'vue';

import {ref} from 'vue';

export default{
    name:"TestFunction",
    setup() {
        let msg = ref("hello vue3");
        let age = ref(99);

        // 定义方法
        const doLogin = (username, password) => {
            console.log(username);
            console.log(password);

            age.value++;
            msg.value = 'hello MKTongXue';
        }

        // 调用钩子函数，并传入回调函数
        // 另外需要注意，这个钩子函数不需要返回
        onMounted(() => {
            console.log("Vue3 使用 onMounted() 函数")
        })

        // 现在就可以通过计算属性去定义一个变量了
        const currentTime = computed(()=>{
            // age 响应式数据值变化，才会更新计算属性
            age.value++;
            return Date.now()
        })

        // watch 函数
        watch(age, (newValue, oldValue) => {
            console.log("newValue", newValue);
            console.log("oldValue", oldValue);
        })

        // 注意，计算属性需要在 return 中返回
        return {doLogin, currentTime, age, msg};
    }
}
</script>
```

* 先从 `vue` 中导入 `watch` 函数。
* 在 `setup` 中去监控变量，第一个参数是要监控的变量，第二个参数则是一个回调函数，回调函数的参数就是所监控变量值的变化。


# 7 `ref` 和 `reactive` 函数

（1）


# 8 结束
