# Vue

[Vue 官方文档](https://cn.vuejs.org/v2/guide/)

### 安装脚手架

```js
npm install -g @vue/cli  // 安装脚手架，用于生成项目
npm install -g @vue/cli-service-global  // 快速原型开发 编译 .vue 文件
```

### 其他命令

```js
vue --version  // 查看 Vue 版本
npm install -g @vue/cli-init  // 桥接工具 拉取旧版本

vue serve test.vue  // 编译 .vue 文件
vue create item  // 创建项目

vue ui  // 界面化 Vue
```

### Vue 实例

```js
new Vue({
    el: "",  // 选择器
    data: {},  // 数据
    template: "<div></div>",
    render () {},  // dom 结构渲染
    directives: {},  // 自定义指令
    filters: {},  // 过滤器
    methods: {},  // 函数调用
    computed: {},   // 计算属性，数据与原先一致则会缓存
    watch: {},  // 侦听器
    components: {},  // 组件
    model: {},  // 监听组件内 prop、事件
});
```

### 钩子函数

```js
new Vue({
    // 创建
    beforeCreate () {},  // 
    created () {},  // 可以拿到 data

    // 挂载
    beforeMount () {},  // 未编译的 dom 结构
    mounted () {},  // dom 编译完成

    // 数据
    beforeDate () {},  // 更改数据
    undated () {},  // 数据更新完成

    // 卸载
    beforeDestroy () {},  // 清除定时器
    destroyed () {},
})
```
