# Axios 对接开发规范

> Axios 是一个基于 Promise 的 HTTP 客户端，适用于浏览器和 node.js。本文档旨在提供 Axios 在项目中对接后端 API 的开发规范，以确保代码的一致性、可维护性及效率。



## 1. Axios 实例化

为了方便管理和维护，推荐为不同的业务或后端服务创建独立的 Axios 实例。

```javascript
import axios from 'axios';

const apiClient = axios.create({
  baseURL: 'https://api.example.com',
  timeout: 1000,
  headers: {'X-Custom-Header': 'foobar'}
});
```



## 2. 请求和响应拦截器

使用请求和响应拦截器可以在请求发送或响应返回前统一处理数据或逻辑，如添加认证信息、处理错误等。

### 请求拦截器

```javascript
apiClient.interceptors.request.use(config => {
  // 在发送请求之前做些什么，例如添加token
  config.headers.Authorization = `Bearer ${token}`;
  return config;
}, error => {
  // 对请求错误做些什么
  return Promise.reject(error);
});
```

### 响应拦截器

```javascript
apiClient.interceptors.response.use(response => {
  // 对响应数据做点什么
  return response;
}, error => {
  // 对响应错误做点什么
  return Promise.reject(error);
});
```



## 3. API 封装

封装 API 函数可以提高代码的复用性和可维护性。推荐将相关 API 封装在同一个模块或服务中。

```javascript
const userService = {
  getUser(id) {
    return apiClient.get(`/users/${id}`);
  },
  createUser(data) {
    return apiClient.post('/users', data);
  },
  // 其他用户相关的API
};
```



## 4. 错误处理

对于 Axios 请求的错误处理，推荐使用`try...catch`结构，并结合`async/await`语法提高代码的可读性。

```javascript
async function fetchUser(id) {
  try {
    const response = await userService.getUser(id);
    console.log(response.data);
  } catch (error) {
    console.error('Error fetching user:', error);
    // 根据错误类型做出相应处理
  }
}
```



## 5. 取消请求

Axios 提供了取消请求的功能，这在组件卸载时取消未完成的请求或避免重复请求时非常有用。

```javascript
const { CancelToken } = axios;
let cancel;

apiClient.get('/users', {
  cancelToken: new CancelToken(function executor(c) {
    // executor 函数接收一个 cancel 函数作为参数
    cancel = c;
  })
});

// 取消请求
cancel('Operation canceled by the user.');
```



## 6. 超时处理

设置请求超时时间可以避免因后端服务响应缓慢而导致的页面卡顿。

```javascript
apiClient.get('/users', {
  timeout: 5000 // 设置超时时间为 5 秒
});
```