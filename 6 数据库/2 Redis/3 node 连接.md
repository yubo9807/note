# node 连接 redis

`npm install -D redis`

```js
const redis = require('redis');
const client = redis.createClient({
    host: '127.0.0.1',
    post: 6379,
    password: '****'
});

client.set('key', 'value', (err, reply) => {

})

client.get('key', (err, reply) => {

})
```

> redis@4.0 以下不支持 Promise，可借助 node util 中的 promisefy

```js
const redis = require('redis');
const { promisefy } = require('util');
const client = redis.createClient({});

const getAsync = promisefy(client.get).bind(client);

getAsync('name').then(reply => {
    
})
```
