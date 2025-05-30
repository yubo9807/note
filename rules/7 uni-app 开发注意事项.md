**2022.09.23 杨宇波**

## 版本推荐
+ vue2，原因 vue3 对应的 UI 组件库还没有支持到 `.nvue`；
+ 如果想使用 compositionAPI 的写法，可以引入 `@vue/composition-api`和 	`uni-composition-api`（vue2.7 虽然已经发布，但暂时还无法适配 uni）；

## TS
+ 一定要升级到 4.0 版本以上，不然 APP 打包时会有一系列的 TS 报错；

## 配置项
+ 不要给小程序设置 `"lazyCodeLoading": "requiredComponents"`，这个烂属性会导致某些苹果机型白屏；

## 文件
+ `.vue`文件基于浏览器引擎编译，`.nvue`基于原生 APP 渲染引擎编译，两者开发区别差异比较大；
+ 静态文件要放在可以访问的第三方服务器地址或者小程序云资源内（小程序规定代码包不能超过 2MB ）；

## 自定义 tabbar
1. 不要使用微信推荐的 `custom-tab-bar`组件，个人感觉无论是文档还是使用上并不是特别友好；

## 插槽
1. 尽量减少插槽的使用，在 APP 中可能直接导致插槽内容消失；
2. 在 H5 中一切正常，可以获取插槽的个数以及具体内容；
3. 在小程序中只会获取到 `{ default: true }`，这将导致我们无法直接通过插槽内容去做一些事；

```vue
<!-- 组件调用：通过绑定不同的 name 值去实现多个插槽内容 -->
<SwiperCard :angle="4" :width="646" :height="968" :loop="true">
  <template #1>111</template>
  <template #2>222</template>
  <template #3>333</template>
</SwiperCard>

<!-- 组件内容 -->
<view v-for="(item, index) in swiperList" :key="index">
  <slot :name="item" />
</view>

<script>
export default {
  setup() {
    const swiperList = ref([]);

    // 初始化操作
    onMounted(() => {
      /*
        获取插槽：
      	{ 1: true, 2: true, 3: true }
      */
      const arr = Object.keys(current.slots);
      arr.forEach(val => swiperList.push(val));
    })
    // ...

    return { swiperList }
  }
}
</script>
```

## DOM
+ 不要有操作 dom 的想法（`v-html`也不行），一定要通过响应式数据改变；
+ 禁止使用 ref，这样会导致各端不兼容（通过 ref 调用子组件的函数是可以的）；
+ 一律使用 uni 提供的选择器方法，防止选不到，一律传 this；

```typescript
import { ComponentInstance } from '@vue/composition-api';

/**
 * 获取元素 rect
 * @param selector class | id ...
 * @param all 是否多选
 * @returns 
 */
export function getRect(self: ComponentInstance, selector: string, all = false): Promise<UniNamespace.NodeInfo> {
  return new Promise((resolve) => {
    uni.createSelectorQuery()
      .in(self)[all ? 'selectAll' : 'select'](selector)
      .boundingClientRect((rect: UniNamespace.NodeInfo) => {
        if (all && Array.isArray(rect) && rect.length) {
          resolve(rect)
        }
        if (!all && rect) {
          resolve(rect)
        }
      })
      .exec()
  })
}
```

```typescript
export default () => {
  onMounted(async () => {
    const rect = await getRect(current.proxy, '.class');
    console.log(rect);
  })
}
```

## Canvas 画板
+ 小程序中的 canvas 与浏览器中的 canvas 差异比较大，甚至在使用 `.nvue`的 renderjs 也要考虑它的流畅性；

## 环境区分
```typescript
/**
 * 获取环境
 * @returns wxapp   小程序环境
 * @returns wxh5    公众号环境
 * @returns browser 浏览器环境
 * @returns app     APP环境
 */
export function getENVIR() {
  if (!navigator) return 'wxapp';  // 微信开发工具中获取不到 navigator

  const ua = navigator.userAgent.toLowerCase();
  const isWeixin = ua.indexOf('micromessenger') !== -1;
  const isInApp = /(^|;\s)app\//.test(ua);
  if (isWeixin) {
    if ((window as any).__wxjs_environment === 'miniprogram') {
      return 'wxapp';
    } else {
      return 'wxh5';
    }
  } else {
    if (!isInApp) {
      return 'browser';
    } else {
      return 'app';
    }
  }
}
```

