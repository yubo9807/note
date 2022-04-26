# Vue3.0 重大改动

### 1. 去掉了构造函数 Vue，用 createApp 代替

> 原因：开发多页应用时，Vue.use()、Vue.mixin()、Vue.component() 会影响所有 vue 应用

```js
import { createApp } from 'vue';
import App from './App.vue';

const app = createApp(App);  // 创建应用，不再是一个组件
app.use();
app.mount('#app');
```

### 2. this 指向 proxy 代理对象，不再指向组件实例

### 3. 使用 composition API

```html
<template>
    <h1 @click="count++">{{ count }}</h1>
</template>

<script>
import { ref } from 'vue';  // 提供响应式
export default {
    setup () {  // 执行在所有生命周期之前
        // console.log(this);  //--> undefined

        let count = ref(0);
        return {
            count  // 返回对象最终会附着在组件实例上
        };
    }
};
</script>
```

##### 功能代码抽离

```html
<template>
    <h1 @click="add">{{ count }}</h1>
</template>

<script>
export default {
    setup () {
        return {
            ...countRef();
        };
    }
};

function countRef () {
    import { ref } from 'vue';
    let count = ref(0);
    const add = () => count.value ++;
    return {
        count,
        add,
    }
}
</script>
```
