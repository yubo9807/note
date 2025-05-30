# Vuex

##### main.js

```js
import Vue from 'vue'
import Vuex from 'vuex'
import App from './App.vue'

Vue.use(Vuex);

const store = new Vuex.store({
    state: {
        count: 0,
    }
})

new Vue({
    render: h => h(App),
    store,
}).$mount('#app')
```

##### cmp.vue

```js
export default {
    created () {
        console.log(this.$store.state.count);  //--> 0
    }
}
```

##### cmp.vue

```js
import { mapState } from 'vuex'
export default {
    computed: {
        ...mapState(['count']),
        ...mapState({
            storeCount: 'count',  //== state => state.count  重命名，防止与 data 数据冲突
        })
    },
    created () {
        console.log(this.$store.state.count);  //--> 0
    }
}
```

## Getter

```js
const store = new Vuex.store({
    getters: {
        countAdd: num => num + 10;
    }
})
```
```js
import { mapGetters } from 'vuex'
export default {
    computed: {
        ...mapGetters(['countAdd']),
    },
    created () {
        console.log(this.countAdd(12));  //--> 22
    }
```

## Mutation

- 严格模式下，更改 Vuex 的 state 中的状态的唯一方法是提交 mutation

```js
const store = new Vuex.store({
    // process.env.NODE_ENV !== 'prodution'
    strict: true,  // 开启 Vuex 严格模式，深度监听对象（性能下降）
    state: {
        count: 10,
    },
    mutations: {
        /**
         * @param {Object} state state 数据对象
         * @param {*} num 传入参数
         */
        countIncrement (state, num) {
            state.count += num
        }
    }
})
```

```js
import { mapMutations } from 'vuex'
export default {
    created () {
		this.countIncrement(10);
		console.log(this.$store.state.count);  //--> 20
	}
```

## Actions

```js
const store = new Vuex.store({
    // process.env.NODE_ENV !== 'prodution'
    strict: true,  // 开启 Vuex 严格模式，深度监听对象（性能下降）
    state: {
        count: 10,
    },
    actions: {
        countIncrement (store, num) {
            setTimout(() => {  // Actions 内可执行异步操作
                store.state.count += num;
            }, 1000)
        }
    },
})
```

```js
import { mapMutations } from 'vuex'
export default {
    created () {
        new Promise((res, rej) => {
            this.$store.dispatch('countIncrement', 10);
            res();
        }).then(() => {
            console.log(this.$store.state.count);  //--> 20
        })
    }
}
```
