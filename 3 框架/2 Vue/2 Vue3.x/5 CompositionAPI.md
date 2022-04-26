# CompositionAPI

1. 更好的逻辑复用和代码组织；
2. 更好的类型推导（TS）。

## setup

```js
export default {
    setup (props, context) {
        context.attrs;  // Vue2 的 this.$attrs
        context.slots;  // Vue2 的 this.$slots
        context.emit;  // Vue2 的 this.$emit
        
        onBeforeMount();  // 挂载前一刻
        onMounted();  // 挂载结束
        onBeforeUpdate();  // 数据更新时，但页面还未改动
        onUpdated();  // 数据更新，页面已经将数据替换
        onBeforeUnmount();  // 卸载组件之前
        onUnmounted();  // 卸载组件之后
        onErrorCaptured((err, instance, info) => {});  // 捕获一个来自子孙组件的错误时被调用
        onRenderTracked(e => {});  // 参数依赖收集
        onRenderTriggered(e => {});  // 依赖更改导致页面重新渲染时调用
    }
}
```





