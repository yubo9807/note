## 版本
1. 每个项目都需注明 node、npm/yarn 版本；
2. 根据业务需求选择 vue(3|2) 版本，老项目考虑升级 vue@2.7；

## 组件
1. 基础组件文件名为 base 开头，使用完整单词而不是缩写；
2. 每个组件都应该放在一个文件夹中，并且文件或文件夹名称不能出现大写，一律采用短横线分割；
    1. git 虽然有相应的配置区分大小写文件，但也要避免不必要的麻烦。

```plain
components
	└─ my-comp
  	├─ readme.md  # 若传参较多，添加组件说明
		├─ index.vue
		└─ item.vue   # 子组件
```

3. 代码中的自行封装的组件引用一律使用大驼峰，第三方 UI 库依然使用短横线方式，jsx 一律使用大驼峰；

```vue
<div>
  <MyComp />
  <el-input />
</div>
```

## 样式
1. 除公共组件外，每个 .vue 文件中的样式必须加 scoped 属性；
2. 在样式较多的情况下考虑引入外部样式文件，并且考虑引入多个模块；

```css
<style lang="scss" scoped>
@import './module.scss';
</style>
```

3. **不准从 UI 设计稿中复制样式**；

## Typescript
1. 项目引入 TS，减少代码低级错误，也方便后续维护；
2. JS 天生不适合做大型/复杂项目（弱类型/解释型）；
3. 在后端返回数据嵌套较深时，考虑使用 TS 装饰器做数据校验；

## composition API
1. option API 数据/函数过于集中，为维护者不太友好；this 指向问题无法更好的支持 TS；
2. 放弃使用 mixins，业务迭代会使代码复杂度直线上升；
3. 使用 hooks 方式编程，将业务功能一致的代码集中化；甚至可以考虑模块引入；

```typescript
export default {
  setup: () => ({
    ...init(),       // 功能模块抽离。建议是一个函数，防止变量污染
    ...operation(),
  })
}
```

## props
1. 利用 TS 类型断言将类型描述具体，并在上方标识块级注释；

```typescript
export default {
  props: {
    /**
     * 需缓存的页面 name 值
     */
    list: {
      type: Array as PropType<string>,
      default: () => [],
    }
  }
}
```

## store
+ 除 uni-app 框架及老项目外，新项目使用 pinia 代替 vuex；

## 数据请求
1. 不建议使用 `response.code === 200`的方式判断接口是否正常返回数据，这样的逻辑放在拦截器中判断；
2. 所有的请求接口函数以 `api_`开头；
3. 报错提示统一在拦截器中判断，并提供字段可取消全局报错；

```typescript
function api_userList(params) {
  return request({
    url: '/api/userlist',
    method: 'get',
    params,
    notips: true,  // 自定义字段，取消全局报错
  })
}
```

```typescript
instance.interceptors.response.use(response => {
  const { data, config } = response;
  if (data && data.code === 200) {
    return Promise.resolve(data);
  } else {
    !config.noTips && ElMessage.error(data.message);
    return Promise.reject(data);
  }
}, error => {})

function asyncto() {
  return promise
    .then(data => [ null, data ])
    .catch(err => [ err, null ]);
}

export default function(option) {
  return asyncto(interface(option));
}
```

```typescript
async function getUserList() {
  const [err, res] = await api_userList();
  if (err) return;
  
  // code...
}
```

