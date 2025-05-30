# render 渲染函数

- 优先级比 template 更高
- 运行时体积更小，加载时间更快
- 更好的编程能力

```html
<div id="app"></div>  <!-- <h1>hello</h1> -->

<script>
    new Vue({
        render: createElement => {
            const vNode = createElement('h1', 'hello');
            console.log(vNode);
            return vNode;
        }
    }).$mount('#app');
</script>
```

```html
<div id="app">
    <my-cmp :level='1'>一级标题</my-cmp>
    <my-cmp :level='2'>二级标题</my-cmp>
    <my-cmp :level='3'>三级标题</my-cmp>
</div>

<script>
    Vue.component('my-cmp', {
        props: {
            level: {
                type: Number,
                required: true
            }
        },
        created () {
            
        },
        render (createElement) {
            return createElement('h' + this.level, this.$slots.default)
        }
    });
    new Vue({
        el: '#app'
    })
</script>
```

[createElement 参数](https://cn.vuejs.org/v2/guide/render-function.html)

```html
<div id="app"></div>  <!-- <h1>hello</h1> -->

<script>
    new Vue({
        render: createElement => {
            return createElement('h1', {
                class: {
                    foo: true,
                    bar: false
                },
                style: {
                    color: 'red'
                },
                attrs: {  // 普通特性
                    id: 'demo',
                    index: 3
                },
                domProps: {
                    innerHTML: '<span>bozai</span>'
                },
                on: {  // 事件监听
                    click () {
                        console.log(1234)
                    }
                },
            }, ['hello']);
        }
    }).$mount('#app');
</script>
```
