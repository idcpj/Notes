[TOC]

> [参考手册](https://github.com/axios/axios)
## 安装
`npm install axis -save`

## demo
```
axios.get('/user', {
    params: {
      ID: 12345
    }
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  })
  .then(function () {
    //不管是否出错,请求后执行
  });  

``` 

## Interceptors  拦截器
```
axios.interceptors.request.use(function (config) {
    //请求前操作
    return config;
  }, function (error) {
    return Promise.reject(error);
  });

axios.interceptors.response.use(function (response) {
    得到返回值后的前置操作
    return response;
  }, function (error) {
    return Promise.reject(error);
  });
```
