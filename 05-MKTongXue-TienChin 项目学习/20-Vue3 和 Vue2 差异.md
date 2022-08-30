# 1 包含的课程

* 《076.Vue3中的变量定义方式_TienChin》
* 《077.Vue3中方法的定义_TienChin》
* 《078.Vue3中钩子函数的定义_TienChin》
* 《079.Vue3中的计算属性_TienChin》
* 《080.Vue3中的watch函数_TienChin》
* 《081.Vue3中的ref和reactive_TienChin》
* 《082.Vue3中的setup函数_TienChin》


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
```javaScript
<template>
    <div>
        <div>{{age}}</div>

        <div>{{book.name}}</div>

        <div>{{book.author}}</div>
    </div>
</template>

<script>
    import {ref, reactive} from 'vue';

    export default {
        name: "My03",
        setup() {
            const age = ref(99);

            const book = reactive({
                name: "三国演义",
                author: '罗贯中'
            });

            return {age, book};
        }
    }
</script>

<style scoped></style>
```

一般来说，我们通过 `ref` 来定义一个变量，一般都是原始数据类型，例如 `String`、`Number`、`BigInt`、`Boolean` 等，通过 `reactive` 来定义一个对象。

如上面的案例所示，定义了 `book` 对象之后，接下来的访问中，通过 `book.xxx` 就可以访问到 `book` 中的属性值了。

但是，假设我们在定义的时候，定义的是 `book` 对象，但是我们访问的时候，却希望能够直接按照属性来访问，此时可以直接展开变量，但是，如果直接通过三个点去展开变量 `...book`，会导致变量的响应式特点失效，此时，我们可以通过 `toRefs` 函数，让变量恢复响应式的特点。

```javaScript
<template>
    <div>
        <div>{{age}}</div>

        <!-- <div>{{book.name}}</div> -->
        <!-- <div>{{book.author}}</div> -->

        <div>{{name}}</div>
        <div>{{author}}</div>
        <button @click="updateBookInfo">更新图书信息</button>
    </div>
</template>

<script>
    import {ref, reactive, toRefs} from 'vue';

    export default {
        name: "My03",
        setup() {
            const age = ref(99);

            const book = reactive({
                name: "三国演义",
                author: '罗贯中'
            });

            const updateBookInfo = ()=>{
                // 修改书名
                // 注意，在 vue3 中，现在方法中访问变量，不再需要 this
                book.name = '三国演义 AAA';
            }
            
            // 如果直接写 ...book 会导致响应式失效
            // 通过 toRefs 函数，可以解决这个问题 ...toRefs(book)
            return {age, ...toRefs(book), updateBookInfo};
        }
    }
</script>

<style scoped></style>
```

（2）小结
* `ref` 定义原始数据类型；`reactive` 定义对象。
* 如果用到了对象展开，那么需要用到 `toRefs` 函数将对象中的属性变为响应式。
* 在 `vue3` 中，定义的变量、函数等等，在使用的时候，都不需要 `this`。


# 8 `setup()` 方法

（1）
```javaScript
<template>
    <div>
        <div>{{age}}</div>

        <div>{{book.name}}</div>
        <div>{{book.author}}</div>

        <div>{{name}}</div>
        <div>{{author}}</div>
        <div>
            <button @click="updateBookInfo">更新图书信息</button>
        </div>

    </div>
</template>

<!-- 直接在 script 节点中定义 setup 属性，然后，script 节点就像以前 jquery 写法一样 -->
<script setup>
    import {ref, reactive, toRefs} from 'vue';

    const age = ref(99);

    const book = reactive({
        name: "三国演义",
        author: '罗贯中'
    });

    const updateBookInfo = () => {
        book.name = '三国演义 BBB';
    }

    // 展开的变量
    const {name, author} = toRefs(book);
</script>

<style scoped></style>
```

直接在 `script` 节点中，增加 `setup` 属性，然后 `script` 节点中定义的变量名、方法名等等，默认就会自动返回，我们只需要使用即可。


# 9 结束