## 回调地狱
+ 无论是小程序还是 uni 提供的一些内置函数，很容易出现回调地狱问题；

```typescript
uni.checkSession({
  success() {
    // code...
  },
  fail() {
    uni.login({
      success() {
        // 给后端发送 code
        uni.request({
          url: '/api/login',
        }, {
          success() {
            // code...
          },
          fail() {
            uni.showToast({
              title: '登录失败',
              icon: 'none'
            })
          }
        })
      },
      fail() {
        uni.showToast({
          title: '获取用户信息失败',
          icon: 'none'
        })
      }
    })
  }
})
```

### 将 uni 中的回调函数变为异步函数
```typescript
/**
 * 对微信的内置函数做处理（解决了大部分函数回调地狱问题，个别例外的请自行修改）
 * @param func 微信内置函数
 * @param noTips 取消拦截报错
 * @returns [ error, data ] 请求失败 error == null
 */
export function wechatFuncDealWith(func: Function, option = {}, noTips = false) {

  const promise = new Promise((resolve, reject) => {
    func(Object.assign(option, {
      success(res) {
        resolve(res)
      },
      fail(err) {
        !noTips && uni.showToast({ title: err.errMsg, icon: 'none' })
        reject(err)
      },
    }))
  })

  return asyncto(promise);
}
```

```typescript
onLoad(async () => {

  const [checkErr, checkRes] = await wechatFuncDealWith(uni.checkSession);
  if (checkRes) return;

  // 重新登录
  const [loginErr, loginRes] = await wechatFuncDealWith(uni.login, {}, true);
  if (loginErr) {
    uni.showToast({ title: '获取用户信息失败', icon: 'none' });
    return;
  }

  // 向后端重新发送数据
  const [err, res] = await api_login({});
  if (err) return;

  // code...
})
```

## 钩子函数
+ uni 中特定的一些钩子（`onShow``onHide``...`）无法在子组件中直接使用；

### 将钩子在子组件中变成 hooks
```typescript
import { provide } from "@vue/composition-api";
import { onHide, onLoad, onPageScroll, onShow } from "uni-composition-api"


export type HookName = 'onLoad' | 'onShow'
export type HookItem = {
  name: HookName
  hook: Function
}
export type HookFunc = (hookName: HookName, func: Function) => {}

export const ADD_HOOK_FUNC = 'addHookFunc';

/**
 * 子组件无法直接使用 uni 中的一些钩子
 * 向子组件注入一些钩子
 * 使用：引入到父组件当中，在子组件中使用 inject 添加相应的钩子
 */
export default () => {

  const hookFuncList: HookItem[] = [];  // 收集钩子函数

  // 向子组件提供一个可以调用钩子的函数
  provide(ADD_HOOK_FUNC, (name: HookName, hook: Function) => {
    hookFuncList.push({ name, hook });
  })

  const promise = Promise.resolve();

  /**
   * 执行对应的钩子函数
   * @param hookName
   * @param params 钩子自带参数
   */
  async function performFunc(hookName: HookName, params: any = void 0) {
    await promise;  // 在微队列中执行这些添加的钩子
    const funcList = hookFuncList.filter(val => val.name === hookName);
    funcList.forEach(val => val.hook(params));
  }


  // #region 执行对应收集到的钩子
  onLoad(option => performFunc('onLoad', option));

  onShow(() => performFunc('onShow'));
  // #endregion


  return {}
}
```

```typescript
export default (props, context) => {
  const hookFunc: HookFunc = inject(ADD_HOOK_FUNC);
  hookFunc('onShow', () => {
    console.log('onshow 1111');
  })
  hookFunc('onShow', () => {
    console.log('onshow 2222');
  })
}
```



