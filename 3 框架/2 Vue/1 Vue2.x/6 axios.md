# axios

### 发送请求

```js
axios({
    method: 'get',  // 请求方式
    baseURL: '',  // 请求的域名，基本地址
    url: '',  // 请求路径
    params: {},  // 会将请求的参数拼接到 url 上
    data: {},  // 会将请求参数放在请求体中
    headers: {},  // 设置请求头
    timeout: 1000,  // 请求超时
})
```

> 设置默认 baseURL：axios.defaults.baseURL = '域名';

### 并发

```js
axios.all([
    axios.get('/a'),
    axios.get('/b'),
]).then(axios.spread((aRes, bRes) => {
    console.log(aRes, bRes);
}));
```

### 拦截器

```js
axios.interceptors.request.use(config => {
    config.methed = 'POST';  // 改变请求方式
    config.url = '/data';  // 改变请求地址
    return config;
});
```

```js
axios.interceptors.response.use(response => {
    if (response.status == 200) {
        return response.data;
    } else {
        // ...
    }
});
```

#### 取消拦截

```js
let interceptors = axios.interceptors.response.use();
axios.interceptors.response.eject(interceptors);
```

#### 拦截实例

```js
const instance = axios.create();
instance.interceptors.request.use();
```
