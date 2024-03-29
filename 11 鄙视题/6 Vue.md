# Vue

## Vue 指令有哪些？

v-if、v-show、v-for、v-bind、v-html、v-text、v-once、v-pre、v-model、v-slot

## 列表组件中的 key 作用是什么？

1. 更准确：key 值具有唯一性，避免了复用的情况
2. 查询速度更快：通过生成 map 对象来遍历集合，更加快速的查询到该对象地址

## 双向数据绑定原理

- 监控带有 v-model 属性的 input 框，在失去焦点时触发对数据的监听，刷新页面。

## 响应式原理

- vue 数据响应式的初衷是为了实现数据和函数的联动，当数据发生变化后，用到该数据的函数自动重新运行；
- 具体的开发中，数据和 render 函数关联在一起，从而实现了数据变化自动运行 render，在感官上就看到的组件的重新渲染；
- 除了自动关联 render 函数，还有 computed、watch 这样的 API 也属于数据响应式。

1. 监听属性修改，捕获事件；
2. 对数据进行渲染，
    - 建立树形结构，模板与节点之间形成映射关系，查找节点与属性，进行挂载；
3. 改变数据，只对该数据对应的节点进行数据刷新，挂载替换。

## 说说对于虚拟 DOM 与 DOM 之间 diff 算法的理解

- Vue 中的 DOM 之间的 diff 算法与二叉树之间的比较比较相似，通过递归来比较各个子节点之间的状态来确定元素及属性的变化，对节点的位置信息进行记录

## 为什么在组件中 data 是一个函数，而 new Vue() 可以是一个对象？

- 因为组件是需要被重复调用的，所以必须是一个函数，
    - 如果是一个对象，作用域没有分开，子组件的 data 值就会相互影响；
    - 如果是一个函数，每个实例就可以维护一份被返回对象独立的拷贝；
- new Vue() 不会被重复复用，所以可以是一个对象。

## 子组件为何不可以修改父组件传递的 prop，如果修改了，Vue 是如何监控到属性的修改并给出警告的。

- 单向数据流，易于监测数据的流动，出现了错误可以更加迅速的定位到错误发生的位置；
    - 每当父组件属性值修改时，该值都将被覆盖；
- 组件对于data的监听是深度监听，而对于props的监听是浅度监听。

## 双向数据绑定和单项数据流

- **双向绑定**：数据改变驱动视图改变，视图反过来也可以改变数据；
- **单项数据流**：只通过数据改变驱动视图改变。

> 原理：数据劫持，观察者模式

## MVC 与 MVVM 的区别

1. **MVC**： 最早出现于服务端，通过控制器来响应不同的资源请求，处理所需要的数据，生成视图给客户端。model view controller。
2. **MVVM**：为解决页面代码/数据的复杂度问题。通过数据渲染视图，通过视图改变数据模型。

> 前端难以使用 MVC 模式的原因：前端中的 controller 处理的是复杂的用户操作；Vue/React 使用的是单向数据流，若需要共享数据，则必须将数据提升到顶层组件，然后一层一层传递，极其繁琐。若共享数据很多，会导致上下文中的数据变得非常复杂。

### MVC框架的主要问题

- 对 DOM 操作的代价非常高
- 程序运行缓慢且效率低下
- 内存浪费严重
- 由于循环依赖性，组件模型需要围绕 models 和 views 进行创建

## Vue 和 React 有哪些区别

1. **数据流**：
    - **React** 主张函数式编程，所以推崇纯组件，数据不可变，单向数据流；
    - **Vue** 的思想是响应式的，也就是基于是数据可变的，通过对每一个属性建立Watcher来监听，当属性变化的时候，响应式的更新对应的虚拟dom。
2. **监听数据变化实现原理**：
    - `Vue` 通过 `getter/setter` 以及一些函数的劫持，能精确知道数据变化，不需要特别的优化就能达到很好的性能；
    - `React` 默认是通过比较引用的方式进行的，如果不优化( `PureComponent` / `shouldComponentUpdate` )可能导致大量不必要的 VDOM 的重新渲染。
3. **组件通信**：
    - **Vue** 中我们组合不同功能的方式是通过 `Mixin`；
    - **React** 中通过 `HoC` (高阶组件)。
4. **性能优化**：
    - **React** `shouldComponentUpdate` ；
    - **Vue** 内部实现 `shouldComponentUpdate` 的优化，由于依赖追踪系统存在，通过 `watcher` 判断是否需要重新渲染(当一个页面数据量较大时，`Vue` 的性能较差，造成页面卡顿，所以一般数据比较大的项目倾向使用 `React` )。
5. **代码层面**：
    - **React** 在写法上比 Vue 更加随意；
    - **Vue2** 过度的改变了 this 指向问题，很难将功能进行模块化分离，不好维护；
6. **模板**：
    - **vue template**：只能访问 data，prop、method，可以静态的分析和优化（结合 TypeScript 相对困难）；
    - **jsx**：动态逻辑比较多，没法静态的做分析和优化；

## Redux 三个原则

- **单一事实来源：**整个应用的状态存储在单个 store 中的对象/状态树里。单一状态树可以更容易地跟踪随时间的变化，并调试或检查应用程序。
- **状态是只读的：**改变状态的唯一方法是去触发一个动作。动作是描述变化的普通 JS 对象。就像 state 是数据的最小表示一样，该操作是对数据更改的最小表示。
- **使用纯函数进行更改：**为了指定状态树如何通过操作进行转换，你需要纯函数。纯函数是那些返回值仅取决于其参数值的函数。

## 单一事实来源

- Redux 使用 “Store” 将程序的整个状态存储在同一个地方。因此所有组件的状态都存储在 Store 中，并且它们从 Store 本身接收更新。单一状态树可以更容易地跟踪随时间的变化，并调试或检查程序。

## Redux 有哪些优点

- 结果的可预测性 -  由于总是存在一个真实来源，即 store ，因此不存在如何将当前状态与动作和应用的其他部分同步的问题。
- 可维护性 -  代码变得更容易维护，具有可预测的结果和严格的结构。
- 服务器端渲染 -  你只需将服务器上创建的 store 传到客户端即可。这对初始渲染非常有用，并且可以优化应用性能，从而提供更好的用户体验。
- 开发人员工具 -  从操作到状态更改，开发人员可以实时跟踪应用中发生的所有事情。
- 社区和生态系统 -  Redux 背后有一个巨大的社区，这使得它更加迷人。一个由才华横溢的人组成的大型社区为库的改进做出了贡献，并开发了各种应用。
- 易于测试 -  Redux 的代码主要是小巧、纯粹和独立的功能。这使代码可测试且独立。
- 组织 -  Redux 准确地说明了代码的组织方式，这使得代码在团队使用时更加一致和简单。

## vuex 和 redux 之间的区别

- **redux** 使用的是不可变数据，而 **vuex** 的数据是可变的；
- **redux** 每次都是用新的 `state` 替换旧的 `state`，而 **vuex** 是直接修改；
- **redux** 在检测数据变化的时候，是通过`diff`的方式比较差异的，而 **vuex** 其实和 Vue 的原理一样，是通过 `getter/setter`来比较的(如果看 `vuex` 源码会知道，其实他内部直接创建一个 `Vue` 实例用来跟踪数据变化。
