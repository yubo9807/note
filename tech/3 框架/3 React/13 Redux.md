# Redux

## action

- action 是一个平面对象，它的 `__proto__` 指向 `Object.prototype`；
- 必须要有 type 属性，用于描述操作类型；
- action 创建函数应为无副作用的纯函数。

## reducer

## store

|                  |                    |
| ---------------- | ------------------ |
| `dispatch`       | 分发一个 action    |
| `getstate`       | 得到仓库中当前状态 |
| `replaceReducer` | 替换当前的 reducer |
| `subscribe`      | 注册一个监听器     |

